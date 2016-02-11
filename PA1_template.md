# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
The raw data is loaded into the dataframe rawdata. No further preprocessing is needed.

```r
rawdata <- read.csv("activity.csv")
```

## What is mean total number of steps taken per day?
For this question the following calcuations are done:
- Aggregation of total number of steps per day
- Drawing of a equivalent histogramm
- Computing mean and median of total steps per day


```r
part2data <- aggregate(rawdata$steps, by = list(rawdata$date), FUN = sum, na.rm = TRUE)
names(part2data) <- c("date", "steps")
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 3.2.3
```

```r
# Histogramm
qplot(part2data$steps, binwidth = 1000) + 
	xlab("Total Number of Steps per Day") +
	ylab("Frequencies") +
	theme(axis.title = element_text(face = "bold", size = 12)) +
	geom_histogram(color = "black", fill = "green", binwidth = 1000)
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)

```r
# mean and median of the total number of steps taken per day
x <- summary(part2data$steps)
print(x[c("Mean", "Median")])
```

```
##   Mean Median 
##   9354  10400
```


## What is the average daily activity pattern?
Following steps are executed:   
- Calculation of the average steps per intervall across all days
- Detection of the interval(s) containing the maximal number of steps


```r
# Daily Activities
part3data <- aggregate(rawdata$steps, by = list(rawdata$interval), FUN = mean, na.rm = TRUE)
names(part3data) <- c("interval", "steps")
ggplot(part3data, aes(x = interval, y = steps)) + geom_line()
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)

```r
maxvalue <- max(part3data$steps)
maxinterval <- subset(part3data, steps == maxvalue)
print(maxinterval)
```

```
##     interval    steps
## 104      835 206.1698
```


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
