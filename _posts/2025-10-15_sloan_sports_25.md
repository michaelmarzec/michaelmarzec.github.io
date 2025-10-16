---
layout: post
title: "2025 Sloan Sports Conference: Research Papers"
comments: false
---



I am back with more thoughts on Sloan Sports Research Papers! This year, I'll stick to three papers that caught my eye.


### [CoachAI+ Badminton Environment: A Realistic Badminton Game Simulator for Enhancing Player Performance](https://www.sloansportsconference.com/research-papers/coachai-badminton-environment-realistic-badminton-game-simulator-for-enhancing-player-performance)

As a self-proclaimed tennis nerd (an analytics venture I am hoping to dive deeper into soon), I was immediately drawn to this badminton analysis, a sport that clearly carries enough similarity to tennis. As a bonus, I find markov-decision processes (MDP) theory particularly useful (perhaps I am biased due to its potential applicability to a couple of work projects) but regardless, I was excited to see how this work drew an intersection between the two.

In short, the paper uses MDP to simulate badminton matches and extract insights on strategy, performance, and touches on predicted match outcomes. More specifically, it translates badminton gameplay into tabular data (BLSR) – I assume this is similar to Jeff Sackman's [match charting](https://github.com/JeffSackmann/tennis_MatchChartingProject) – simulates gameplay dynamics using latent geometric brownian motion (LGBM) and deploys an MDP based on player-specific historical data.

I was impressed by a novel concept (to me, at least): Realism Constraints. The paper explains a few complementary forms of constraint, including shot type, court and behavior. These constraints improve simulation accuracy by constraining the agents (i.e., players) to realistic action and as a by-product helps with labeling error. I found there were some limitations that seemed aggressive (e.g., I was surprised that a response to a lob has to be a smash or a drop shot), however, I'll hold any criticism considering a significant lack of familiarity with badminton (and subjective analysis is essentially comparing it to tennis).

The concept provides a critical heuristic to a technical approach that can otherwise fall astray. I also wonder if it limits innovative strategic discoveries – if there's an approach a player should take that falls outside the realistic boundaries. However, that might be better suited for the strategic style of play section of this paper, rather than a limitation of a boundary set to improve simulation efficacy.

The last piece, and probably the most critical, was the match analysis. This approach can identify strategies (based on a pre-determined set of strategies), evaluate the effectiveness of each, and identify strengths and weaknesses in future opponents. For example, the pace of a shot was used to imply success in a matchup (slower was actually better in this instance). But I'd be curious whether hitting slower is a result of a specific strategy that worked, or in isolation led to better results (i.e., correlation vs causation).

Altogether, I'd love to see this analysis applied to tennis! There's really interesting concepts in the MDP approach and certainly has large potential to be generalized.

### [Beyond the Box Score: Using Psychological Metrics to Forecast NBA Success](https://www.sloansportsconference.com/research-papers/beyond-the-box-score-using-psychological-metrics-to-forecast-nba-success)

Improving forecasting accuracy on anything NBA related (and especially drafting) feels like a game played at the margins, which drew my attention to this paper. In short, the researchers claim to add roughly 5% accuracy to the prediction accuracy of a player making an NBA roster (and provide complementary survival analysis on the longevity of an NBA player measured by games played and by games started).

I think there are similarities to last year's paper around measuring competitiveness (see "[Measuring Individual Competitiveness](https://michaelmarzec.github.io/sloans_sports_24)"). In other words, another approach to quantifying what was once considered an intangible – an ongoing evolution in sports analysis.

Returning to the "psychological metrics", this paper uses a narrowed linguistics dataset that captures interviews and press conferences from NCAA championship games and evaluates using lightGBM and survival models (cox-proportional hazard and kaplan-meier).

The results are promising. Using psychological metrics alone improves over random choice and adding the LIWC (Linguistic Inquiry and Word Count) features consistently improves performance and attribute-based models. However, I think the narrow dataset leaves significant room for additional testing.

While the paper defends the selection-—important players on championship teams are interviewed—-this creates potential for selection bias. Not to mention that the paper compares lightGBM models (LIWC vs performance-based) using different datasets.

The concept is applicable beyond draft models and extends to other sports (which the paper calls out). However, the research doesn't yet convince me that LIWC is independently predictive. Rather, this data can augment existing models—though it needs additional testing across larger populations to validate its true impact.

### [CLIPP: Causal Impact of Offensive Linemen on Pass Plays](https://www.sloansportsconference.com/research-papers/causal-impact-of-offensive-linemen-on-pass-plays)

This is the most technically impressive and important paper that I have read in recent memory. As a quick summary, the research uses causal analysis (!) to measure the impact of individual offensive lineman on passing plays (specifically, passing completions).

The approach removes confounding variables and unbiased effect estimation using a causal framework: CATE (conditional average treatment effect) based on a treatment (QB pressures, hits, and sacks), an outcome (completions) and features (a tracking dataset from the 2023 NFL Big Data Bowl).

It uses a doubly robust estimation by combining outcome regression (predicting outcome based on T and features X) with propensity score weighting (probability of receiving T based on features X). In significant over-simplification, by balancing covariates for the treated and untreated groups, it can predict outcomes in an unbiased manner.

They also have a detailed walkthrough of various critical tests – covariate balancing (standardized mean differencing tests), placebo tests, subsampling, goodness of fit checks, and sensitivity analysis (i.e., omitting confounders and subsequent tests).

What makes this impressive is its focus on causality. A lot of research—corporate and academic alike—focuses on novel concepts and technically complex models, but loses sight of the day one foundation: we want causation, not correlation. This is obviously a bit dramatized, but the critique is consistent.

Causality can be incredibly difficult to prove: both difficult to find in the data and a technically challenging process. This paper successfully identifies causality, validates it with realistic comparisons (e.g., PFF rankings, All-Pro elections), and identifies next steps like weather and crowd effects.

This research is extremely exciting to me – it's production-grade and genuinely useful. The paper references other applications, and the framework could extend to domains like NBA defense, using tracking data to identify causal impact on team defensive performance.
