## Reproductible Research
by Roger D. Peng, PhD, Jeff Leek, PhD, Brian Caffo, PhD
Coursera June 2014 session 

### Assignement 1
https://github.com/coursera-jm/RepData_PeerAssessment1

## Introduction

We want first ensure, as per instructions, that all statement will be outputs. 

```r
# set global options
opts_chunk$set(echo=TRUE)
```

We also initalize some common variables:

```r
# cleanup
rm(list=ls())

# for reproductibility
set.seed(590607)

# some usefule variables
dt = Sys.time()
date <- format(dt,"%d-%b-%Y")
time <- format(dt,"%H:%M:%S")

Rversion <- version$version.string
```

This analysis has been performed using R software package for statistical analysis.
The version of R used was R version 3.1.0 (2014-04-10).

This socument has been generated on 12-Jun-2014 at 12:41:50.

## Analysis as per assignement

### 1. Loading and preprocessing the data

  - Show any code that is needed to load the data

We download the dataset from the internet and unzip it. Then, we used read.csv to read the file.


```r
# baseDir will be prefixing all data accesses
baseDir <- "."

# create data and figuressub-directory if necessary
dataDir <- file.path(baseDir, "data")
if(!file.exists(dataDir)) { dir.create(dataDir) }

figuresDir <- file.path(baseDir, "figures")
if(!file.exists(figuresDir)) { dir.create(figuresDir) }

zipFilePath <- file.path(dataDir, "activity.zip")
dateFilePath <- file.path(dataDir, "date_time_downloaded.txt")
# download original data if necessary (skip if exists already as it takes time and bandwith)
if(!file.exists(zipFilePath)) { 
  zipFileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
  download.file (zipFileUrl, zipFilePath, method="curl")
  DTDownloaded <- format(Sys.time(), "%Y-%b-%d %H:%M:%S")
  cat (DTDownloaded, file=dateFilePath)
} else {
  DTDownloaded <- scan(file=dateFilePath, what="character", sep="\n")
}

filePath <- file.path(dataDir, "activity.csv")
# unzip file if necessary
if(!file.exists(filePath)) { 
  unzip (zipFilePath, exdir=dataDir)
}

# read dataset and load data in R
dataset <- read.csv(filePath, header = TRUE) 

cat ("The dataset is located at", filePath, "and was downloaded on downloaded on", DTDownloaded)
```

```
## The dataset is located at ./data/activity.csv and was downloaded on downloaded on 2014-Jun-12 12:06:46
```

We verify the dataset structure:

```r
str(dataset)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

The variables included in this dataset are:

    - steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)
    - date: The date on which the measurement was taken in YYYY-MM-DD format
    - interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of ``17568`` observations in this dataset for 17,568 expected from the instructions.

  - Process/transform the data (if necessary) into a format suitable for your analysis

```r
# let's get dates instead of character strings
```

### 2. What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

  - Make a histogram of the total number of steps taken each day

```r
p <- pdf(file.path(figuresDir, "histogramSteps.pdf"))
hist(dataset$steps)
dev.off()
```

```
## pdf 
##   2
```

  - Calculate and report the mean and median total number of steps taken per day

```r
mn <- mean(dataset$steps, na.rm=TRUE)
md <- median(dataset$steps, na.rm=TRUE)
```
The mean number of steps is ``37.3826`` and the median is ``0``.

As we can see, most days are 
### What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
# mode, e.g. http://stackoverflow.com/questions/2547402/standard-library-function-in-r-for-finding-the-mode
Mode <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}
```

### Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)


2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.


3. Create a new dataset that is equal to the original dataset but with the missing data filled in.


4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


3. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


### Are there differences in activity patterns between weekdays and weekends?

For this part the "weekdays()" function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels -- "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.


2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis).



## References

1. R Core Team. R: A language and environment for statistical computing. URL: http://www.R-project.org. R Foundation for Statistical Computing, 2013.

2. R Markdown Page. URL: http://www.rstudio.com/ide/docs/authoring/using_markdown. 


