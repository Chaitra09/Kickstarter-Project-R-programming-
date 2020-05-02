# Kickstarter-Project-R-programming-
Kickstarter is the world's largest crowdfunding platform for creative projects

library(MASS)

library(caret)

library(dplyr)

Data1 <- read.csv("C:/Statistics/Final Dataset/kiwc.csv",header=TRUE)

head(Data1)
                                                      name main_category        deadline goal        launched
1                  Acting Out Yoga Presents: Anna in Paris    Publishing  7/2/2012 23:08 1500  6/2/2012 23:08
2                                  Auto Icon Screen Prints        Design  3/18/2015 1:00 1500 2/12/2015 19:20
3 Peter Squires' New 7" Record - Recorded by Steve Albini!         Music   2/1/2016 3:00  500  1/5/2016 20:40
4                                   Much Ado About Nothing       Theater 4/30/2012 22:00 6000 3/29/2012 15:08
5                                                    Bacon          Food  9/9/2014 21:18   23 7/11/2014 21:18
6                                          MARLEY WAS DEAD    Publishing  8/1/2013 19:00 4000  7/1/2013 19:00
       state backers .data_Film...Video .data_Music .data_Food .data_Crafts .data_Games .data_Design .data_Comics
1     failed       0                  0           0          0            0           0            0            0
2 successful     971                  0           0          0            0           0            1            0
3 successful      31                  0           1          0            0           0            0            0
4     failed       9                  0           0          0            0           0            0            0
5     failed       0                  0           0          1            0           0            0            0
6 successful      99                  0           0          0            0           0            0            0
  .data_Publishing .data_Fashion .data_Theater .data_Art .data_Photography .data_Technology .data_Dance
1                1             0             0         0                 0                0           0
2                0             0             0         0                 0                0           0
3                0             0             0         0                 0                0           0
4                0             0             1         0                 0                0           0
5                0             0             0         0                 0                0           0
6                1             0             0         0                 0                0           0
  .data_Journalism Season Prj_Name_Length Duration Launched_Year Deadline_Year
1                0 Summer              39       30          2012          2012
2                0 Winter              23       34          2015          2015
3                0 Winter              56       27          2016          2016
4                0 Spring              22       32          2012          2012
5                0 Summer               5       60          2014          2014
6                0 Summer              15       31          2013          2013

num_columns <- c('Prj_Name_Length')
Data1[num_columns] <- sapply(Data1[num_columns], as.numeric)
