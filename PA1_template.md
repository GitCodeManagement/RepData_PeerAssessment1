Reproducible Research : Peer Reviewed Assignment 1
==================================================

###Loading and preprocessing the data
1) Load the data


```r
activity <- fread(file="activity.csv",sep = ",",na.strings = "NA",stringsAsFactors = FALSE,header=TRUE)
```


2) In activity data frame, change 'date` column from character type to Date type

```r
activity$date <- as.Date(activity$date,format = "%Y-%m-%d")
```

###What is mean total number of steps taken per day?

1) Histogram of Total number of steps taken each day



```r
hist(totalSteps_day[!is.na(totalSteps_day$x),]$x, xlab="Total Steps taken per day", main="Histogram of Total Number of Steps taken per day", breaks=55)
abline(v=mean(totalSteps_day$x,na.rm = TRUE),col="green",lwd=2)
abline(v=median(totalSteps_day$x,na.rm = TRUE),col="blue",lwd=2)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)

2) Mean and Median of total number of steps taken

        Mean   : 10766
        Median : 10765

###What is the average daily activity pattern?

1) Time series plot 5 minute Interval Vs average number of steps taken averaged across all days



```r
with(avg_steps_interval,plot(Interval,AvgSteps,typ="l",xlab="Interval", ylab="Average number of steps", col="blue", main="Time Interval Vs Average number of steps taken, averaged for all days"))
peak_avg <- avg_steps_interval[which(avg_steps_interval$AvgSteps==max(avg_steps_interval$AvgSteps)),]$Interval
abline(v=peak_avg,lwd=2,col="green")
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)

2) The 5 min interval, on average across all the days in the dataset, contains maximum number of steps 

        Interval where average number of steps maximum  :  835
        Average Max number of steps taken               :  206.1698113

###Imputing missing values
1) Total number of missing values (NA's) in the dataset

        Total number of rows having missing values : 2304



2) Histogram of total number of steps taken

        Missing values are filled with median of average number of steps taken each day - 37)
        

```r
hist(total_steps_day$avgSteps,xlab="Total Number of Steps taken per day", main="Histogram of Total Number of Steps taken per day",breaks=61)
abline(v=mean(total_steps_day$avgSteps),col="green",lwd=2)
abline(v=median(total_steps_day$avgSteps),col="blue",lwd=2)
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png)

3) Mean and Median of total number of steps taken

        Mean   : 10751
        Median : 10656 

The Mean and Median values after imputing are slightly lower than previous computation of omitting the missing values. The impact to original dataset is low.

###Are there differences in activity patterns between weekdays and weekends?


1) Plot to show the difference in activity between Weekday and Weekend
        
        There seems to be higher level of activity during Weekend than Weekday
        

```r
library(ggplot2)
ggplot(imput_avg_interval,aes(Interval,avgSteps))+geom_line(aes(col=DayType))+facet_wrap(~DayType, ncol=1)+labs(x="Interval",y="Average Number of steps", title="Interval Vs Average Number of steps in an interval, averaged by weekend and weekday")+geom_smooth(method = "lm",aes(col=DayType),se=FALSE)
```

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15-1.png)






