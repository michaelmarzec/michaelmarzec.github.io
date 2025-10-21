---
layout: post
title: "NBA-Age Analysis: Infrastructure"
comments: false
---

<h3 style="text-align: center;"><a href="https://nbaage.com/"><ins>nbaage.com</ins></a></h3>

When analysts, media members, and fans discuss the average age of an NBA team, there’s often a missing nuance. Typically, there will be a statement like “Team X is the 5th youngest team in the NBA”, and that information results from a quick average of every member of the roster. In my opinion, this fails to convey an accurate representation, as that average is skewed by low usage and end-of-bench players.

#### Information Objective

My goal is to present an innovative view of NBA team ages. Rather than convey that the Minnesota Timberwolves are the 7th youngest team, I’d like to explain that the Timberwolves are the 5th youngest team when weighted by minutes and the 4th youngest team when weighted by usage rate. This could indicate that the Wolves rely on young players surrounded by older low-usage veterans. We can also see that their team-wide average is pulled up by the ‘Combo’ position (i.e., Patrick Beverly). Over a full season, perhaps we can identify inflection points such as key injuries or when a team decides to ‘tank'.

#### Infrastructure Objective

During development, I aimed to create a tech stack that will (for cheap, if not free) provide a clean, easy-to-interpret, and automated presentation of NBA team ages. This infrastructure should reduce, if not entirely eliminate, manual upkeep, allowing for time spent analyzing the data and enhancing website functionality.

#### Data Extraction

All data is extracted (nightly) using Python (BeautifulSoup, urllib, etc.), automated via AWS Lambda, stored in S3, and scraped from Ben Falk’s <ins>[cleaningtheglass.com](https://cleaningtheglass.com/)</ins>. A couple of lessons learned:
- When developing an AWS Lambda function, keep it lightweight. There is a compressed limit of 50mb.
- In this instance, I adjusted from storing data in a Parquet file (my preferred local storage method) to a CSV, so I could remove the PyArrow library.
- <ins>[Linked](https://github.com/keithrozario/Klayers/blob/master/deployments/python3.8/arns/us-east-2.csv)</ins> is a fantastic resource for Python ARNs.

#### Front End

The web framework is developed using the Flask library. Data is ingested from S3 (i.e., Boto3), which conveniently creates an automated pipeline due to the Lambda function. The data is manipulated via a handful of Pandas operations, which feed the <ins>*[sortable](https://flask-table.readthedocs.io/en/stable/#sortable-tables)*</ins> data table and the time-series data to HTML templates.

The HTML table template uses a basic structure and a simple CSS file (i.e., the bulk of the research/work was completed via the Flask-Table library). 

The HTML time-series template uses Chart.js and a slightly more complex CSS file:
- I manually created a JSON set for each team which strikes me as an opportunity for improvement via some type of an automated for-loop solution.
- My flex-wrapper class was a lifesaver. I struggled to station the footer below the chart, but the combination of ‘display’, ‘flex-direction’, and ‘justify-content’ resolved the issue.

#### Deployment

This website might not exist without <ins>[Zappa](https://github.com/zappa/Zappa)</ins>. For anyone unfamiliar, the library uses AWS Lambda (as such, this website leverages Lambda twice … perhaps another point for improvement) to serve a Python application and connect it via Amazon’s API Gateway. Zappa’s user interface requests a few basic parameters, and a quick Google search will provide helpful hints like leveraging the pre-built slim_handler, using the AWS us-east-2 region, and the ‘zappa tail’ function for troubleshooting.

#### Custom Domains: Process Walkthrough 

In addition, Zappa allows for custom domains. The following is a quick walkthrough for any newcomers that would like to consolidate the research process:
- I love <ins>[Google Domains](https://domains.google.com/)</ins>. It has an accessible interface, which is simple to maintain and does not require managing another new website account (assuming you already have a Google account). Buy your favorite domain and move along.
- In the AWS Certificate Manager, request a ‘Public Certificate’, enter a domain name, and request a DNS validation. Once this is available, select the option to ‘Create records in Route 53’.
- In AWS Route 53, there is an NS-Type record name for your domain. Copy the four NS ‘routes’ (e.g., ns-1000.awsdns-11.org.), open the DNS:Custom Name Servers tab in Google Domains, and save the four different NS values.
- The custom domain should now be active. Take the ARN value from your AWS Certificate page, and add the following in your zappa_settings.json file:
“certificate_arn”: “arn_value”, “Domain” : "custom_domain”
- Run a zappa update *project name* and your domain should be live.

#### Sign Off

For anyone who is still reading, I hope this helped. Please feel free to reach out with any questions, comments, or ideas for <ins>[nbaage.com](https://nbaage.com/)</ins>!

Any significant infrastructure updates will be added here, and I plan to post analysis using this data-–as usual, the data pipeline and visualization is just the first step. In addition, if you attempt to replicate this process and encounter any errors, shoot me an email and I’ll be happy to give you my best effort.
