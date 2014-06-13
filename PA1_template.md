# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
zip_fname <- "activity.zip"
raw_file <- unzip(zip_fname, list=TRUE)$Name
zz <- read.csv(unz(zip_fname, as.character(raw_file)))

date <- split(zz$steps,zz$date)
interval <- split(zz$steps,zz$interval)
```


## What is mean total number of steps taken per day?
### Histogram

```r
sum_date <- lapply(date, sum, na.rm =TRUE)
temp <- c()

for(i in 1:length(sum_date)){
        temp <- c(temp, sum_date[[i]])        
}

hist(temp, xlab = "Total Number of Steps Taken Per Day", main ="Histogram of The Total Number of Steps Taken Each Day", ylab ="Number of days")
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

### Mean:

```r
mean(temp, na.rm =T)
```

```
## [1] 9354
```
### Median:

```r
median(temp, na.rm =T)
```

```
## [1] 10395
```
## What is the average daily activity pattern?
### Plot:

```r
mean_interval <- lapply(interval, mean, na.rm =TRUE)
temp1 <- c()

for(i in 1:length(mean_interval)){
        temp1 <- c(temp1, mean_interval[[i]])        
}
unique_interval <- unique(zz$interval)
plot(unique_interval,mean_interval, type ="l")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 

### Max. No. of Steps:

```r
sum_interval <- lapply(interval, sum, na.rm =TRUE)
temp2 <- c()

for(i in 1:length(sum_interval)){
        temp2 <- c(temp2, sum_interval[[i]])        
}
index <- which(max(temp2) == temp2)
unique_interval[index]
```

```
## [1] 835
```



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
