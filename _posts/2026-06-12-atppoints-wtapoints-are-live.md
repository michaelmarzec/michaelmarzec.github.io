---
layout: post
title: "atppoints.com and wtapoints.com are Live!"
comments: false
---

<h3 style="text-align: center;"><a href="https://atppoints.com/"><ins>atppoints.com</ins></a> | <a href="https://wtapoints.com/"><ins>wtapoints.com</ins></a></h3>

ATP and WTA rankings are fascinating in that they determine player seedings but are rarely reflective of the true order of player ability. They're global to all surfaces (as they should be), but entering a tournament, favorites are surface-specific. It's already well-reflected in win probability models (e.g., gambling odds, Elo ratings) that rankings don't always equate to being better than your opponent. Additionally, points can be unevenly distributed: a player might be heavily reliant on a single tournament, or their points might be skewed toward a specific level of competition (e.g., dominating 500s but struggling against higher-level competition in 1000s or Grand Slams). I wanted more nuance when evaluating a player's ranking, and I couldn't find a tool that provided it, so I built one.

### What is it?

[atppoints.com](https://atppoints.com/) and [wtapoints.com](https://wtapoints.com/) are ranking points trackers for the ATP and WTA tours, respectively. Both sites break down each player's ranking points by tournament, so you can see exactly where their points originate.

On the table view, you can filter by surface, tournament level, and date range to slice the data however you'd like. Want to know who has the most clay court points? Or whose ranking is propped up by a single Grand Slam result? A few clicks gets you there.

Beyond the table, there are four visualization options to explore: a Stacked Bar chart for comparing point distributions across players, a Sankey diagram to see how points flow by tournament level, a Bump Chart to track ranking movement over time (along with the biggest risers and fallers of the past year), and a Heatmap to spot patterns across players and tournaments. Each offers a different lens on the same underlying data, sourced from [Jeff Sackmann's tennis datasets](https://github.com/JeffSackmann) and updated daily.

### What's Next?

This is just the start. I'm excited to keep building and open to feedback on what would make these sites more useful. If you have thoughts, feel free to reach out.
