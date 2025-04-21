---
editor_options: 
  markdown: 
    wrap: sentence
---

# Understanding Pitcher Performance after Pitch Clock Implementation

by Jack and Luke

## Summary

The purpose of our project was to analyze Major League Baseball pitcher performance before and after the implementation of the pitch clock. Among the rule changes that took effect in 2023, the addition of the pitch clock is arguably the most impactful, vastly increasing the pace of the game. Before, pitchers essentially had an unlimited time to pitch, now, pitchers are required to throw to the plate within 18 seconds when runners are on base and 15 seconds when the bases are empty. Failure to pitch in the allotted time results in an automatic ball. With seemingly more restrictions, it would be expected that pitchers have found it hard to adjust to the change and therefore aren't as successful. To test this theory, we observed and visualized key pitcher metrics such as strike percentage, innings pitched, and ERA per game before and after the rule change. We find that pitcher outcomes do not change substantially with the addition of the pitch clock, but observe that variability within performance outcomes tightens after the addition of the pitch clock. This suggests that performance metrics are becoming more uniform, with outcomes grouping more consistently towards the mean and median.                    


## Methods and Analysis

Data was obtained from MLB's Statcast. We limited our focus to starting pitcher data from 2021-2024 to ensure that observations were balanced for outcomes before and after the implementation of the pitch clock. We obtained data on 411 starting pitchers, with a minimum of 20 games played in to be included in the dataset. We obtained data pertaining to many different pitcher outcomes, but focused primarily on strike percentage, innings pitched, and ERA. Each observation represented a starting pitcher's outcomes in a given year.
  Data was cleaned when necessary to visualize key metrics and to distinguish between whether the pitch clock was implemented or not. Strike percentage was calculated by dividing strikes by the total amount of adjusted pitches. Adjusted pitches represented all pitches excluding automatic calls to better reflect outcomes. The variable "pitch_clock" was created to filter whether the outcomes occurred before or after the rule change.
  Our data was visualized by two boxplots and a density plot. Innings pitched per game was visualized as a density plot, which showed that the spread of average innings pitched per game was tightening a little under 6 innings with the inclusion of the pitch clock. For strike percentage, we observed that strike percentage decreased from 65.08% to 64.62% with the addition of the pitch clock. We also observe that variation decreases with the addition of the pitch clock. It's hard to say whether the decrease is due to random variation within the data or due to the addition of the pitch clock. For pitcher ERA per game, we observed an increase in ERA from 3.94 to 3.96. We again observe the spread tightening with the inclusion of the pitch clock. Again, this small difference could be due to random variation within the data and not necessarily due to the rule change. While the visualizations don't show significant differences in pitching outcomes before and after the pitch clock, the tightening spread of the data shows that performance is becoming more consistent and less variable. We attribute this effect to the more standardized game tempo that the pitch clock creates, requiring pitchers to work at a consistent pace regardless of the game situation. This is reflected in the insights from average innings pitched per game, with the pitch clock tightening the spread and becoming more uniform around 5.67 innings pitched per game. We believe that these findings help illustrate the nature of pitching performance and outcomes before and after the rule change. We acknowledge the limitations of our data, in that we only observe starting pitcher outcomes. This omits relief and closing pitchers, who may be more sensitive to changes given they don't pitch as long as starting pitchers. We also glean that over the course of 4 seasons, many pitchers may have been injured, called down or retired, not meeting the cutoff of 20 games, which would omit them from the dataset. We hope that future research will build upon these insights. Particularly, it would be interesting to see differences between young and older pitchers or relief pitchers and starting pitchers.    


## Handout

Our presentation can be found [here](DCS117%20Final.pdf).

## Memo

A link to the code and how we created our graphics in our memo can be found [here](memo/memo.html).

## Data

Major League Baseball.
"Statcast: Custom Leaderboard." Baseball Savant.
Accessed April 15, 2025.
<https://baseballsavant.mlb.com/leaderboard/custom?year=2025%2C2024%2C2023%2C2022%2C2021%2C2020%2C2019%2C2018%2C2017%2C2016%2C2015&type=pitcher&filter=&min=q&selections=pa%2Ck_percent%2Cbb_percent%2Cwoba%2Cxwoba%2Csweet_spot_percent%2Cbarrel_batted_rate%2Chard_hit_percent%2Cavg_best_speed%2Cavg_hyper_speed%2Cwhiff_percent%2Cswing_percent&chart=false&x=pa&y=pa&r=no&chartType=beeswarm&sort=xwoba&sortDir=asc>.

## References

Major League Baseball.
"Statcast: Custom Leaderboard."

Major League Baseball.
"Pitch Timer." MLB.com. Accessed April 15, 2025.
<https://www.mlb.com/glossary/rules/pitch-timer>.
