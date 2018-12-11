

# Peer Review: Getting and Cleaning Data project
This repository is a submission for Getting and Cleaning Data course project. 
It has the instructions on how to run an analysis on Human Activity recognition dataset.

## Dataset
[Human Activity Recognition Using Smartphones](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

## Files
1. `CodeBook.md` a code book that describes the variables, the data, and transformations

2. `run_analysis.R` performs the data preparation and then followed by the 5 steps required as described in the course project’s definition:
    - Merges the training and the test sets to create one data set.
    - Extracts only the measurements on the mean and standard deviation for each measurement.
    - Uses descriptive activity names to name the activities in the data set
    - Appropriately labels the data set with descriptive variable names.
    - From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
3. `FinalData.txt is` the exported final data. 

## NOTES
if you have a problem in downloading the file, just used `http` instead of `https`
```
> if (!file.exists(filename)){
+   fileURL <- "http://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
+   download.file(fileURL, filename, method="curl")
+ }  
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 59.6M  100 59.6M    0     0   323k      0  0:03:08  0:03:08 --:--:--  318k 
```
