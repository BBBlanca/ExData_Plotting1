## Introduction

This assignment uses data from
the <a href="http://archive.ics.uci.edu/ml/">UC Irvine Machine
Learning Repository</a>, a popular repository for machine learning
datasets. In particular, we will be using the "Individual household
electric power consumption Data Set" which I have made available on
the course web site:


* <b>Dataset</b>: <a href="https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip">Electric power consumption</a> [20Mb]

* <b>Description</b>: Measurements of electric power consumption in
one household with a one-minute sampling rate over a period of almost
4 years. Different electrical quantities and some sub-metering values
are available.


The following descriptions of the 9 variables in the dataset are taken
from
the <a href="https://archive.ics.uci.edu/ml/datasets/Individual+household+electric+power+consumption">UCI
web site</a>:

<ol>
<li><b>Date</b>: Date in format dd/mm/yyyy </li>
<li><b>Time</b>: time in format hh:mm:ss </li>
<li><b>Global_active_power</b>: household global minute-averaged active power (in kilowatt) </li>
<li><b>Global_reactive_power</b>: household global minute-averaged reactive power (in kilowatt) </li>
<li><b>Voltage</b>: minute-averaged voltage (in volt) </li>
<li><b>Global_intensity</b>: household global minute-averaged current intensity (in ampere) </li>
<li><b>Sub_metering_1</b>: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered). </li>
<li><b>Sub_metering_2</b>: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light. </li>
<li><b>Sub_metering_3</b>: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.</li>
</ol>

## Loading the data





When loading the dataset into R, please consider the following:

* The dataset has 2,075,259 rows and 9 columns. First
calculate a rough estimate of how much memory the dataset will require
in memory before reading into R. Make sure your computer has enough
memory (most modern computers should be fine).

* We will only be using data from the dates 2007-02-01 and
2007-02-02. One alternative is to read the data from just those dates
rather than reading in the entire dataset and subsetting to those
dates.

* You may find it useful to convert the Date and Time variables to
Date/Time classes in R using the `strptime()` and `as.Date()`
functions.

* Note that in this dataset missing values are coded as `?`.


## Making Plots

Our overall goal here is simply to examine how household energy usage
varies over a 2-day period in February, 2007. Your task is to
reconstruct the following plots below, all of which were constructed
using the base plotting system.

First you will need to fork and clone the following GitHub repository:
[https://github.com/rdpeng/ExData_Plotting1](https://github.com/rdpeng/ExData_Plotting1)


For each plot you should

* Construct the plot and save it to a PNG file with a width of 480
pixels and a height of 480 pixels.

* Name each of the plot files as `plot1.png`, `plot2.png`, etc.

* Create a separate R code file (`plot1.R`, `plot2.R`, etc.) that
constructs the corresponding plot, i.e. code in `plot1.R` constructs
the `plot1.png` plot. Your code file **should include code for reading
the data** so that the plot can be fully reproduced. You should also
include the code that creates the PNG file.

* Add the PNG file and R code file to your git repository

When you are finished with the assignment, push your git repository to
GitHub so that the GitHub version of your repository is up to
date. There should be four PNG files and four R code files.


The four plots that you will need to construct are shown below. 


### Plot 1


![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 


### Plot 2

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


### Plot 3

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


### Plot 4

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png)

Plot 1 Code:
rr<-read.table("household_power_consumption.txt", header = TRUE, sep = ";")
library(lubridate)
tt<- dmy(rr$Date)
yy<- cbind(rr, tt)
library(dplyr)
uu<- filter(yy, tt %in% c(as.Date("2007-02-01"), as.Date("2007-02-02")))
par("mfrow"= c(1,1))
hist(as.numeric(uu$Global_active_power), xlab = "Global Active Power (kilowatts)", ylab = "Frequency", main = "Global Active Power", col = "red")
dev.copy(png, file = "plot1.png")
dev.off()
![plot1](https://user-images.githubusercontent.com/83883191/119416213-2a573380-bcc1-11eb-9748-11c6e1625af0.png)

Plot 2 Code:
rr<-read.table("household_power_consumption.txt", header = TRUE, sep = ";")
library(lubridate)
tt<- dmy(rr$Date)
yy<- cbind(rr, tt)
library(dplyr)
uu<- filter(yy, tt %in% c(as.Date("2007-02-01"), as.Date("2007-02-02")))
par("mfrow"= c(1,1))
uu<- uu %>% mutate(DateTime = paste(Date, Time, sep = " "))
uu$DateTime <- as.POSIXct(uu$DateTime, format = "%d/%m/%Y %H:%M:%S")
plot(uu$DateTime, uu$Global_active_power, type = "l", ylab = "Global Active Power", xlab = "")
dev.copy(png, file = "plot2. png")
dev.off()
plot2. png![image](https://user-images.githubusercontent.com/83883191/119416364-71452900-bcc1-11eb-943c-25dd5b474f3f.png)

Plot 3 Code:
rr<-read.table("household_power_consumption.txt", header = TRUE, sep = ";")
library(lubridate)
tt<- dmy(rr$Date)
yy<- cbind(rr, tt)
library(dplyr)
uu<- filter(yy, tt %in% c(as.Date("2007-02-01"), as.Date("2007-02-02")))
par("mfrow"= c(1,1))
uu<- uu %>% mutate(DateTime = paste(Date, Time, sep = " "))
uu$DateTime <- as.POSIXct(uu$DateTime, format = "%d/%m/%Y %H:%M:%S")
plot(uu$DateTime, uu$Sub_metering_1, type = "l", col = "black", ylab = "Energy sub metering", xlab = "")
lines(uu$DateTime, uu$Sub_metering_2, type = "l", col = "red", ylab = "", xlab = "")
lines(uu$DateTime, uu$Sub_metering_3, type = "l", col = "blue", ylab = "", xlab = "")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = 1, lwd = 2.5, col = c("black", "red", "blue"), cex = 0.3)
dev.copy(png, file = "plot3. png")
dev.off()
plot3. png![image](https://user-images.githubusercontent.com/83883191/119416521-cb45ee80-bcc1-11eb-87f8-bc9a511f30b3.png)

Plot 4 Code:
par("mfrow" = c(2,2))
par("mar" = c(5,5,2,2))
plot(uu$DateTime, uu$Global_active_power, type = "l", ylab = "Global Active Power", xlab = "")
plot(uu$DateTime, as.numeric(uu$Voltage), type = "l", ylab = "Voltage", xlab = "Datetime")
plot(uu$DateTime, uu$Sub_metering_1, type = "l", col = "black", ylab = "Energy sub metering", xlab = "")
lines(uu$DateTime, uu$Sub_metering_2, type = "l", col = "red", ylab = "", xlab = "")
lines(uu$DateTime, uu$Sub_metering_3, type = "l", col = "blue", ylab = "", xlab = "")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = 1, lwd = 2.5, col = c("black", "red", "blue"), cex = 0.1)
plot(uu$DateTime, as.numeric(uu$Global_reactive_power), type = "l", ylab = "Global_reactive_power", xlab = "Datetime")
dev.copy(png, file = "plot4. png")
dev.off()
plot4. png![image](https://user-images.githubusercontent.com/83883191/119416540-dbf66480-bcc1-11eb-9e58-08cc81e73f7e.png)
