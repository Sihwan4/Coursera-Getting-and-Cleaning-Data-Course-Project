# Coursera-Getting-and-Cleaning-Data-Course-Project
* This codebook explains variables, codes in run_analysis.R
+ X_train.txt and X_test contains data of triaxial accelration, angular velocity, time, frequency domain variables
+  In features.txt, 1~561 reflects 561 variables
+ Subjects  are 1 ~ 30
+ Activity labels 1~6 mean Walking ~ laying


### The next code download zip file

> t0<-"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"

> download.file(t0,"UCI_HAR_Dataset.zip")

* The next code unzip the file  and set work directory

> unzip("UCI_HAR_Dataset.zip")

> setwd("./UCI HAR Dataset")


# In the beginning, we read the text files
### Read activity labels
>activity_labels <- read.table("activity_labels.txt",sep=" ",stringsAsFactors = F)

### Read features
>ftrs <- read.table("features.txt",sep=" ", stringsAsFactors = F)

>ftrs <- as.character(ftrs[,2])

### Read test sets 'X_test' and make column names using 'ftrs'

>X_test <- read.table("./test/X_test.txt",stringsAsFactors = F)

>colnames(X_test) <- ftrs

### Get y_test to get activity labels

>y_test<- read.table("./test/y_test.txt",stringsAsFactors = F)

>colnames(y_test) <- "activity"

### Read subjects of test

>st<-read.table("./test/subject_test.txt",stringsAsFactors = F)

### Read each text files in the train sets, as done in the test sets

>X_tr <- read.table("./train/X_train.txt",stringsAsFactors = F)

>colnames(X_tr) <- ftrs

>y_tr<- read.table("./train/y_train.txt",stringsAsFactors = F)

>colnames(y_tr) <- "activity"

>str<-read.table("./train/subject_train.txt",stringsAsFactors = F)


# Step 1. Merge the test/train files,
 
 * and then combine "test_total1" and "train_total1" to "total", using function "rbind"
 
>test_total1 <- cbind(X_test,subject = st[,1],activity = y_test[,1])

>train_total1 <- cbind(X_tr,subject = str[,1],activity = y_tr[,1])

>total <- rbind(test_total1, train_total1)

# Step 2. Select "mean" and "std"
 *  and save it to 'selected_features',
    +  so ftrs0 reflects selected features,
    + and columns in total will be selected using 'subject', 'activity', and ftrs0
  
>selected_features<- grep("mean|std",ftrs)

>ftrs0 <- ftrs[selected_features]

>total<-total[,c("subject","activity",ftrs0)]

# Step 3. Change activity label

>total$activity <- activity_labels[total$activity,2]

# Step 4. Adjust variable names.

>ftrs0<-gsub("-","_",ftrs0)

>ftrs0<-gsub("^f","Frequency_",ftrs0)

>ftrs0<-gsub("^t","Time_",ftrs0)

>ftrs0<-gsub("meanFreq","Mean_frequency",ftrs0)

>ftrs0 <- gsub("mean", "Mean_value", ftrs0)

>ftrs0 <- gsub("std", "Standard_deviation", ftrs0)

>ftrs0<-gsub('Acc',"_Acceleration",ftrs0)

>ftrs0<-gsub('GyroJerk',"_Angular_Acceleration",ftrs0)

>ftrs0<-gsub("Jerk","_Jerk",ftrs0)

>ftrs0<-gsub('Gyro',"_Angular_Speed",ftrs0)

>ftrs0<-gsub('Mag',"_Magnitude",ftrs0)

>ftrs0<-gsub('\\()',"",ftrs0)

>colnames(total) <- c("subject","activity",ftrs0)

# Step 5. get means per subject per activity
* Load dplyr, to use function "group_by" and "summrise_all"
* Write tidy data


>library(dplyr)

>tidy2 <- group_by(total,subject,activity)

>tidy2 <- summarise_all(tidy2,funs(mean))

>write.table(tidy2,"Tidy.txt", row.names=F)


# As a result
* You get "Tidy.txt" file in "UCI HRA Dataset" directory
