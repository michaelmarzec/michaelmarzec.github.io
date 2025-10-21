---
layout: post
title: "2024 Sloans Sports Conference: Research Papers"
comments: false
---



Dating to 2017, I’ve developed a habit of reading about five papers from the Sloan Sports Analytics Conference’s research paper competition. This tradition started after I attended the 2017 conference in person–the only time I’ve attended live. I sat in on a few keynote speakers with recognizable names (e.g., Bob Myers, Nate Silver, Mark Cuban) but found myself drawn to the research paper presentations. They felt more aligned with the innovative spirit of the conference–or perhaps with my bias towards the underlying data-driven work.

Regardless, I figured I might as well begin capturing my notes for posterity's sake. And with that said, here are my brief, unorganized, and long overdue thoughts on my five favorite papers from the 2024 conference.


### [Approaching In-Venue Quality Tracking from Broadcast Video using Generative AI](https://assets-global.website-files.com/5f1af76ed86d6771ad48324b/65bfe3cc13cac76100ab0611_193972%20-%20Approaching%20In-Venue%20Quality%20Tracking%20from%20Broadcast%20Video%20using%20Generative%20AI.pdf)

It seems that from every casual ChatGPT user to SaaS industry leader, there’s a genuine curiosity about how generative AI can be practically and widely applied. This paper is a great example!

The authors demonstrate how diffusion models can augment missing tracking data by leveraging event data. In theory, tracking data can eventually be democratized. For instance, in American professional sports, there are finite teams and thus stadiums which makes it feasible for all organizations to equip their facilities with appropriate tracking cameras.

But what about minor leagues, international competition (this research focused on soccer broadcasting), and various levels of college, or even high school sports? This method could provide a valuable tool within these contexts, or for professional organizations scouting talent within these settings.

The testing methodology was relatively straightforward. The authors compared tracking data from a soccer match equipped with full tracking capabilities against the same match reconstructed using only broadcast and event data. The results were impressive, achieving at least 94% accuracy compared to the original in-venue tracking software.

While some sports, like basketball, have broadcasts that inherently capture most, if not all, of the playing field, this approach seems particularly promising for sports like football across the various levels mentioned above. Altogether, this is a novel approach to ensembling data and applying generative AI to successfully approximate comprehensive tracking capabilities.

### [Analyzing NBA Player Positions and Interactions with Density-Functional Fluctuation Theory](https://assets-global.website-files.com/5f1af76ed86d6771ad48324b/65bff386803e405540a9d279_193938%20-%20Analyzing%20NBA%20Player%20Positions%20and%20Interactions.pdf)

There are countless statistical approaches to understanding an NBA player’s shooting performance. Tracking data has enabled metrics like field goal percentage while controlling for location on the floor, the shooter’s typical success from said spot on the floor, and the nearest defender’s positioning.

This paper takes it a step further by accounting for the impact of _all_ players on the floor on a shot’s probability of success. Rather than dive into the methodology, I want to highlight some intriguing applications.
First, the concept of _player gravity_ is particularly compelling. The paper refers to the attention a player commands from the defense, which influences the effectiveness of the entire offense. For example, when Steph Curry is on the court, his mere presence draws defenders, opening opportunities for his teammates, whether or not he’s the one taking the shot. While gravity can be inferred from high-level stats like on/off court metrics, this paper provides a more granular approach.
Another potential application lies in coaching. Using this methodology, a coach could design plays by evaluating scenarios like: _If players 2-5 are positioned at spots B-E, where is the optimal shooting location for player 1?_ While correlation versus causation issues may arise, such insights could serve as complementary data for refining playbooks.
Defensively, this methodology could have even broader implications. It could help define optimal defensive alignments or strategies—such as zone vs. man-to-man, pick-and-roll coverage, or weak-side rotation strategy—to minimize offensive success. Additionally, it might allow for isolating individual players to evaluate their impact on defensive efficiency, offering a unique approach to encapsulating a player’s defensive impact.
Finally, this concept could extend to other sports, like tennis. By analyzing variables such as ball speed, spin, location, and player positioning, this approach could theoretically identify the optimal shot for an attacking player to hit or the best recovery position for the defensive player. The potential for this type of analysis across sports is both fascinating and promising.

### [Estimating NBA Team Shot Selection Efficiency from Aggregations of True, Continuous Shot Charts: A Generalized Additive Model Approach](https://assets-global.website-files.com/5f1af76ed86d6771ad48324b/65bfe5b6d3687858ab4b2552_193942%20Estimating%20NBA%20Team%20Shot%20Selection%20Efficiency%20from%20Aggregations%20of...%20.pdf)

The _GAN Approach to NBA Team Shot Selection Efficiency_ paper provides a more statistically relevant take on the classic NBA red-to-green shot chart by incorporating free throw impact via a GAM model. Traditional points-per possession (PPP) shot charts overlook field goal attempts (FGAs) that went unrecorded due to a defensive foul. This method addresses that gap, effectively increasing the weight of shots near the basket.

The paper also includes a [web app](https://sportdataviz.syr.edu/TrueShotChart/) that will quickly kill thirty minutes by exploring your favorite teams over the years. For example, check out Anthony Edwards 2022 shot chart: the GAM model reveals a lot more red near the hoop!
A key focus of the paper is refining our understanding of the value of a three-pointer versus a two-pointer. It notes:
>"In 2021-22, there was no significant leaguewide three-point premium or dispremium when considering aggregations of traditional shot charts. However, when considering aggregations of true shot charts, we find a significant and deepening three-point dispremium at the league level since the 2018-19 season."

Interestingly, in the 22-23 and 23-24 seasons, the average three-point attempts (3PA) declined indicating a potential league-wide adjustment to a dispremium. However, in the 24-25 season, as of writing this post, there’s been a sharp incline to 37.4 3PA per game (from 35.1 in 23-24) suggesting that teams did not actually recognize a dispremium.

Altogether, 3PA is a piece to the puzzle, rather than the puzzle itself. This paper highlights that there are other factors impacting offensive efficiency, but it’s enlightening (and a bit refreshing) to read a quantitative outlook on a 3-point premium cap.

### [How to Predict the Performance of NBA Draft Prospects](https://assets-global.website-files.com/5f1af76ed86d6771ad48324b/65bff115e0833ee8efc4a5b5_193977%20-%20How%20to%20Predict%20the%20Performance%20of%20NBA%20Draft%20Prospects.pdf)

The NBA draft is widely acknowledged as a probabilistic gamble, introducing randomness and luck into an otherwise quantitatively-refined industry. Yet, any edge that increases a team’s chances of drafting the right player is invaluable.

This paper introduces relevance-based prediction algorithms to NBA draft prospect modeling domain. Specifically, this entails using relevance, fit, and codependence. Practically speaking, this involves algorithmically narrowing the sample to historical comparisons deemed most similar to the player being evaluated, thereby improving the model's predictive accuracy.

Beyond improving prediction accuracy, the authors keenly highlight another critical benefit to this approach: model transparency. Relevance-based algorithms provide clear insights into how historical comparisons influence predictions. For example, the paper highlights Mark Williams' top three comparisons: TJ Leaf, Marvin Bagley and Brice Johnson. In other words, those annoying (and often arbitrary) draft-day player comparisons can finally leverage quantitative reasoning, and an analytics team can better translate its models for the front office.

Overall, I find using relevance-based predictions to be a novel and useful approach. However, the paper acknowledges one of its own shortcomings: a lack of applied independent variables. Certainly, a production-ready version would incorporate more college data and player attributes (e.g., wingspan). 

A personal gripe is the use of _minutes played_ as a dependent variable. Minutes played can be highly influenced by draft position—higher picks often receive more minutes due to financial investment and public expectations. I’ve read various papers and models that use an all-in-one metric like VORP, EPM, etc. and look at performance over a player's first few years, career lifespan, or career peak, depending on what you are optimizing for. But again, this can be easily fixed if the model was translated to a production state.

Overall, relevance-based predictions offer a compelling way to enhance NBA draft modeling, blending accuracy, transparency, and practicality to bring new rigor to a high-stakes process.

### [Measuring Individual Competitiveness](https://assets-global.website-files.com/5f1af76ed86d6771ad48324b/65bfe462a965e37488b51bb6_193966%20-%20Measuring%20Individual%20Competitiveness%20and%20its%20Impact%20on%20Sporting%20Success.pdf)
My favorite paper! This research measures competitiveness in youth athletes and their coaches, using an incredible dataset and a novel approach. Specifically, the authors measure how competitive each athlete is, whether competitiveness is coachable, if competitiveness is predictive of future success, and how age (from 10-18) impacts these factors.

The analysis uses data collected from Athletic Bilbao’s elite Spanish Youth Academy, covering athletes from 2011 to 2018 and tracking their subsequent results through 2023. During the 2011-2018 timeline, athletes were tested via various objective experiments to evaluate competitiveness complemented by anecdotal evidence provided by the coaches (for athletes) and the head of the academy (for coaches).

In short, the paper suggests that a competitive coach can increase competitievness in their athletes, which can lead to higher likelihood of professional athletic success.

However, age is a significant factor.
- Under 13: Overly competitive coaching can negatively impact athletes. This perhaps aligns with the idea that at a young age, it’s more important to draw children into the sport than to push them too hard. 
- 13-16: This is the sweet spot. A competitive coach can, on average, significantly impact the likelihood of their athletes future success. Using the author’s methodology, if a player converts from 0 to 1 in competitiveness, they have a 10% higher probability of a professional contract.
- Over 16: At this stage, competitive coaching has no significant impact.

I highly recommend reading this paper. The authors do an incredible job at tackling such an abstract topic, and successfully align their methodology with the long-term timeline of soccer academies.

Accordingly, I would love to see similar research conducted at a tennis academy. In part, due to a bias for tennis and in larger part I’d like to see how results compare within a more individualistic domain.

Finally, the authors briefly discuss the differences in early childhood competitiveness between boys and girls. The paper references research that considers how boys are stereotypically placed into more competitive environments via cultural norms. In turn, social scientists have drawn a hypothesis between competitive upbringings contributing to male and female labor market differentials.

Male versus female competitiveness and its connection to labor markets is a BIG topic. This paper merely comments on it, and I can’t pretend to add anything more. But I think it’s an interesting callout, especially as this paper introduces quantification of competitive nature, and how it can both project athletic success and in this grander context, societal implications such as a theoretical economic impact.
