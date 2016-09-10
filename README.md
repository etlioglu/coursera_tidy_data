# coursera_tidy_data
## Getting and Cleaning Data

## run_analysis.R

## reading the test and the train data respectively
dfTest <- read.table("test/X_test.txt")
dfTrain <- read.table("train/X_train.txt")

# dfTest and dfTrain have dimesions of 2947  561 and 7352  561 respectively.
# The 561 columns (variables, features) have inexplicit names
# The feature names are supplied in a separate file (features.txt)
dfFeat <- read.table("features.txt")
# setting the column names of the dfTest and dfTrain
colnames(dfTest) <- dfFeat$V2
colnames(dfTrain) <- dfFeat$V2

# extracting the columns of interest
# grep returns the indices
intFeat <- grep(".*-mean\\(\\).*|.*-std\\(\\).*", dfFeat$V2)
dfTest <- dfTest[intFeat]
dfTrain <- dfTrain[intFeat]

# adding a column with subject ids to each table
# subject ids are loaded
dfSubTest <- read.table("test/subject_test.txt")
dfSubTrain <- read.table("train/subject_train.txt")
# subject ids are added as the first columns
dfTest <- data.frame(subject = dfSubTest$V1, dfTest)
dfTrain <- data.frame(subject = dfSubTrain$V1, dfTrain)

# adding a column with activity labels to each table
# activity labels are loaded
dfActTest <- read.table("test/y_test.txt")
dfActTrain <- read.table("train/y_train.txt")
# adding activity labels as the second column
dfTest <- as.data.frame(append(dfTest, list(activity = dfActTest$V1), after = 1))
dfTrain <- as.data.frame(append(dfTrain, list(activity = dfActTrain$V1), after = 1))

# setting up explicit activity names for the activity column
dfMerged$activity[dfMerged$activity=="1"] <- "WALKING"
dfMerged$activity[dfMerged$activity=="2"] <- "WALKING_UPSTAIRS"
dfMerged$activity[dfMerged$activity=="3"] <- "WALKING_DOWNSTAIRS"
dfMerged$activity[dfMerged$activity=="4"] <- "SITTING"
dfMerged$activity[dfMerged$activity=="5"] <- "STANDING"
dfMerged$activity[dfMerged$activity=="6"] <- "LAYING"

# the dplyr package is used for grouping and summarising
library(dplyr)
# grouping based on the subject and activity columns
dfGrouped <- group_by(dfMerged, subject, activity)
# retrieving group averages
dfTidyData <- summarise_each(dfGrouped,funs(mean))
