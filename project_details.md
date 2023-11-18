Hey there, I did this project as my last Assignment as a Google data analysis student on Coursera.

About the project:> In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geo tracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

The approach I am planning to do this project by going through the six phases of data analysis, Such as Ask, Prepare, Process, Analyze, Share, Act.

ASK ---------
The questions that need to be answered are: · How do annual members and casual riders use Cyclistic bikes differently? · Why would casual riders buy Cyclistic annual memberships? · How can Cyclistic use digital media to influence casual riders to become members?

PREPARE-------- The dataset follows the ROCCC Analysis as described below: Reliable - yes, not biased Original - yes, can locate the original public data Comprehensive - yes, not missing important information Current - yes, updated monthly Cited - yes I will be using the public dataset located HERE. The data has been made available by Motivate International Inc. under this license

PROCESS--------- I have downloaded 12 months (year 2022) data from the company website and saved to project folder after unzipping. Once the 12 months data is stored in my computer then I loaded the csv files to R studio where I decided to do initial cleaning.

Importing Data into RStudio from Download Folder.

USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202210-divvy-tripdata.csv") month2 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202211-divvy-tripdata.csv") month3 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202212-divvy-tripdata.csv") month4 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202301-divvy-tripdata.csv") month5 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202302-divvy-tripdata.csv") month6 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202303-divvy-tripdata.csv") month7 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202304-divvy-tripdata.csv") month8 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202305-divvy-tripdata.csv") month9 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202306-divvy-tripdata.csv") month10 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202307-divvy-tripdata.csv") month11 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202308-divvy-tripdata.csv") month12 <-read.csv("C:\USER\Downloads\Projects\Divvy\12MOnthsDataunzip\202309-divvy-tripdata.csv") Instead of cleaning individual month Data I decided to Join all the months in to a single Data Frame then proceed to cleaning, OneYearData <- Rbind(month1, month2, month3, month4, month5, month6, month7, month8, month9, month10, month11, month12) Now the 12 months of data frames are combined to one single file called OneYearData. I load packages called “skimr”,”janitor”,”lubridate” and “dplyr” to check the summary and basic data manipulation.

install.packages("janitor") library("janitor") install.packages("skimr") library("skimr") install.packages("dplyr") library("dplyr") install.packages("lubridate") library("lubridate") To get the comprehensive summary of the data set. skim_without_charts(OneYearData) or glimpse(OneYearData) summary(OneYearData)

Output of "summary(OneYearData)"

Now to delete all NA values OneYearNoNA <- na.omit(OneYearData) to check number of rows and columns dim(OneYearNoNA) 5661859 13 OneYearData <- OneYearNoNA In the summary output its clear that the data types in “started_at” and “ended_at” columns are characters so for the better analysis purpose I am changing it into Date data type by using following code. To know how casual and members use bikes differently I need a column says how long each user uses the bikes. To get ride time subtract “start_time” from “end_time”.

OneYearData$ride_time_min <- difftime(OneYearData$ended_at,OneYearData$started_at, units = c("mins")) Check the data type of new column and it is as difftime class Change it to numeric value. OneYearData$ride_time_min <- as.numeric(OneYearData$ride_time_min) Create a new column called “day_of_week” to know which day of the week a rider use the bikes. First get the start date from column “started_at” OneYearData$start_date <- lubridate::date(OneYearData$started_at) dim(OneYearData) OneYearData$day_of_week <- wday(OneYearData$start_date,label = TRUE,abbr = FALSE) Now save the finished data frame as a new csv file. write.csv(OneYearData, "OneYearDivvy2022.csv",row.names = FALSE)

ANALYSIS and 5 SHARE------------
I am using Tableau for the analysis, Once loaded the csv file I performed following analysis. How the casual and member riders used bikes in 12 months

How the casual and member riders used bikes in 12 months From the pie diagram its clear that casual riders using bikes more time compared to annual members.

Now lets see how casual and members use bikes during a week.

The above graph shows casual riders are using bikes more in weekend days than members. Also, in weekdays casual riders using comparatively same as members but in a slightly less time than members.

Now lets see what type of bikes they use for a better understanding.

Members are using nearly zero docked bikes when compared to casual riders.

Lets see which are the top 5 cities.

How the users used bikes during the year?

The above graph shows 12 months usage data and it clear that the ride time is decreasing during winter months due to the fact that users prefer other mode of transportation during winter. Also, above graph shows during the months June, July and august the ride time of casual users are much higher when comparing with annual members so that buying annual membership is profitable for the casual customers as well as the company. Due to the less usage of bikes in winter season the company earns less, this can be managed by converting casual riders to annual members.

ACT -----------Recommendations----------
Casual riders use more time than annual members during the weekend days, on week days both casual and members uses bikes in a same pattern but annual members usage time is slightly higher. During the winter season both casual and annual members use bike less often so that converting casual users to annual members can be profitable for the company as well as for the casual users because Casual users tend to use bikes more than annual members during second and third quarter. By focusing existing casual users and giving them suitable offers may trigger them to purchase annual memberships. When giving offers to existing casual users on social media try to add some reports for their previous riding time to let them know that buying annual memberships are actually beneficial for them as well. Use location charts in the analysis to target people on social media where bike usage is comparatively lesser.
