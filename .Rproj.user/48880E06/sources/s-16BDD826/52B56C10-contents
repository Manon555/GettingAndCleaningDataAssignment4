install.packages("dplyr")
library(dplyr)

## Step 1: Download and extraction of zipped raw data files

fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,"dataset.zip",mode = "wb")
unzip("dataset.zip")

## Step 2: Reading 6 tables into R and combination of the six table into one single table (mydata object)
## For training data set: training data (X_train.txt), subject ID information (subject_train.txt), activity ID information (y_train.txt)
## For test data set: training data (X_test.txt), subject ID information (subject_test.txt), activity ID information (y_test.txt)

# read and explore the files of the training data set
x_train <- read.table("UCI HAR Dataset/train/X_train.txt")
str(x_train)
y_train <- read.table("UCI HAR Dataset/train/y_train.txt")
str(y_train)
activity <- y_train[,1]
s_train <- read.table("UCI HAR Dataset/train/subject_train.txt")
str(s_train)
subject <- s_train[,1]

# combine subject information, activity information and training data in one data set
train <- mutate(x_train, subject, activity, .before=V1)
names(train)
train[1:10, 1:5]

# read and explore the files of the test data set
x_test <- read.table("UCI HAR Dataset/test/X_test.txt")
str(x_test)
y_test <- read.table("UCI HAR Dataset/test/y_test.txt")
str(y_test)
activity <- y_test[,1]
s_test <- read.table("UCI HAR Dataset/test/subject_test.txt")
str(s_test)
subject= s_test[,1]

# combine subject information, activity information and test data in one data set
test <- mutate(x_test, subject, activity, .before=V1)
names(test)
test[1:10, 1:5]

# combine training and test data in one data set
mydata <- rbind(train, test)

## Step 3: Read variable names (features.txt) and label the data set with variable names

features <- read.table("UCI HAR Dataset/features.txt")
str(features)
colnames(mydata)[3:ncol(mydata)] <- features$V2

## Step 4: Extract only the measurements on the mean and standard deviation for each measurement

mean.pos <- grep("mean[^F]", names(mydata))
std.pos <- grep("std", names(mydata))
pos = sort(c(1,2,std.pos,mean.pos))
mydata = mydata[,pos]
colnames(mydata)

## Step 5: Read activity labels table (activity_labels.txt) and use descriptive activity names for the activities in the data set

labels <- read.table("UCI HAR Dataset/activity_labels.txt")
str(labels)
mydata$activity

for(i in labels[,1])
{
  mydata[which(mydata$activity==i),"activity"] <- labels[i,2]
}

## Step 6: Appropriately change the labels of the data set to descriptive variable names

colnames(mydata) <- gsub("[^a-zA-Z]","", colnames(mydata))
colnames(mydata) <- gsub("^t","time", colnames(mydata))
colnames(mydata) <- gsub("^f","freq", colnames(mydata))
colnames(mydata) <- gsub("Acc","Accel", colnames(mydata))
colnames(mydata) <- gsub("Mag","Magnit", colnames(mydata))

## Step 7: Group the mydata table by subject and activity. 
## Create a second independent data set (mydata2 object) and 
## summmarize with the average of each variable for each activity and each subject

mydata <- group_by(mydata,subject, activity)
mydata2 <- summarise_at(mydata,names(mydata)[3:ncol(mydata)],mean)
names(mydata2)[3:ncol(mydata2)] <- gsub("^","mean",names(mydata2)[3:ncol(mydata2)])

## Step 8: Export the table with the tidy data set as .txt file (mean.train.test.X.txt)

write.table(mydata2, "mean.train.test.X.txt", row.names=FALSE, sep=",") 

