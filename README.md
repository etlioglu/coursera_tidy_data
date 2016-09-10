# coursera_tidy_data
## Getting and Cleaning Data

Coursera Getting and Cleaning Data course requires tidying a publised data set:
Human Activity Recognition Using Smartphones Dataset Version 1.0

Information on the original data set can be found below:
Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Università degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
www.smartlab.ws


The "tidy" dataset includes the following files:
- "README.txt" : this file
- "tidy_data.txt" : cleaned and processed data set
- "run_analysis.R" : the R script used to produce the tidy data set
- codebook.txt : list of variables

Analysis overview:
- the test and the training data sets are read as data frames and proper column names are set
- columns providing "mean" and " "standard deviation" are extracted
- two columns, "subject" and "activity" are added to each data frame
- the two data frames are merged into a single data frame
- activity column is changed from codes to explicit activity names
- the data frame is grouped by "subject" and "activity" columns
- group mean values of each of the features (columns) are calculated

Deatiled analysis information is provided in the "run_analysis.R" code file.
