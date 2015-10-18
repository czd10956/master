#Reproducible Research Assessment 1
===================================

##Read Data

```r
data=read.csv("activity.csv")
datanew=data
a=factor(data$date)
```
##Total steps per day

```r
sum=tapply(data$steps,a,sum)
hist(sum)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

```r
mean(sum,na.rm=TRUE)
```

```
## [1] 10766.19
```

```r
median(sum,na.rm=TRUE)
```

```
## [1] 10765
```
##Average Daily Pattern

```r
average=array(sum/12/24)
plot(unique(a),average,type="l")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 

```r
a[which.max(average)]
```

```
## [1] 2012-10-01
## 61 Levels: 2012-10-01 2012-10-02 2012-10-03 2012-10-04 ... 2012-11-30
```
##NA issue

```r
sum(is.na(data$steps)==TRUE)
```

```
## [1] 2304
```

```r
for (i in 1:nrow(data)){
    if (is.na(data[i,1])){
    datanew[i,1]=mean(sum,na.rm=TRUE)
    }
}
sumnew=tapply(data$steps,a,sum)
hist(sumnew)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

```r
mean(sum,na.rm=TRUE)
```

```
## [1] 10766.19
```

```r
median(sum,na.rm=TRUE)
```

```
## [1] 10765
```
##weekday and weekend

```r
for (i in 1:nrow(data)){
    if (weekdays(as.Date(datanew[i,2])) %in% c("Saturday","Sunday")){
    datanew[i,4]="weekend"
    }
    else{
        datanew[i,4]="weekday"
    }
}
```
