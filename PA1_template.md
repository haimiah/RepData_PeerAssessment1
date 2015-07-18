# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
Unzip the file, if not already done so, then read it in.

```r
if (!(file.exists("activity.csv"))) { 
    unzip("activity.zip")
    }
activityData <- read.csv("activity.csv")
```

Make sure dates are interpreted as dates

```r
activityData$date <- as.Date(activityData$date, "%Y-%m-%d")
```

## What is mean total number of steps taken per day?
Calculate the total number of steps per day (note NAs are ignored by default in the aggregate function)

```r
stepsPerDay <- aggregate(steps ~ date, data=activityData, FUN=sum)
```

Histogram of total steps per day

```r
hist(stepsPerDay$steps, 
     main="Distribution of Total Steps per Day", 
     xlab = "Total steps per day", 
     col = "red", 
     breaks=10, 
     xlim = c(0,max(stepsPerDay$steps)))
```

![](PA1_template_files/figure-html/HistStepsPerDay-1.png) 

Now, calculate the mean and median number of steps per day.

```r
meanStepsPerDay <- as.character(round(mean(stepsPerDay$steps),2))
medianStepsPerDay <- median(stepsPerDay$steps)
```
The mean steps per day is **10766.19** and the median is **10765**

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
