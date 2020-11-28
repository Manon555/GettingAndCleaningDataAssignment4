Step 1: Download and extraction of zipped raw data files

Step 2: Reading 6 tables into R and combination of the six table into one single table (mydata object)
For training data set: training data (X_train.txt), subject ID information (subject_train.txt), activity ID information (y_train.txt)
For test data set: training data (X_test.txt), subject ID information (subject_test.txt), activity ID information (y_test.txt)

Step 3: Read variable names (features.txt) and label the data set with variable names

Step 4: Extract only the measurements on the mean and standard deviation for each measurement

Step 5: Read activity labels table (activity_labels.txt) and use descriptive activity names for the activities in the data set

Step 6: Appropriately change the labels of the data set to descriptive variable names


Step 7: Group the mydata table by subject and activity. Create a second independent data set (mydata2 object) and summmarize with the average of each variable for each activity and each subject


Step 8: Export the table with the tidy data set as txt file (mean.train.test.X.txt)


