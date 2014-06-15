## Reproductible Research
by Roger D. Peng, PhD, Jeff Leek, PhD, Brian Caffo, PhD

Coursera - June 2014 session 

#### Assignement 1 in https://github.com/coursera-jm/RepData_PeerAssessment1


### Introduction

  - Instructions are in the "doc" sub-directory" (instructions.pdf). 
  - This analysis is performed through PA1_template.Rmd, which is compiled to PA1_template.md which, in turn, generates an HTML output: PA1_template.html. As per assignement instructions, these files are located in the root directory of this GitHub repository (https://github.com/coursera-jm/RepData_PeerAssessment1).
  - Data are saved in the "data" sub-directory.
  - Figures are generated in the "figure" sub-directory.
  
### Data

The data for this assignment can be downloaded from the course web site: [Activity monitoring data] (https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip) [52K].

The variables included in this dataset are:

* **steps**: Number of steps taking in a 5-minute interval (missing values are coded as `NA`).
* **date**: The date on which the measurement was taken in YYYY-MM-DD format.
* **interval**: Identifier for the 5-minute interval in which measurement was taken.

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this
dataset.

### Analysis 

The following steps are documented in "PA1_template.Rmd":

* Loading and preprocessing the data.
* What is mean total number of steps taken per day?
* What is the average daily activity pattern?
* Imputing missing values.
* Are there differences in activity patterns between weekdays and weekends?