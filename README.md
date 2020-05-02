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
Prj_Name_Length<-Data1$Prj_Name_Length

Prj_Name_Length

cut(Prj_Name_Length,10)

cut(Prj_Name_Length,10,labels=c("First","Second","Third","Fourth","Five","Six","Seven","eight","nine","ten"))
  [1] Fourth Second Seven  Second Six    First  Seven  Seven  Third  Seven  First  Seven  Six    First  Second First 
  [17] Third  Second Seven  Five   Third  Second Six    Six    Five   Third  Six    First  Seven  Five   Five   Five  
  [33] First  Third  Fourth Seven  Second Fourth Six    Third  First  Seven  Second Fourth Seven  Third  Five   Seven 
  [49] Seven  First  First  First  Five   Five   First  Six    Six    Five   Third  Six    Seven  Third  Third  First 
  [65] First  First  Second Third  Second Third  First  First  Five   Third  Fourth Five   Five   Five   Third  Six   
  [81] First  Six    Seven  Five   Six    First  First  Five   Fourth Fourth Six    Five   Fourth Seven  Seven  Second
  
  
Data1$bins<-cut(Prj_Name_Length,10,labels=c("First","Second","Third","Fourth","Five","Six","Seven","eight","nine","ten"))
Data1

                                                                                       name main_category
1                                                   Acting Out Yoga Presents: Anna in Paris    Publishing
2                                                                   Auto Icon Screen Prints        Design
3                                  Peter Squires' New 7" Record - Recorded by Steve Albini!         Music
4                                                                    Much Ado About Nothing       Theater
5                                                                                     Bacon          Food
6                                                                           MARLEY WAS DEAD    Publishing
7                                Hip-Hop Script - Rhyming Prose in Poetic Storytelling Form    Publishing
8                                They All Fall Down: Book and Music Inspired by True Events    Publishing
9                                                               Power outage survival stove        Design
10                              Po-Rum-Bo - A card matching game with an intersecting twist         Games
11                                                                         Go F#@D yourself        Crafts
12                             Launch Franklin Home Page: The Go To Place for Franklin News    Journalism
13                                       The First (Ever!) Buffalo Cherry Blossom Festival!           Art
14                                                                         Cookie Dunk Dunk         Games
15                                                                 RiverRock Music Festival         Music
16                                                                        Heroes Everywhere           Art
17                                                                High Voltage Image Making           Art
18                                                                     CMYK 4 Poster Series        Design
19                             Forensics Forever!- Committed to performing arts excellence!       Theater
20                                             Nuanced Concrete: Postcards from Apocalypses           Art
21                                                               Never Let the Right One Go    Publishing
22                                                                   Joseph & Maka's Studio         Dance
23                                       Sit Stay Ride: The Story of America's Sidecar Dogs  Film & Video
24                                  A song to End Slavery. For the FreeWorld 2015 Campaign.         Music
25                                         Home Grown Books: Fine Art for Beginning Readers    Publishing
26                                                               ParaNova (a neo-noir film)  Film & Video
27                                   New Album: BRICK AND MORTAR. New Book: HITLESS WONDER.         Music
28                                                                         A Hand of Talons       Theater
29                               Linknotize, Fund Us and Help Cure Internet Hole Addiction!         Games
30                                              CAT: A Thruster for Interplanetary CubeSats    Technology
31                                          These Grey Men: Album and Tour by John Dolmayan         Music
32                                           LANA - A Short Film Directed By Berman Fenelus  Film & Video
33                                                                              UnBorn Hero  Film & Video
34                                                              Destiny's Fate - Round Two!        Comics
35                                                  Learn Game Programming (codeschool.org)    Technology
              deadline         goal         launched      state backers .data_Film...Video .data_Music .data_Food
1       7/2/2012 23:08      1500.00   6/2/2012 23:08     failed       0                  0           0          0
2       3/18/2015 1:00      1500.00  2/12/2015 19:20 successful     971                  0           0          0
3        2/1/2016 3:00       500.00   1/5/2016 20:40 successful      31                  0           1          0
4      4/30/2012 22:00      6000.00  3/29/2012 15:08     failed       9                  0           0          0
5       9/9/2014 21:18        23.00  7/11/2014 21:18     failed       0                  0           0          1
6       8/1/2013 19:00      4000.00   7/1/2013 19:00 successful      99                  0           0          0
7     10/30/2014 21:58      2000.00  9/30/2014 22:58     failed       1                  0           0          0
8       3/15/2013 4:59      6000.00    2/6/2013 6:07 successful     113                  0           0          0
9       6/7/2016 17:07     80000.00   4/8/2016 17:07     failed       5                  0           0          0
10      5/29/2012 3:00     10000.00   4/6/2012 15:05     failed      33                  0           0          0
11      11/7/2014 0:11       200.00   10/8/2014 0:11     failed       1                  0           0          0
12      8/31/2012 1:38     10000.00    8/1/2012 1:38     failed      13                  0           0          0
13    12/31/2013 21:15      5000.00 11/26/2013 19:56 successful     108                  0           0          0
14      4/5/2014 16:14     56000.00  2/19/2014 16:14     failed      65                  0           0          0
15      11/3/2014 6:00     25000.00  9/17/2014 20:21     failed       5                  0           1          0
16      6/6/2012 22:31      5000.00   5/7/2012 22:31     failed       5                  0           0          0
17     3/26/2014 16:33      5000.00  2/24/2014 17:33 successful     525                  0           0          0
18     7/19/2012 22:35       750.00   6/4/2012 22:35     failed      16                  0           0          0
19     5/25/2015 18:46    150000.00  4/20/2015 18:46     failed       1                  0           0          0
20      8/30/2013 3:10       307.00    8/1/2013 3:10     failed      12                  0           0          0
21      3/24/2012 5:00      1000.00   3/6/2012 19:24     failed      14                  0           0          0
  
# 10 Fold Cross Validation
> Train <- createDataPartition(Data1$state, p=0.7, list=FALSE)
> training <- Data1[ Train, ]
> testing <- Data1[ -Train, ]
> ctrl <- trainControl(method = "repeatedcv", number = 10, savePredictions = TRUE)
> mod_fit <- train(state ~ main_category+goal+Season+Launched_Year+Duration+Deadline_Year,data=Data1, method="glm", family="binomial",trControl = ctrl, tuneLength = 5)
There were 11 warnings (use warnings() to see them)
> pred = predict(mod_fit, newdata=testing)
> confusionMatrix(data=pred, testing$state)
Confusion Matrix and Statistics

            Reference
Prediction   failed successful
  failed       2752       1427
  successful    747       1073
                                          
               Accuracy : 0.6376          
                 95% CI : (0.6253, 0.6498)
    No Information Rate : 0.5833          
    P-Value [Acc > NIR] : < 2.2e-16       
                                          
                  Kappa : 0.2244          
 Mcnemar's Test P-Value : < 2.2e-16       
                                          
            Sensitivity : 0.7865          
            Specificity : 0.4292          
         Pos Pred Value : 0.6585          
         Neg Pred Value : 0.5896          
             Prevalence : 0.5833          
         Detection Rate : 0.4587          
   Detection Prevalence : 0.6966          
      Balanced Accuracy : 0.6079          
                                          
       'Positive' Class : failed   

  
