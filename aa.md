#Blabla TITLE

##Synopsis

##Data Processing

##



```r
library(data.table)
library(ggplot2)
# if(!file.exists('data.zip'))
# download.file('https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2'
# , 'data.bz2') setwd('git/repdata_peerassessment2')
rawData <- as.data.table(read.table(bzfile("data.bz2"), sep = ",", header = TRUE, 
    na.strings = ""))

```

> v1 <-  life[order(FATALITIES,decreasing=TRUE),][1:20,c("EVTYPE","FATALITIES"),with=FALSE]
> v2 <-  life[order(INJURIES,decreasing=TRUE),][1:20,c("EVTYPE","INJURIES"),with=FALSE]
You can also embed plots, for example:


```r
life <- rawData[, list(HEALTHDAMAGE = sum(FATALITIES, na.rm = TRUE) * 2 + sum(INJURIES, 
    na.rm = TRUE)), by = EVTYPE]
plotdata <- life[order(HEALTHDAMAGE, decreasing = TRUE)][1:10]
plotdata$EVTYPE <- as.factor(as.character(plotdata$EVTYPE))
plotdata$EVTYPE <- factor(plotdata$EVTYPE, plotdata$EVTYPE)
ggplot(plotdata, aes("", HEALTHDAMAGE, colour = plotdata$EVTYPE)) + geom_boxplot()
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-21.png) 

```r

nonlife <- rawData[, list(ECODAMAGE = sum(PROPDMG, na.rm = TRUE) + sum(CROPDMG, 
    na.rm = TRUE)), by = EVTYPE]
plotdata <- nonlife[order(ECODAMAGE, decreasing = TRUE)][1:10]
plotdata$EVTYPE <- as.factor(as.character(plotdata$EVTYPE))
plotdata$EVTYPE <- factor(plotdata$EVTYPE, plotdata$EVTYPE)
ggplot(plotdata, aes("", ECODAMAGE, colour = plotdata$EVTYPE)) + geom_boxplot()
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-22.png) 


