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
Calculate the average steps per 5-minute interval (averaged accross all days)

```r
stepsPerInterval <- aggregate(steps ~ interval, data=activityData, FUN=mean)
```
Plot a time-series of this information

```r
plot(stepsPerInterval, 
     type="l", 
     main="Average Number of Steps per 5-minute Interval",
     ylab="Average Number of Steps", 
     xlab="5-minute Interval", 
     col="red")
polygon(x=stepsPerInterval$interval, y=stepsPerInterval$steps, col="red")
```

![](PA1_template_files/figure-html/AvgStepsPer5MinInterval-1.png) 

Calculate the 5-minute interval containing the maximum average number of steps

```r
intervalOfMaxMeanSteps <- subset(
    stepsPerInterval, 
    subset=steps==max(stepsPerInterval$steps), 
    select=interval)$interval
```
The 5-minute interval is **835**

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
