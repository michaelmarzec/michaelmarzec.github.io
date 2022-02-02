---
layout: post
title: "NBA-Age Analysis: Infrastructure"
comments: false
---

<h3 style="text-align: center;"><a href="https://nbaage.com/"><ins>nbaage.com</ins></a></h3>

When analysts, media members, and fans discuss the average age of an NBA team, there’s often a missing nuance. Typically, it’s a reference like “Team X is the 5th youngest team in the NBA” and that marker results from a quick average of every roster member. In my opinion, this fails to convey an accurate representation as that average is skewed by low usage and end-of-bench players.

#### Information Objective

Present an innovative view of NBA ages. Rather than convey that the Minnesota Timberwolves are the 7th youngest team, I’d like to explain that the Timberwolves are the 5th youngest team when weighted by minutes and the 4th youngest team when weighted by usage rate. This could indicate that the Wolves rely on young players surrounded by older low-usage veterans. We can also see that their team-wide average is pulled up by the ‘Combo’ position (i.e., Patrick Beverly). Over a full season, perhaps we can identify inflection points such as key injuries or when a team decides to ‘tank.’ 

#### Infrastructure Objective

Develop a tech stack that will (for cheap, if not free) provide a clean, easy-to-interpret, and automated presentation of NBA team ages. This infrastructure should reduce, if not eliminate, manual upkeep, allowing for time spent analyzing the data and enhancing website functionality.

#### Data Extraction

All data is extracted (nightly) using Python (BeautifulSoup, UrlLib, etc.), automated via AWS Lambda, stored in S3, and scraped from Ben Falk’s <ins>[cleaningtheglass.com](https://cleaningtheglass.com/)</ins>. A couple of lessons learned:
- When developing an AWS Lambda function, keep it lightweight! There is a compressed limit of 50mb.
- In this instance, I adjusted from storing data in a Parquet file (my preferred local storage method) to a CSV, so I could remove the PyArrow library.
- <ins>[Linked](https://github.com/keithrozario/Klayers/blob/master/deployments/python3.8/arns/us-east-2.csv)</ins> is a fantastic resource for Python ARNs.

#### Front End

The web framework is developed using the Flask library. Data is ingested from S3 (i.e., Boto3), which conveniently creates an automated pipeline due to the Lambda function. The data is manipulated via a handful of Pandas operations, which feed the <ins>*[sortable](https://flask-table.readthedocs.io/en/stable/#sortable-tables)*</ins> data table and the time-series data to HTML templates.

The HTML table template uses a basic structure and a simple CSS file (i.e., the bulk of the research/work was completed via the Flask-Table library). 

The HTML time-series template uses chart.js and a slightly more complex CSS file:
- I manually created a json set for each team which strikes me as an opportunity for improvement via some type of an automated for-loop solution.
- My flex-wrapper class was a lifesaver. I struggled to station the footer below the chart, but the combination of ‘display’, ‘flex-direction’, and ‘justify-content’ resolved the issue.

#### Deployment

This website might not exist without <ins>[Zappa](https://github.com/zappa/Zappa)</ins>. For anyone unfamiliar, the library uses AWS Lambda (as such, this website leverages Lambda twice … perhaps another point for improvement) to serve a Python application and connect it via Amazon’s API Gateway. Zappa’s user interface requests a few basic parameters and a quick Google will provide you with helpful hints like leveraging the pre-built slim_handler, using the AWS us-east-2 region, and the ‘zappa tail’ function for troubleshooting.

In addition, Zappa allows for custom domains. The following is a quick walkthrough for any newcomers that would like to consolidate the research process:
- I love <ins>[Google Domains](https://domains.google.com/)</ins>. Accessible interface, simple to maintain and you don’t have to manage another new website account. Buy your favorite domain and continue.
- In the AWS Certificate Manager, request a ‘Public Certificate’, enter your domain name, and request a DNS validation. Once this is available, select the option to ‘Create records in Route 53.’
- In AWS Route 53, you should now have an NS-Type record name for your domain. Copy the four NS ‘routes’ (e.g., ns-1000.awsdns-11.org.), open the DNS:Custom Name Servers tab in Google Domains, and save the four different NS values.
- Your custom domain should be active now! You just need the ARN value from your AWS Certificate page. In your zappa_settings.json file add the following:
“certificate_arn”: “arn_value”
“Domain”:”custom_domain”
- Run a zappa update *project name* and your domain should be live!

#### Sign Off

For anyone who is still reading, I hope this helped. Please feel free to reach out with any questions, comments, or ideas for <ins>[nbaage.com](https://nbaage.com/)</ins>! I intend for it to evolve, but we all know life can get in the way. 

Any significant infrastructure updates will be added here and I plan to post analysis using this data-–as usual, the data pipeline and presentation is just the first step. In addition, if you attempt to replicate this process and encounter any errors, shoot me an email and I’ll be happy to give you my best effort.
