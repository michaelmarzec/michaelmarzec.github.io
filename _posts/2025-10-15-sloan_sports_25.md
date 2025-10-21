---
layout: post
title: "2025 Sloan Sports Conference: Research Papers"
comments: false
---



I am back after another batch of Sloan Sports Research papers. This year I'm sticking with three that caught my eye.


### [CoachAI+ Badminton Environment: A Realistic Badminton Game Simulator for Enhancing Player Performance](https://www.sloansportsconference.com/research-papers/coachai-badminton-environment-realistic-badminton-game-simulator-for-enhancing-player-performance)

As a self-proclaimed tennis nerd (and someone hoping to dig deeper into tennis analytics soon), I was immediately drawn to this badminton analysis. The two sports share clear similarities, and as a bonus, I have a particular interest in Markov decision process (MDP) theory, partly because of its potential relevance to a few projects at work. Either way, I was excited to see how this paper connected the two.

In short, the authors use MDPs to simulate badminton matches and extract insights on strategy, performance, and predicted outcomes. They translate gameplay into structured tabular data (BLSR) —- which I assume is similar to Jeff Sackmann’s [match charting](https://github.com/JeffSackmann/tennis_MatchChartingProject) —- simulate dynamics using latent geometric Brownian motion (LGBM), and build MDP models trained on player-specific historical data.

One of the more novel ideas here (at least to me) was the introduction of realism constraints: rules around shot type, court position, and player behavior. These constraints improve simulation accuracy by forcing the modeled players to behave realistically and help reduce labeling error. Some seemed overly strict (for example, a lob can only be countered by a smash or drop shot), but I’ll hold any criticism and defer to the badminton experts on that.

Realism constraints serve as an important heuristic for a technical approach that might otherwise drift too far from real-world play. That said, I do wonder whether they limit the discovery of innovative strategies — moves that might fall outside the “realistic” bounds but could still be effective. However, that might be better suited to the paper’s discussion of strategic style of play rather than a critique of the constraints themselves, which are attempting to improve simulation accuracy.

The most compelling piece, though, was the match analysis. This section identifies which strategies players used (based on a pre-defined set of strategies), evaluates their effectiveness, and identifies strengths and weaknesses in future opponents. For example: slower shot pace correlated with better outcomes for a certain player. That raises a key question: was success driven by slower play itself, or by strategies that happened to involve slower shots? (In other words: correlation vs. causation).

Altogether, I'd love to see this analysis applied to tennis! There's really interesting concepts in the MDP approach and certainly has potential to be generalized across various sports.

### [Beyond the Box Score: Using Psychological Metrics to Forecast NBA Success](https://www.sloansportsconference.com/research-papers/beyond-the-box-score-using-psychological-metrics-to-forecast-nba-success)

Improving forecasting accuracy in the NBA (especially around the NBA draft) feels like a game played at the margins, which drew my attention to this paper. In this work, the researchers claim a 5% boost in predicting whether a player will make an NBA roster, and provide complementary survival analysis by modeling career longevity (via games played and games started).

Side note: this paper reminds me of last year’s [Measuring Individual Competitiveness](https://michaelmarzec.github.io/sloans_sports_24) paper -- another approach to quantifying 'intangible' traits... an ongoing evolution in sports analysis.

Returning to "psychological metrics", this paper uses a narrowed linguistics dataset that captures interviews and press conferences from NCAA championship games and evaluates using lightGBM and survival models (Cox-proportional hazard and Kaplan-Meier).

The results are promising. Psychological metrics alone outperform random baselines, and adding LIWC (Linguistic Inquiry and Word Count) features consistently improves both performance and attribute-based models. Still, the dataset feels narrow, leaving room for much broader validation.

The authors justify this selection -— important players on championship teams are typically interviewed and are often top NBA prospects -- which could introduce potential selection bias. Moreover, the paper compares LightGBM models (LIWC vs. performance-based) trained on different datasets, complicating the results.

Even with those caveats, the concept has real potential to enhance NBA draft forecasting and to be applied across other sports (as the paper notes). I’m just not yet convinced that LIWC features are independently predictive. For now, they seem better suited to complementing traditional performance metrics -— an intriguing signal that warrants larger-scale testing.

### [CLIPP: Causal Impact of Offensive Linemen on Pass Plays](https://www.sloansportsconference.com/research-papers/causal-impact-of-offensive-linemen-on-pass-plays)

This is the most technically impressive and important SSAC paper that I have read in recent memory. The research uses causal inference (!) to measure the individual impact of offensive lineman on passing plays (specifically, passing completions).

The approach removes confounding variables and unbiased effect estimation using a causal framework: CATE (conditional average treatment effect) based on a treatment (QB pressures, hits, and sacks), an outcome (completions) and features (a tracking dataset from the 2023 NFL Big Data Bowl).

They employ a doubly robust estimation approach, combining outcome regression (predicting completion based on treatment and features) with propensity score weighting (the probability of receiving a given treatment). In simplified terms, by balancing covariates between treated and untreated groups, they isolate causal effects rather than correlations.

The paper also walks through a series of thorough validation tests: covariate balancing (via standardized mean difference), placebo and subsampling checks, goodness-of-fit assessments, and sensitivity analyses (testing robustness to omitted confounders).

I am genuinely impressed by its focus on causality. A lot of research -— academic and corporate alike —- chase novel concepts but lose sight of the underlying objective: identifying causal drivers of performance, not just correlations. This paper does not. It demonstrates causality convincingly, validates its findings against real-world benchmarks like PFF rankings and All-Pro selections, and even outlines natural extensions such as incorporating weather and crowd effects.

I found this research genuinely exciting. It is production-grade and practical. The framework could easily be adapted to other sports, like using tracking data to measure the causal impact of defenders in the NBA. I recommend giving it a read!
