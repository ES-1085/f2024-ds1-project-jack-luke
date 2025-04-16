Project memo
================
Luke and Jack

This document should contain a detailed account of the data clean up for
your data and the design choices you are making for your plots. For
instance you will want to document choices you’ve made that were
intentional for your graphic, e.g. color you’ve chosen for the plot.
Think of this document as a code script someone can follow to reproduce
the data cleaning steps and graphics in your handout.

``` r
library(tidyverse)
library(broom)
```

## Data Clean Up Steps for Overall Data

### Step 1: Import and Clean Data

``` r
baseball <- read.csv("../data/pitching_data_2021-2024.csv")
baseball <- baseball %>%
  mutate(pitch_clock = ifelse(year >= 2023, "Yes", "No"))

# Step 1: Keep pitchers with all 4 years of data
baseball_1plot <- baseball %>%
  group_by(player_id) %>%
  filter(all(c(2022, 2023) %in% year)) %>%
  ungroup()

# Step 2: Calculate adjusted pitches and strike rate row by row
baseball_1plot <- baseball_1plot %>%
  mutate(
    adjusted_total_pitches = p_total_pitches - ifelse(is.na(p_automatic_ball), 0, p_automatic_ball),
    strike_percent = (p_total_strike / adjusted_total_pitches) * 100
  ) %>%
  filter(!is.na(pitch_clock), adjusted_total_pitches > 0)

baseball <- baseball %>%
  mutate(
    adjusted_total_pitches = p_total_pitches - ifelse(is.na(p_automatic_ball), 0, p_automatic_ball),
    strike_percent = (p_total_strike / adjusted_total_pitches) * 100
  ) %>%
  filter(!is.na(pitch_clock), adjusted_total_pitches > 0)

# Step 3: Collapse to one row per pitcher per pitch_clock (pre/post)
baseball_1plot <- baseball_1plot %>%
  group_by(player_id, pitch_clock) %>%
  summarise(
    avg_strike_percent = mean(strike_percent, na.rm = TRUE),
    total_pitches = sum(adjusted_total_pitches, na.rm = TRUE),
    .groups = "drop"
  )

baseball_3plot <- baseball %>%
  group_by(player_id, pitch_clock) %>%
  summarise(
    p_era = mean(p_era, na.rm = TRUE),
    total_pitches = sum(adjusted_total_pitches, na.rm = TRUE),
    .groups = "drop"
  )
```

### Step 2: \_\_\_\_\_\_\_\_

## Plots

### Plot 1: Boxplot of Strike Percentage

#### Data cleanup steps specific to plot 1

These data cleaning sections are optional and depend on if you have some
data cleaning steps specific to a particular plot

#### Final Plot 1

``` r
plot1_boxplot <- ggplot(baseball_1plot, aes(x = pitch_clock, y = avg_strike_percent, fill = pitch_clock)) +
  geom_boxplot(alpha = 0.7) +
  stat_summary(fun = mean, geom = "point", shape = 20, size = 3, color = "black") +  # black dot for mean
  stat_summary(
    fun = mean,
    geom = "text",
    aes(label = round(..y.., 2)),
    vjust = -1.2,
    color = "black",
    size = 4
  ) +  # mean label
  labs(
    title = "Strike % by Pitch Clock Era (Adjusted for Automatic Balls)",
    x = "Pitch Clock Implemented?",
    y = "Average Strike %"
  ) +
  theme(legend.position = "none")

ggsave("strike_percent_by_pitch_clock.png", plot = plot1_boxplot, width = 8, height = 6)
```

    ## Warning: The dot-dot notation (`..y..`) was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `after_stat(y)` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

### Plot 2: Innings pitched Density Plot

``` r
baseball$ip_game <- baseball$p_formatted_ip/baseball$p_game
densityplot <- ggplot(baseball, aes(x = ip_game, fill = factor(pitch_clock))) +
  geom_density(alpha = 0.5) +
  labs(
    title = "Innings Pitched (IP) per Game by Pitch Clock",
    x = "IP per Game",
    y = "Percent of Observations",
    fill = "Pitch Clock"
  ) +
  theme_minimal()

ggsave("Innings_Pitcher_per_game.png", plot = densityplot, width = 8, height = 6)
```

### Plot 3: Boxplot of ERA

``` r
ERAbox_plot <-
  ggplot(baseball_3plot, aes(x = pitch_clock, y = p_era, fill = pitch_clock)) +
  geom_boxplot(alpha = 0.7) +
  stat_summary(fun = mean, geom = "point", shape = 20, size = 3, color = "black") +  # black dot for mean
  stat_summary(
    fun = mean, 
    geom = "text", 
    aes(label = round(..y.., 2)), 
    vjust = -1.2, 
    color = "black", 
    size = 4
  ) +  # text label of mean
  labs(
    title = "Pitcher ERA Per Game By Pitch Clock", 
    x = "Pitchclock Implemented?",
    y = "ERA by Game"
  ) +
  theme(legend.position = "none")
ggsave("ERA_by_Pitchclock.png", plot = ERAbox_plot, width = 8, height = 6)
```

### Plot 4: \_\_\_\_\_\_\_\_\_\_\_
