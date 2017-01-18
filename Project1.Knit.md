# Abstract

Fitbit, Nike, and Jawbone (2015) personal activitity monitoring devices enable capture for large amount of data about personal movement. This report makes use of sample data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

# Data

The data for this assignment can be downloaded from the course web site:

Dataset: Activity monitoring data [52K]. The variables included in this dataset are:

    steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)

    date: The date on which the measurement was taken in YYYY-MM-DD format

    interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset. See Appendix Data Extract in the annex for listings of the first and last ten rows of data.

# Loading and preprocessing the data

1. Load the data (i.e. read.csv())

        Read data file from the workding directory
        activity <- read.csv("activity.csv")

1. Process/transform the data (if necessary) into a format suitable for your analysis

        # Convert factor date as date data type, as.Date(dates, "%y/%m/%d")
        activity$date <- as.Date(activity$date, "%Y-%m-%d") 

# What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

1. Calculate the total number of steps taken per day

        # sum the total steps per day
        totalsteps <- aggregate(steps ~ date, activity, sum )
        # label the column for clarity
        names(totalsteps)[names(totalsteps)=="steps"] <- "totalsteps"
        # print the output to the console
        totalsteps

        ## date totalsteps
        ## 1  2012-10-02        126
        ## 2  2012-10-03      11352
        ## 3  2012-10-04      12116
        ## 4  2012-10-05      13294
        ## 5  2012-10-06      15420
        ## 6  2012-10-07      11015
        ## 7  2012-10-09      12811
        ## 8  2012-10-10       9900
        ## 9  2012-10-11      10304
        ## 10 2012-10-12      17382
        ## 11 2012-10-13      12426
        ## 12 2012-10-14      15098
        ## 13 2012-10-15      10139
        ## 14 2012-10-16      15084
        ## 15 2012-10-17      13452
        ## 16 2012-10-18      10056
        ## 17 2012-10-19      11829
        ## 18 2012-10-20      10395
        ## 19 2012-10-21       8821
        ## 20 2012-10-22      13460
        ## 21 2012-10-23       8918
        ## 22 2012-10-24       8355
        ## 23 2012-10-25       2492
        ## 24 2012-10-26       6778
        ## 25 2012-10-27      10119
        ## 26 2012-10-28      11458
        ## 27 2012-10-29       5018
        ## 28 2012-10-30       9819
        ## 29 2012-10-31      15414
        ## 30 2012-11-02      10600
        ## 31 2012-11-03      10571
        ## 32 2012-11-05      10439
        ## 33 2012-11-06       8334
        ## 34 2012-11-07      12883
        ## 35 2012-11-08       3219
        ## 36 2012-11-11      12608
        ## 37 2012-11-12      10765
        ## 38 2012-11-13       7336
        ## 39 2012-11-15         41
        ## 40 2012-11-16       5441
        ## 41 2012-11-17      14339
        ## 42 2012-11-18      15110
        ## 43 2012-11-19       8841
        ## 44 2012-11-20       4472
        ## 45 2012-11-21      12787
        ## 46 2012-11-22      20427
        ## 47 2012-11-23      21194
        ## 48 2012-11-24      14478
        ## 49 2012-11-25      11834
        ## 50 2012-11-26      11162
        ## 51 2012-11-27      13646
        ## 52 2012-11-28      10183
        ## 53 2012-11-29       7047

1. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

        # sum the total steps per day
        x <- aggregate(steps ~ date, activity, sum)
        # plot the histogram and label
        plot(x$steps ~ x$date, type="h", lwd = 7, ylab="Frequency (steps)", xlab="Activity Days")

1. Calculate and report the mean and median of the total number of steps taken per day

        # take the mean of the individual days
        tendency <- aggregate(steps ~ date, activity, mean, na.rm=TRUE)
        # take the median of the individual days
        medianTendency  <- aggregate(steps ~ date, activity, median, na.rm=TRUE)
        # combind in one table
        tendency <- cbind(tendency, medianTendency$steps)
        # rename the mean column lablefor clarity
        names(tendency)[names(tendency)=="steps"] <- "mean"
        # rename median column label for clarity
        names(tendency)[names(tendency)=="medianTendency$steps"] <- "median"
        # print the table to the console
        tendency 

        ##          date       mean median
        ## 1  2012-10-02  0.4375000      0
        ## 2  2012-10-03 39.4166667      0
        ## 3  2012-10-04 42.0694444      0
        ## 4  2012-10-05 46.1597222      0
        ## 5  2012-10-06 53.5416667      0
        ## 6  2012-10-07 38.2465278      0
        ## 7  2012-10-09 44.4826389      0
        ## 8  2012-10-10 34.3750000      0
        ## 9  2012-10-11 35.7777778      0
        ## 10 2012-10-12 60.3541667      0
        ## 11 2012-10-13 43.1458333      0
        ## 12 2012-10-14 52.4236111      0
        ## 13 2012-10-15 35.2048611      0
        ## 14 2012-10-16 52.3750000      0
        ## 15 2012-10-17 46.7083333      0
        ## 16 2012-10-18 34.9166667      0
        ## 17 2012-10-19 41.0729167      0
        ## 18 2012-10-20 36.0937500      0
        ## 19 2012-10-21 30.6284722      0
        ## 20 2012-10-22 46.7361111      0
        ## 21 2012-10-23 30.9652778      0
        ## 22 2012-10-24 29.0104167      0
        ## 23 2012-10-25  8.6527778      0
        ## 24 2012-10-26 23.5347222      0
        ## 25 2012-10-27 35.1354167      0
        ## 26 2012-10-28 39.7847222      0
        ## 27 2012-10-29 17.4236111      0
        ## 28 2012-10-30 34.0937500      0
        ## 29 2012-10-31 53.5208333      0
        ## 30 2012-11-02 36.8055556      0
        ## 31 2012-11-03 36.7048611      0
        ## 32 2012-11-05 36.2465278      0
        ## 33 2012-11-06 28.9375000      0
        ## 34 2012-11-07 44.7326389      0
        ## 35 2012-11-08 11.1770833      0
        ## 36 2012-11-11 43.7777778      0
        ## 37 2012-11-12 37.3784722      0
        ## 38 2012-11-13 25.4722222      0
        ## 39 2012-11-15  0.1423611      0
        ## 40 2012-11-16 18.8923611      0
        ## 41 2012-11-17 49.7881944      0
        ## 42 2012-11-18 52.4652778      0
        ## 43 2012-11-19 30.6979167      0
        ## 44 2012-11-20 15.5277778      0
        ## 45 2012-11-21 44.3993056      0
        ## 46 2012-11-22 70.9270833      0
        ## 47 2012-11-23 73.5902778      0
        ## 48 2012-11-24 50.2708333      0
        ## 49 2012-11-25 41.0902778      0
        ## 50 2012-11-26 38.7569444      0
        ## 51 2012-11-27 47.3819444      0
        ## 52 2012-11-28 35.3576389      0
        ## 53 2012-11-29 24.4687500      0

        # total daily mean and median averages respectively
        mean(activity$steps, na.rm=TRUE)

        ## [1] 37.3826

        median(activity$steps, na.rm=TRUE)

        ## [1] 0

# What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

        # calculate mean steps by interval 
        x <- aggregate(steps ~ interval, activity, mean, na.rm=TRUE)
        # plot the line chart and label
        plot(x, type="l", xlab="5-min Interval", ylab="Average Steps Taken")

1. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

        # cross check the graph's largest interval
        x$interval[x$steps==max(x$steps)]

        ## [1] 835

# Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

        # Sum the NA values 
        sum(is.na(activity$steps))

        ## [1] 2304

1. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

The preponderance of missing data are complete days, impute no activity into the data set for missing values. That is, impute a zero for NA values in the data set.

1. Create a new dataset that is equal to the original dataset but with the missing data filled in.

        # create the new table to impute values for NA
        imputed <- activity
        # substitute NA with zero
        imputed$steps[is.na(imputed$steps)] <- 0
        # cross check, no NA's
        sum(is.na(imputed$steps))

        ## [1] 0

        # cross check again, total entries add up to data set
        sum(!is.na(imputed$steps))

        ## [1] 17568

1. a. Make a histogram of the total number of steps taken each day Calculate and report the mean and median total number of steps taken per day.

        # calculate the frequencies by day
        imputedsum <- aggregate(steps ~ date, imputed, sum)
        # plot the historgram and label
        plot(imputedsum$steps ~ imputedsum$date, type="h", lwd = 7, ylab="Imputed Frequency (steps)", xlab="Imputed Activity Days")  

1. b. Calculate and report the mean and median total number of steps taken per day.

        # calculate the mean by day with imputed data set
        tendency <- aggregate(steps ~ date, imputed, mean)
        # calculate the median by day with the imputed data set
        medianTendency  <- aggregate(steps ~ date, imputed, median)
        # combine into on table
        tendency <- cbind(tendency, medianTendency$steps)
        # label the mean column for clarity
        names(tendency)[names(tendency)=="steps"] <- "mean"
        # label the median column for clarity
        names(tendency)[names(tendency)=="medianTendency$steps"] <- "median"
        # print out put to console
        tendency 

        ##          date       mean median
        ## 1  2012-10-01  0.0000000      0
        ## 2  2012-10-02  0.4375000      0
        ## 3  2012-10-03 39.4166667      0
        ## 4  2012-10-04 42.0694444      0
        ## 5  2012-10-05 46.1597222      0
        ## 6  2012-10-06 53.5416667      0
        ## 7  2012-10-07 38.2465278      0
        ## 8  2012-10-08  0.0000000      0
        ## 9  2012-10-09 44.4826389      0
        ## 10 2012-10-10 34.3750000      0
        ## 11 2012-10-11 35.7777778      0
        ## 12 2012-10-12 60.3541667      0
        ## 13 2012-10-13 43.1458333      0
        ## 14 2012-10-14 52.4236111      0
        ## 15 2012-10-15 35.2048611      0
        ## 16 2012-10-16 52.3750000      0
        ## 17 2012-10-17 46.7083333      0
        ## 18 2012-10-18 34.9166667      0
        ## 19 2012-10-19 41.0729167      0
        ## 20 2012-10-20 36.0937500      0
        ## 21 2012-10-21 30.6284722      0
        ## 22 2012-10-22 46.7361111      0
        ## 23 2012-10-23 30.9652778      0
        ## 24 2012-10-24 29.0104167      0
        ## 25 2012-10-25  8.6527778      0
        ## 26 2012-10-26 23.5347222      0
        ## 27 2012-10-27 35.1354167      0
        ## 28 2012-10-28 39.7847222      0
        ## 29 2012-10-29 17.4236111      0
        ## 30 2012-10-30 34.0937500      0
        ## 31 2012-10-31 53.5208333      0
        ## 32 2012-11-01  0.0000000      0
        ## 33 2012-11-02 36.8055556      0
        ## 34 2012-11-03 36.7048611      0
        ## 35 2012-11-04  0.0000000      0
        ## 36 2012-11-05 36.2465278      0
        ## 37 2012-11-06 28.9375000      0
        ## 38 2012-11-07 44.7326389      0
        ## 39 2012-11-08 11.1770833      0
        ## 40 2012-11-09  0.0000000      0
        ## 41 2012-11-10  0.0000000      0
        ## 42 2012-11-11 43.7777778      0
        ## 43 2012-11-12 37.3784722      0
        ## 44 2012-11-13 25.4722222      0
        ## 45 2012-11-14  0.0000000      0
        ## 46 2012-11-15  0.1423611      0
        ## 47 2012-11-16 18.8923611      0
        ## 48 2012-11-17 49.7881944      0
        ## 49 2012-11-18 52.4652778      0
        ## 50 2012-11-19 30.6979167      0
        ## 51 2012-11-20 15.5277778      0
        ## 52 2012-11-21 44.3993056      0
        ## 53 2012-11-22 70.9270833      0
        ## 54 2012-11-23 73.5902778      0
        ## 55 2012-11-24 50.2708333      0
        ## 56 2012-11-25 41.0902778      0
        ## 57 2012-11-26 38.7569444      0
        ## 58 2012-11-27 47.3819444      0
        ## 59 2012-11-28 35.3576389      0
        ## 60 2012-11-29 24.4687500      0
        ## 61 2012-11-30  0.0000000      0

        # total daily mean and median averages respectively

        mean(imputed$steps)

        ## [1] 32.47996

        median(imputed$steps)

        ## [1] 0

1. c. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

# Analysis

Yes, increasing the population biased the mean by skewing the mean towards zero from 37.3826 to 32.4797. The median remained robust throughout both calculations. The number of aggregrated day rows increased from 53 to 61, and the frequency of zeros increased with the introduction of zeros for NA's on those days. Without even introducing more zero values for the NA values, the number of zeros are approximately 75%; therefore, the median will remianed zero.

# Are there differences in activity patterns between weekdays and weekends?

For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

Yes. Activity starts earlier and reamains higher throughout the day then subsiding towards the end.

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

        #create a vector of weekdays
        weekdays1 <- c('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')
        #Use `%in%` and `weekdays` to create a logical vector
        #Convert to `factor` and specify the `levels/labels`
        imputed$partofweek <-  factor((weekdays(imputed$date) %in% weekdays1)+1L,
              levels=1:2, labels=c('weekend', 'weekday'))
        #activity$partofweek
         aggregate(steps ~ partofweek, imputed, sum, na.rm=TRUE)

        ##   partofweek  steps
        ## 1    weekend 173692
        ## 2    weekday 396916

1. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.

        # Make a two panel plot
        par(mfrow=c(2,1))
        # Gather the weekday data first
        weekday <- subset(imputed, partofweek=="weekday")
        # calculate the weekday mean fisrt
        wd <- aggregate(steps ~ interval, weekday, mean, na.rm=TRUE)
        # plot the average interval graph for weekdays
        plot(wd, type="l", xlab="Weekday 5-min Interval", ylab="Average Steps")

        # Gather the weekday data first
        weekend <- subset(imputed, partofweek=="weekend")
        # calculate the weekday mean fisrt
        we <- aggregate(steps ~ interval, weekend, mean, na.rm=TRUE)
        # plot the average interval graph for weekends
        plot(we, type="l", xlab="Weekend 5-min Interval", ylab="Average Steps")

# References

1. Fitbit. (2015). Retrieved May 14, 2015, from http://www.fitbit.com.
2. Nike. (2015). Retrieved May 14, 2015, from http://www.nike.com/us/en_us/c/nikeplus-fuel.
3. Jawbone. (2015). Retrieved May 14, 2015, from https://jawbone.com/up.

# Appendix Data Extract

Show the first 10 rows of data

        head(activity, 10)  

        ##    steps       date interval
        ## 1     NA 2012-10-01        0
        ## 2     NA 2012-10-01        5
        ## 3     NA 2012-10-01       10
        ## 4     NA 2012-10-01       15
        ## 5     NA 2012-10-01       20
        ## 6     NA 2012-10-01       25
        ## 7     NA 2012-10-01       30
        ## 8     NA 2012-10-01       35
        ## 9     NA 2012-10-01       40
        ## 10    NA 2012-10-01       45

Show the last 10 rows of data

        tail(activity, 10)  

        ##       steps       date interval
        ## 17559    NA 2012-11-30     2310
        ## 17560    NA 2012-11-30     2315
        ## 17561    NA 2012-11-30     2320
        ## 17562    NA 2012-11-30     2325
        ## 17563    NA 2012-11-30     2330
        ## 17564    NA 2012-11-30     2335
        ## 17565    NA 2012-11-30     2340
        ## 17566    NA 2012-11-30     2345
        ## 17567    NA 2012-11-30     2350
        ## 17568    NA 2012-11-30     2355
