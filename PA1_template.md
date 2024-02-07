---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---




## Loading and preprocessing the data


```r
library(tidyverse)
df_data <- read_csv(file = "activity/activity.csv")
```


## What is mean total number of steps taken per day?


```r
# For this part of the assignment, you can ignore the missing values in the dataset.
# 1. Make a histogram of the total number of steps taken each day
# 2. Calculate and report the mean and median total number of steps taken per day

df_total_steps_per_day <- df_data %>% 
  group_by(date) %>% 
  summarise(total_steps_per_day = sum(steps, na.rm = TRUE))

hist(df_total_steps_per_day$total_steps_per_day, main = "Total number of steps taken each day", xlab = "Total number of steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

>The mean total number of steps taken per day is : **9354**  

>The median total number of steps taken per day is : **10395**


## What is the average daily activity pattern?


```r
# 1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis)
# and the average number of steps taken, averaged across all days (y-axis)
# 2. Which 5-minute interval, on average across all the days in the dataset,
# contains the maximum number of steps?

df_average_steps_per_day_interval <-  df_data %>% 
  group_by(interval) %>%
  summarise(average_steps_per_day_interval = mean(steps, na.rm = TRUE))

# create the plot
plot(df_average_steps_per_day_interval$interval, df_average_steps_per_day_interval$average_steps_per_day_interval, 
     type = "l",  main = "Average across all the days", xlab = "Interval", ylab = "Average steps",
     col = "red", lwd =1)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
max_steps <- max(df_average_steps_per_day_interval$average_steps_per_day_interval)
  
interval_with_max <- df_average_steps_per_day_interval %>% 
  filter(average_steps_per_day_interval == max_steps) %>% 
  pull(interval)
```

The 5 minute interval with maximum number of steps is: **835**


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


