## CookBook

The `run_analysis.R` script performs the data preparation and then followed by the 5 steps required as described in the course project’s definition.

### 1.  Download the dataset
Dataset downloaded and extracted under the folder called UCI HAR Dataset

### 2.  Assign all data frames
- `features <- features.txt` : `561 rows, 2 columns` <br/>
The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ.
```R
             features <- read.table("UCI HAR Dataset/features.txt", col.names = c("n","functions"))
```
- `activities <- activity_labels.txt` : `6 rows, 2 columns` <br/><br/>
List of activities performed when the corresponding measurements were taken and its codes (labels)<br/>
```R
             activities <- read.table("UCI HAR Dataset/activity_labels.txt", col.names = c("code", "activity"))
```
- `subject_test <- test/subject_test.txt` : `2947 rows, 1 column` <br/><br/>
Contains test data of 9/30 volunteer test subjects being observed<br/>
```R
             subject_test <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject")
```
- `x_test <- test/X_test.txt` : `2947 rows, 561 columns` <br/><br/>
Contains recorded features test data<br/>
```R
              x_test <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = features$functions)
```
- `y_test <- test/y_test.txt` : `2947 rows, 1 columns` <br/><br/>
Contains test data of activities’code labels<br/>
```R
              y_test <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "code")
```
- `subject_train <- test/subject_train.txt` : `7352 rows, 1 column` <br/><br/>
Contains train data of 21/30 volunteer subjects being observed<br/>
```R
              subject_train <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject")
```          
- `x_train <- test/X_train.txt` : `7352 rows, 561 columns` <br/><br/>
Contains recorded features train data<br/>
```R
              x_train <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = features$functions)
```        
- `y_train <- test/y_train.txt` : `7352 rows, 1 columns` <br/><br/>
Contains train data of activities’code labels<br/>
```R
              y_train <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "code")
```

### 3. Merges the training and the test sets to create one data set
 - `X` `(10299 rows, 561 columns)` is created by merging `x_train` and `x_test` using `rbind()` function
 ```R
                                      X <- rbind(x_train, x_test)
 ```
- `Y` `(10299 rows, 1 column)` is created by merging `y_train` and `y_test` using `rbind()` function
```R
                                      Y <- rbind(y_train, y_test)
```                                     
- `Subject` `(10299 rows, 1 column)` is created by merging `subject_train` and `subject_test` using `rbind()` function
```R
                             Subject <- rbind(subject_train, subject_test)
```
- `Merged_Data` `(10299 rows, 563 column)` is created by merging `Subject`, `Y` and `X` using `cbind()` function
```R
                                  Merged_Data <- cbind(Subject, Y, X)
```
### 4. Extracts only the measurements on the mean and standard deviation for each measurement
`TidyData` (10299 rows, 88 columns) is created by subsetting `Merged_Data`, selecting only columns: `subject`, `code` and the measurements on the `mean` and `standard deviation (std)` for each measurement

```R
              TidyData <- Merged_Data %>% select(subject, code, contains("mean"), contains("std"))
```
### 5. Uses descriptive activity names to name the activities in the data set
Entire numbers in `code` column of the `TidyData` replaced with corresponding activity taken from second column of the  activities variable

### 6. Appropriately labels the data set with descriptive variable names
- `code` column in `TidyData` renamed into `activities`
- All `Acc` in column’s name replaced by `Accelerometer`
- All `Gyro` in column’s name replaced by `Gyroscope`
- All `BodyBod` in column’s name replaced by `Body`
- All `Mag` in column’s name replaced by `Magnitude`
- All start with character `f` in column’s name replaced by `Frequency`
- All start with character `t` in column’s name replaced by `Time`

### 7. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject
- `FinalData` (180 rows, 88 columns) is created by sumarizing `TidyData` taking the means of each variable for each activity and each subject, after groupped by subject and activity.
- Export `FinalData` into `FinalData.txt` file.
