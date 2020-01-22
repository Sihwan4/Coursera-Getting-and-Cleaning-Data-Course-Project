# Coursera-Getting-and-Cleaning-Data-Course-Project
Coursera-Getting-and-Cleaning-Data-Course-Project

## You may access the original data and description here:
   "http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones"

# When you run the script 'run_analysis.R',
  in the beginning, you will download data
   "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
  as "UCI_HAR_Dataset.zip" file in the work directory,
  and then unzip the file,
  so "UCI HAR Dataset" directory will appear in your work directory.

## We will set "UCI HAR Dataset" as a new working directory


# This script continues to analyze data of the test sets and train sets,
 as next 5 steps:


## Step 1. Read text files 
       # "activity_labels.txt", "features.txt" files are used to label acitivty and identify variable names
       # The six files- "X_test.txt","y_test","subject_test" in "/test" directory 
                        and "X_train.txt","y_train",subject_train" in "/train directory",
          are merged to make a data frame "total"
       
## Step 2. Variables in the data frame "total", whose name contian  "Standard deviation" or "Mean" will be selected

## Step 3. Change activity label using data from "activity_labels.txt"

## Step 4. Adjust variable names with descriptive names, such as:
     # "t" in the beginning to "Time", "f" in the beginning to "Frequency"
     # "mean" to "Mean_value", "std" to "Standard_deviation",
     # "Acc" to "_Acceleration", "GyroJerk" to "_Angular_Acceleration", and so on.

## Step 5. Get means per (subject/activity), and write tidy data
    # Load library 'dplyr', and use function 'group_by()' and 'summrise_all()'

# As a result, 
    # "Tidy.TXT" contains variables whose name contain "Standard deviation" or "Mean"
    # The columns of "Tidy.TXT" are subject, activity, and mean of variables.
