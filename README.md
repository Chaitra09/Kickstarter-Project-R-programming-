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
       
# Logistic Regression with Binning      
> dim(Data1)
[1] 20000    28
> smp_size <- floor(0.70 * nrow(Data1))
> set.seed(123)
> train_ind <- sample(seq_len(nrow(Data1)), size = smp_size)
> train <- Data1[train_ind, ]
> test <- Data1[-train_ind, ]
> dim(train)
[1] 14000    28
> dim(test)
[1] 6000   28
> summary(Data1)
               name            main_category            deadline          goal                      launched            state      
 #NAME?          :    5   Film & Video:3711   6/2/2012 5:59 :    6   Min.   :        1   3/26/2013 20:46:    3   failed    :11664  
 Facade          :    2   Music       :3229   9/1/2010 5:59 :    6   1st Qu.:     2000   8/12/2013 22:10:    3   successful: 8336  
 Keys to the City:    2   Publishing  :2221   1/1/2012 8:59 :    4   Median :     5000   1/10/2013 20:46:    2                     
 Music Video     :    2   Art         :1635   11/1/2014 4:59:    4   Mean   :    38148   1/14/2015 3:01 :    2                     
 My First Film   :    2   Games       :1486   12/1/2014 8:59:    4   3rd Qu.:    15000   1/15/2013 16:01:    2                     
 Pangaea         :    2   Design      :1322   3/1/2012 3:00 :    4   Max.   :100000000   1/15/2015 1:13 :    2                     
 (Other)         :19985   (Other)     :6396   (Other)       :19972                       (Other)        :19986                     
    backers         .data_Film...Video  .data_Music       .data_Food      .data_Crafts     .data_Games      .data_Design   
 Min.   :     0.0   Min.   :0.0000     Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
 1st Qu.:     2.0   1st Qu.:0.0000     1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000  
 Median :    17.0   Median :0.0000     Median :0.0000   Median :0.0000   Median :0.0000   Median :0.0000   Median :0.0000  
 Mean   :   113.2   Mean   :0.1855     Mean   :0.1615   Mean   :0.0656   Mean   :0.0232   Mean   :0.0743   Mean   :0.0661  
 3rd Qu.:    65.0   3rd Qu.:0.0000     3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000  
 Max.   :105857.0   Max.   :1.0000     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
                                                                                                                           
  .data_Comics    .data_Publishing .data_Fashion    .data_Theater       .data_Art       .data_Photography .data_Technology
 Min.   :0.0000   Min.   :0.000    Min.   :0.0000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.0000  
 1st Qu.:0.0000   1st Qu.:0.000    1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.0000  
 Median :0.0000   Median :0.000    Median :0.0000   Median :0.00000   Median :0.00000   Median :0.00000   Median :0.0000  
 Mean   :0.0319   Mean   :0.111    Mean   :0.0518   Mean   :0.03195   Mean   :0.08175   Mean   :0.02845   Mean   :0.0627  
 3rd Qu.:0.0000   3rd Qu.:0.000    3rd Qu.:0.0000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.0000  
 Max.   :1.0000   Max.   :1.000    Max.   :1.0000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.0000  
                                                                                                                          
  .data_Dance      .data_Journalism     Season     Prj_Name_Length.Prj_Name_Length    Duration    Launched_Year  Deadline_Year 
 Min.   :0.00000   Min.   :0.00000   Fall  :4930   Min.   : 1.00000                Min.   : 1.0   Min.   :2009   Min.   :2009  
 1st Qu.:0.00000   1st Qu.:0.00000   Spring:5319   1st Qu.:16.00000                1st Qu.:30.0   1st Qu.:2012   1st Qu.:2012  
 Median :0.00000   Median :0.00000   Summer:5539   Median :29.00000                Median :30.0   Median :2014   Median :2014  
 Mean   :0.01265   Mean   :0.01155   Winter:4212   Mean   :30.87895                Mean   :34.5   Mean   :2013   Mean   :2014  
 3rd Qu.:0.00000   3rd Qu.:0.00000                 3rd Qu.:46.00000                3rd Qu.:38.0   3rd Qu.:2015   3rd Qu.:2015  
 Max.   :1.00000   Max.   :1.00000                 Max.   :85.00000                Max.   :92.0   Max.   :2016   Max.   :2016  
                                                                                                                               
      bins     
 Third  :3300  
 Five   :3066  
 Second :2961  
 First  :2728  
 Fourth :2552  
 Seven  :2397  
 (Other):2996  
> contrasts(Data1$state)
           successful
failed              0
successful          1
> glm.fits <- glm(state~main_category+backers+Season+goal+Launched_Year+Deadline_Year+Duration+bins,data=Data1,family=binomial,control=list(maxit=100),subset=unlist(train))
Warning message:
glm.fit: fitted probabilities numerically 0 or 1 occurred 
> summary(glm.fits)

Call:
glm(formula = state ~ main_category + backers + Season + goal + 
    Launched_Year + Deadline_Year + Duration + bins, family = binomial, 
    data = Data1, subset = unlist(train), control = list(maxit = 100))

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-8.4904  -0.2658  -0.0108   0.1565   8.4904  

Coefficients:
                            Estimate Std. Error  z value Pr(>|z|)    
(Intercept)                7.960e+01  1.445e+01    5.508 3.63e-08 ***
main_categoryComics       -3.833e-01  7.970e-02   -4.810 1.51e-06 ***
main_categoryCrafts       -1.439e-01  6.604e-02   -2.178  0.02937 *  
main_categoryDance         2.529e-01  9.487e-02    2.666  0.00767 ** 
main_categoryDesign       -6.821e-01  7.891e-02   -8.644  < 2e-16 ***
main_categoryFashion       5.502e-01  7.678e-02    7.166 7.74e-13 ***
main_categoryFilm & Video  1.274e+00  4.910e-02   25.937  < 2e-16 ***
main_categoryFood         -1.453e+00  6.062e-02  -23.972  < 2e-16 ***
main_categoryGames        -3.047e-01  6.748e-02   -4.515 6.33e-06 ***
main_categoryJournalism   -8.160e-01  1.204e-01   -6.778 1.22e-11 ***
main_categoryMusic         2.666e+00  4.630e-02   57.586  < 2e-16 ***
main_categoryPhotography   1.024e+00  7.429e-02   13.788  < 2e-16 ***
main_categoryPublishing   -7.609e-01  4.771e-02  -15.948  < 2e-16 ***
main_categoryTechnology   -5.366e+00  1.782e-01  -30.121  < 2e-16 ***
main_categoryTheater      -2.843e-01  6.013e-02   -4.729 2.26e-06 ***
backers                    7.040e-02  4.613e-04  152.620  < 2e-16 ***
SeasonSpring               1.402e+00  3.332e-02   42.068  < 2e-16 ***
SeasonSummer              -6.228e-04  3.290e-02   -0.019  0.98490    
SeasonWinter               6.015e-01  3.762e-02   15.990  < 2e-16 ***
goal                      -4.305e-04  2.807e-06 -153.389  < 2e-16 ***
Launched_Year              2.382e+00  4.863e-02   48.979  < 2e-16 ***
Deadline_Year             -2.422e+00  4.850e-02  -49.948  < 2e-16 ***
Duration                   6.999e-03  9.381e-04    7.460 8.63e-14 ***
binsSecond                -1.551e-02  4.206e-02   -0.369  0.71224    
binsThird                 -2.500e-01  4.270e-02   -5.854 4.79e-09 ***
binsFourth                -8.380e-01  4.501e-02  -18.618  < 2e-16 ***
binsFive                   7.183e-01  4.383e-02   16.390  < 2e-16 ***
binsSix                    1.047e+00  4.344e-02   24.103  < 2e-16 ***
binsSeven                  1.311e-01  4.247e-02    3.087  0.00203 ** 
binseight                  6.661e-01  1.688e-01    3.947 7.92e-05 ***
binsnine                   5.423e-01  3.105e-01    1.746  0.08075 .  
binsten                    2.379e+00  8.455e-02   28.138  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 260614  on 191983  degrees of freedom
Residual deviance:  70787  on 191952  degrees of freedom
  (2421 observations deleted due to missingness)
AIC: 70851

Number of Fisher Scoring iterations: 13
> coef(glm.fits)
            
 
> summary(glm.fits)$coef
                               Estimate   Std. Error       z value      Pr(>|z|)
(Intercept)               79.6006531050 1.445203e+01    5.50792285  3.630925e-08
main_categoryComics       -0.3833478110 7.970220e-02   -4.80975164  1.511179e-06
main_categoryCrafts       -0.1438623536 6.603809e-02   -2.17847525  2.937067e-02
main_categoryDance         0.2529380739 9.487178e-02    2.66610445  7.673585e-03
main_categoryDesign       -0.6820686226 7.890583e-02   -8.64408443  5.423844e-18
main_categoryFashion       0.5501676633 7.677769e-02    7.16572316  7.737700e-13
main_categoryFilm & Video  1.2736440940 4.910494e-02   25.93718700 2.536561e-148
main_categoryFood         -1.4531297568 6.061761e-02  -23.97207091 5.440122e-127
main_categoryGames        -0.3046666893 6.747843e-02   -4.51502319  6.330984e-06
main_categoryJournalism   -0.8160221606 1.203916e-01   -6.77806573  1.217954e-11
main_categoryMusic         2.6659303590 4.629516e-02   57.58550491  0.000000e+00
main_categoryPhotography   1.0243033306 7.429134e-02   13.78765530  3.024306e-43
main_categoryPublishing   -0.7609431543 4.771320e-02  -15.94827450  2.928777e-57
main_categoryTechnology   -5.3662383960 1.781552e-01  -30.12113964 2.562003e-199
main_categoryTheater      -0.2843481535 6.012935e-02   -4.72894107  2.256939e-06
backers                    0.0703985950 4.612657e-04  152.62049856  0.000000e+00
SeasonSpring               1.4017800139 3.332200e-02   42.06770302  0.000000e+00
SeasonSummer              -0.0006228112 3.290045e-02   -0.01893017  9.848968e-01
SeasonWinter               0.6015127893 3.761723e-02   15.99035474  1.491791e-57
goal                      -0.0004305015 2.806591e-06 -153.38945648  0.000000e+00
Launched_Year              2.3818195007 4.862940e-02   48.97900655  0.000000e+00
Deadline_Year             -2.4223387149 4.849753e-02  -49.94767551  0.000000e+00
Duration                   0.0069986697 9.381236e-04    7.46028566  8.633510e-14
binsSecond                -0.0155137355 4.205913e-02   -0.36885537  7.122355e-01
binsThird                 -0.2499527490 4.269534e-02   -5.85433356  4.789266e-09
binsFourth                -0.8379989383 4.501069e-02  -18.61777738  2.305879e-77
binsFive                   0.7183377862 4.382876e-02   16.38964392  2.267691e-60
binsSix                    1.0469354506 4.343637e-02   24.10273771 2.339831e-128
binsSeven                  0.1310786714 4.246802e-02    3.08652685  2.025097e-03
binseight                  0.6660733520 1.687611e-01    3.94684061  7.918924e-05
binsnine                   0.5422822391 3.105203e-01    1.74636621  8.074734e-02
binsten                    2.3789928948 8.454873e-02   28.13753564 3.404831e-174


> glm.probs <-predict(glm.fits,test,type='response')
> glm.pred <- glm.probs
> glm.pred[glm.probs>.5] <- "successful"
> glm.pred[glm.probs<=.5]<- "failed"
> table(glm.pred,test$state)
            
glm.pred     failed successful
  failed       3067        534
  successful    409       1990
  
  
KNN CODE- 
##DATA NORMALIZATION

> data_norm<- function(x) {((x-min(x))/(max(x)-min(x)))} #normalization
> norm_kick<-as.data.frame(lapply(final_kick[-2],data_norm))
> final_binddata<-cbind(final_kick[2],norm_kick)
> trainDF<-final_binddata[1:14000,] #70%
> testDF<- final_binddata[14001:20000,] #30%
> #KNN
> library(class)
> start.time<-Sys.time()

 #KNN LOOP

> TP=rep(0,80)
> FP=rep(0,80)
> TN=rep(0,80)
> FN=rep(0,80)
> for (i in 1:80){
+   prediction_2<-knn(trainDF[-1],testDF[-1],final_binddata[1:14000,1],k=i)
+   TP[i]=table(prediction_2,final_binddata[14001:20000,1])[1,1]
+   TN[i]=table(prediction_2,final_binddata[14001:20000,1])[2,2]
+   FP[i]=table(prediction_2,final_binddata[14001:20000,1])[1,2]
+   FN[i]=table(prediction_2,final_binddata[14001:20000,1])[1,2]
+ }

> stop.time<- Sys.time()
> total.knn.tuningtime<-print(stop.time-start.time)
Time difference of 6.772924 mins
> #metrics 
> accuracytest<-((TP+TN)/(TP+TN+FP+FN))
> sensitivity_test<-(TP/(TP+FN))
> specificity<-(TN/(TN+FP))
> #view metrics
> accuracytest

> #view metrics
> accuracytest
 [1] 0.5689282 0.5678275 0.5636246 0.5665695 0.5604781 0.5658716 0.5653414 0.5654250 0.5685407 0.5684044 0.5687510 0.5640138
[13] 0.5646322 0.5672881 0.5623544 0.5602748 0.5590649 0.5619462 0.5646216 0.5594645 0.5591799 0.5566579 0.5611801 0.5664596
[25] 0.5622677 0.5568899 0.5545024 0.5568826 0.5585764 0.5621845 0.5611247 0.5596330 0.5551504 0.5569697 0.5578437 0.5585914
[37] 0.5589883 0.5568699 0.5618643 0.5548173 0.5500831 0.5486205 0.5477841 0.5516669 0.5497587 0.5514639 0.5526038 0.5499246
[49] 0.5490580 0.5495414 0.5474518 0.5459024 0.5472488 0.5467025 0.5469844 0.5449547 0.5447130 0.5435169 0.5445398 0.5444084
[61] 0.5425626 0.5411765 0.5416299 0.5420162 0.5424376 0.5403617 0.5396337 0.5392732 0.5407820 0.5402198 0.5381467 0.5387087
[73] 0.5371780 0.5376737 0.5401929 0.5394718 0.5418978 0.5409502 0.5409502 0.5393798
> sensitivity_test
 [1] 0.6358772 0.6362367 0.6382693 0.6409018 0.6396655 0.6430640 0.6450194 0.6439750 0.6483007 0.6481195 0.6490643 0.6455243
[13] 0.6471334 0.6490470 0.6469557 0.6440849 0.6449763 0.6464241 0.6482134 0.6441147 0.6443609 0.6427679 0.6460421 0.6503006
[25] 0.6474551 0.6444280 0.6440264 0.6456037 0.6474750 0.6500367 0.6494141 0.6480938 0.6458636 0.6478805 0.6487007 0.6487923
[37] 0.6495788 0.6476122 0.6513651 0.6468615 0.6430113 0.6422939 0.6416627 0.6445826 0.6431644 0.6443274 0.6451999 0.6432329
[49] 0.6427036 0.6435879 0.6431770 0.6422018 0.6429245 0.6429243 0.6435435 0.6423733 0.6426077 0.6420613 0.6429234 0.6434180
[61] 0.6423307 0.6415441 0.6418391 0.6420520 0.6428244 0.6409373 0.6410784 0.6407678 0.6420908 0.6415353 0.6404188 0.6409732
[73] 0.6393704 0.6398450 0.6420118 0.6417707 0.6435711 0.6431808 0.6431808 0.6421624
> specificity
 [1] 0.4718137 0.4677288 0.4501634 0.4534314 0.4366830 0.4460784 0.4395425 0.4424020 0.4419935 0.4419935 0.4407680 0.4338235
[13] 0.4317810 0.4358660 0.4244281 0.4248366 0.4183007 0.4244281 0.4289216 0.4219771 0.4203431 0.4158497 0.4227941 0.4297386
[25] 0.4227941 0.4121732 0.4048203 0.4089052 0.4097222 0.4154412 0.4133987 0.4117647 0.4019608 0.4027778 0.4035948 0.4060458
[37] 0.4052288 0.4031863 0.4105392 0.3978758 0.3917484 0.3884804 0.3872549 0.3929739 0.3901144 0.3929739 0.3946078 0.3905229
[49] 0.3888889 0.3880719 0.3815359 0.3786765 0.3815359 0.3794935 0.3786765 0.3745915 0.3729575 0.3700980 0.3713235 0.3692810
[61] 0.3656046 0.3627451 0.3635621 0.3643791 0.3635621 0.3615196 0.3582516 0.3578431 0.3594771 0.3590686 0.3545752 0.3549837
[73] 0.3541667 0.3545752 0.3574346 0.3553922 0.3590686 0.3566176 0.3566176 0.3537582


KNN CROSS VALIDATION

> library(caret)
> set.seed(42)
> start.time<-Sys.time()
> trControl <- trainControl(method  = "repeatedcv",
+                           number  = 10)
> set.seed(2)
> fit <- train(state ~ .,
+              data       = final_binddata,
+             method     = "knn",
+             tuneGrid   = expand.grid(k = 70:80),
+             trControl  = trControl,
+             metric     = "Specificity"
+ )

> fit
k-Nearest Neighbors 

20000 samples
   38 predictor
    2 classes: 'failed', 'successful' 

No pre-processing
Resampling: Cross-Validated (10 fold, repeated 1 times) 
Summary of sample sizes: 17999, 17999, 18000, 18000, 18000, 17999, ... 
Resampling results across tuning parameters:

  k   Accuracy   Kappa    
  70  0.6151010  0.1657505
  71  0.6144006  0.1639236
  72  0.6139508  0.1627879
  73  0.6144007  0.1632637
  74  0.6147507  0.1635595
  75  0.6146511  0.1629551
  76  0.6150505  0.1640697
  77  0.6138503  0.1611800
  78  0.6138004  0.1607120
  79  0.6136503  0.1597471
  80  0.6140000  0.1600700

Accuracy was used to select the optimal model using the largest value.
The final value used for the model was k = 70.

> plot(fit)
 
> pred<-predict(fit, newdata = final_binddata)
> confusionMatrix(pred,final_binddata$state)
Confusion Matrix and Statistics

            Reference
Prediction   failed successful
  failed       9391       5104
  successful   2273       3232
                                          
               Accuracy : 0.6312          
                 95% CI : (0.6244, 0.6378)
    No Information Rate : 0.5832          
    P-Value [Acc > NIR] : < 2.2e-16       
                                          
                  Kappa : 0.2027          
 Mcnemar's Test P-Value : < 2.2e-16       
                                          
            Sensitivity : 0.8051          
            Specificity : 0.3877          
         Pos Pred Value : 0.6479          
         Neg Pred Value : 0.5871          
             Prevalence : 0.5832          
         Detection Rate : 0.4696     





LDA CODE-
> getwd()
[1] "/Users/muskanjindal"
> Data1 <- read.csv("/Users/muskanjindal/Desktop/kickstarter-projects/proj.csv")
> head(Data1)
                                                      name main_category      deadline goal      launched      state
1                  Acting Out Yoga Presents: Anna in Paris    Publishing  7/2/12 23:08 1500  6/2/12 23:08     failed
2                                  Auto Icon Screen Prints        Design  3/18/15 1:00 1500 2/12/15 19:20 successful
3 Peter Squires' New 7" Record - Recorded by Steve Albini!         Music   2/1/16 3:00  500  1/5/16 20:40 successful
4                                   Much Ado About Nothing       Theater 4/30/12 22:00 6000 3/29/12 15:08     failed
5                                                    Bacon          Food  9/9/14 21:18   23 7/11/14 21:18     failed
6                                          MARLEY WAS DEAD    Publishing  8/1/13 19:00 4000  7/1/13 19:00 successful
  backers .data_Film...Video .data_Music .data_Food .data_Crafts .data_Games .data_Design .data_Comics .data_Publishing
1       0                  0           0          0            0           0            0            0                1
2     971                  0           0          0            0           0            1            0                0
3      31                  0           1          0            0           0            0            0                0
4       9                  0           0          0            0           0            0            0                0
5       0                  0           0          1            0           0            0            0                0
6      99                  0           0          0            0           0            0            0                1
  .data_Fashion .data_Theater .data_Art .data_Photography .data_Technology .data_Dance .data_Journalism Season
1             0             0         0                 0                0           0                0 Summer
2             0             0         0                 0                0           0                0 Winter
3             0             0         0                 0                0           0                0 Winter
4             0             1         0                 0                0           0                0 Spring
5             0             0         0                 0                0           0                0 Summer
6             0             0         0                 0                0           0                0 Summer
  Prj_Name_Length Duration Launched_Year Deadline_Year
1              39       30          2012          2012
2              23       34          2015          2015
3              56       27          2016          2016
4              22       32          2012          2012
5               5       60          2014          2014
6              15       31          2013          2013
> num_columns <- c('Prj_Name_Length')
> Data1[num_columns] <- sapply(Data1[num_columns], as.numeric)
> Prj_Name_Length<-Data1$Prj_Name_Length
> Prj_Name_Length
[2,]              16
    [3,]              52
    [4,]              15
    [5,]              45
    [6,]               7
    [7,]              54
    [8,]              54
    [9,]              20
   [10,]              55
#As the result set is huge, we have shown only specific rows.

> cut(Prj_Name_Length,10)
   [1] (26.2,34.6] (9.4,17.8]  (51.4,59.8] (9.4,17.8]  (43,51.4]   (0.916,9.4] (51.4,59.8] (51.4,59.8] (17.8,26.2]
  [10] (51.4,59.8] (0.916,9.4] (51.4,59.8] (43,51.4]   (0.916,9.4] (9.4,17.8]  (0.916,9.4] (17.8,26.2] (9.4,17.8] 
  [19] (51.4,59.8] (34.6,43]   (17.8,26.2] (9.4,17.8]  (43,51.4]   (43,51.4]   (34.6,43]   (17.8,26.2] (43,51.4]  
  [28] (0.916,9.4] (51.4,59.8] (34.6,43]   (34.6,43]   (34.6,43]   (0.916,9.4] (17.8,26.2] (26.2,34.6] (51.4,59.8]
  [37] (9.4,17.8]  (26.2,34.6] (43,51.4]   (17.8,26.2] (0.916,9.4] (51.4,59.8] (9.4,17.8]  (26.2,34.6] (51.4,59.8]
  [46] (17.8,26.2] (34.6,43]   (51.4,59.8] (51.4,59.8] (0.916,9.4] (0.916,9.4] (0.916,9.4] (34.6,43]   (34.6,43]  
  [55] (0.916,9.4] (43,51.4]   (43,51.4]   (34.6,43]   (17.8,26.2] (43,51.4]   (51.4,59.8] (17.8,26.2] (17.8,26.2]
> Data1$bins<-cut(Prj_Name_Length,10,labels=c("First","Second","Third","Fourth","Five","Six","Seven","eight","nine","ten"))
> Data1
                                                                                       name main_category       deadline
1                                                   Acting Out Yoga Presents: Anna in Paris    Publishing   7/2/12 23:08
2                                                                   Auto Icon Screen Prints        Design   3/18/15 1:00
3                                  Peter Squires' New 7" Record - Recorded by Steve Albini!         Music    2/1/16 3:00
4                                                                    Much Ado About Nothing       Theater  4/30/12 22:00
5                                                                                     Bacon          Food   9/9/14 21:18
6                                                                           MARLEY WAS DEAD    Publishing   8/1/13 19:00
7                                Hip-Hop Script - Rhyming Prose in Poetic Storytelling Form    Publishing 10/30/14 21:58
8                                They All Fall Down: Book and Music Inspired by True Events    Publishing   3/15/13 4:59
9                                                               Power outage survival stove        Design   6/7/16 17:07
10                              Po-Rum-Bo - A card matching game with an intersecting twist         Games   5/29/12 3:00
11                                                                         Go F#@D yourself        Crafts   11/7/14 0:11
12                             Launch Franklin Home Page: The Go To Place for Franklin News    Journalism   8/31/12 1:38
13                                       The First (Ever!) Buffalo Cherry Blossom Festival!           Art 12/31/13 21:15
14                                                                         Cookie Dunk Dunk         Games   4/5/14 16:14
15                                                                 RiverRock Music Festival         Music   11/3/14 6:00
16                                                                        Heroes Everywhere           Art   6/6/12 22:31
17                                                                High Voltage Image Making           Art  3/26/14 16:33
18                                                                     CMYK 4 Poster Series        Design  7/19/12 22:35
19                             Forensics Forever!- Committed to performing arts excellence!       Theater  5/25/15 18:46
20                                             Nuanced Concrete: Postcards from Apocalypses           Art   8/30/13 3:10
> smp_size <- floor(0.70*nrow(proj))
> set.seed(123)
> train_ind <- sample(seq_len(nrow(Data1)), size=smp_size)
> train <- Data1[train_ind, ]
> test <- Data1[-train_ind, ]
> dim(train)
[1] 14000    28
> dim(test)
[1] 6000   28
> library(MASS)
> lda.fit=lda(state ~ main_category+goal+Season+Launched_Year+Duration+Deadline_Year+bins, train)
> lda.fit
Call:
lda(state ~ main_category + goal + Season + Launched_Year + Duration + 
    Deadline_Year + bins, data = train)

Prior probabilities of groups:
    failed successful 
 0.5848571  0.4151429 

Group means:
           main_categoryComics main_categoryCrafts main_categoryDance main_categoryDesign main_categoryFashion
failed              0.02296043          0.03004397        0.006717147          0.06924768           0.05959941
successful          0.04129387          0.01428080        0.020474880          0.05970406           0.03940124
           main_categoryFilm & Video main_categoryFood main_categoryGames main_categoryJournalism main_categoryMusic
failed                     0.1836834        0.07694187         0.07034685             0.016243283          0.1308012
successful                 0.1866827        0.04886442         0.08224363             0.007226428          0.2088782
           main_categoryPhotography main_categoryPublishing main_categoryTechnology main_categoryTheater      goal
failed                   0.03297509              0.12652662              0.07840743           0.01831949 50520.798
successful               0.02271163              0.08843772              0.04026153           0.05075705  9337.762
           SeasonSpring SeasonSummer SeasonWinter Launched_Year Duration Deadline_Year binsSecond binsThird binsFourth
failed        0.2641671    0.2805325    0.2149487      2013.664 35.74145      2013.733  0.1606009 0.1653639  0.1212750
successful    0.2713352    0.2646249    0.2064694      2013.244 32.78527      2013.302  0.1305919 0.1637990  0.1383345
            binsFive   binsSix binsSeven   binseight    binsnine    binsten
failed     0.1373962 0.1069858 0.1133366 0.009159746 0.002076209 0.02283830
successful 0.1720578 0.1290434 0.1297316 0.008258775 0.002236752 0.01892636

Coefficients of linear discriminants:
                                    LD1
main_categoryComics        1.001926e+00
main_categoryCrafts       -1.244674e+00
main_categoryDance         1.700155e+00
main_categoryDesign       -3.788295e-01
main_categoryFashion      -8.358232e-01
main_categoryFilm & Video -1.688718e-01
main_categoryFood         -8.137964e-01
main_categoryGames         1.958781e-01
main_categoryJournalism   -1.415591e+00
main_categoryMusic         5.382244e-01
main_categoryPhotography  -9.493042e-01
main_categoryPublishing   -8.754542e-01
main_categoryTechnology   -1.098039e+00
main_categoryTheater       1.420326e+00
goal                      -1.352643e-07
SeasonSpring              -1.372865e-02
SeasonSummer              -2.104731e-01
SeasonWinter              -4.520619e-03
Launched_Year              5.483242e-02
Duration                  -3.834316e-02
Deadline_Year             -2.974260e-01
binsSecond                 2.905303e-01
binsThird                  5.239005e-01
binsFourth                 7.625072e-01
binsFive                   9.358461e-01
binsSix                    9.464679e-01
binsSeven                  8.967967e-01
binseight                  4.668420e-01
binsnine                   3.298359e-02
binsten                    3.091376e-01
> lda.pred=predict(lda.fit, Data1)
> names(lda.pred)
[1] "class"     "posterior" "x"        
> lda.class=lda.pred$class
> table(lda.class, Data1[,6])
            
lda.class    failed successful
  failed       9449       5163
  successful   2215       3173
> mean(lda.class==Data1[,6])
[1] 0.6311
> sum(lda.pred$posterior[,1]>=.5)
[1] 14612
> sum(lda.pred$posterior[,1]<.5)
[1] 5388
> lda.pred$posterior[1:20,1]
        1         2         3         4         5         6         7         8         9        10        11        12 
0.6073702 0.6941895 0.4766350 0.3297543 0.7782492 0.7410805 0.6269357 0.6311821 0.8060586 0.5324853 0.7799336 0.6628902 
       13        14        15        16        17        18        19        20 
0.4859957 0.6818374 0.6056855 0.5631569 0.5561951 0.6815137 0.3639249 0.4845823 
> lda.class[1:20]
 [1] failed     failed     successful successful failed     failed     failed     failed     failed     failed    
[11] failed     failed     successful failed     failed     failed     failed     failed     successful successful
Levels: failed successful
> sum(lda.pred$posterior[,1]>.9)
[1] 11
 
LDA CROSS VALIDATION
> library(MASS)
> library(dplyr)
> Data1 <- read.csv("/Users/muskanjindal/Desktop/kickstarter-projects/proj.csv")
> head(Data1)
                                                      name main_category      deadline goal      launched      state
1                  Acting Out Yoga Presents: Anna in Paris    Publishing  7/2/12 23:08 1500  6/2/12 23:08     failed
2                                  Auto Icon Screen Prints        Design  3/18/15 1:00 1500 2/12/15 19:20 successful
3 Peter Squires' New 7" Record - Recorded by Steve Albini!         Music   2/1/16 3:00  500  1/5/16 20:40 successful
4                                   Much Ado About Nothing       Theater 4/30/12 22:00 6000 3/29/12 15:08     failed
5                                                    Bacon          Food  9/9/14 21:18   23 7/11/14 21:18     failed
6                                          MARLEY WAS DEAD    Publishing  8/1/13 19:00 4000  7/1/13 19:00 successful
  backers .data_Film...Video .data_Music .data_Food .data_Crafts .data_Games .data_Design .data_Comics .data_Publishing
1       0                  0           0          0            0           0            0            0                1
2     971                  0           0          0            0           0            1            0                0
3      31                  0           1          0            0           0            0            0                0
4       9                  0           0          0            0           0            0            0                0
5       0                  0           0          1            0           0            0            0                0
6      99                  0           0          0            0           0            0            0                1
  .data_Fashion .data_Theater .data_Art .data_Photography .data_Technology .data_Dance .data_Journalism Season
1             0             0         0                 0                0           0                0 Summer
2             0             0         0                 0                0           0                0 Winter
3             0             0         0                 0                0           0                0 Winter
4             0             1         0                 0                0           0                0 Spring
5             0             0         0                 0                0           0                0 Summer
6             0             0         0                 0                0           0                0 Summer
  Prj_Name_Length Duration Launched_Year Deadline_Year
1              39       30          2012          2012
2              23       34          2015          2015
3              56       27          2016          2016
4              22       32          2012          2012
5               5       60          2014          2014
6              15       31          2013          2013
> num_columns <- c('Prj_Name_Length')
> Data1[num_columns] <- sapply(Data1[num_columns], as.numeric)
> Prj_Name_Length<-Data1$Prj_Name_Length
> Prj_Name_Length   
 [2,]              16
    [3,]              52
    [4,]              15
    [5,]              45
    [6,]               7
    [7,]              54
    [8,]              54
    [9,]              20
   [10,]              55
[ reached getOption("max.print") -- omitted 19000 rows ]
# As the result set is huge, we have shown only specific rows.

> cut(Prj_Name_Length,10)
   [1] (26.2,34.6] (9.4,17.8]  (51.4,59.8] (9.4,17.8]  (43,51.4]   (0.916,9.4] (51.4,59.8] (51.4,59.8] (17.8,26.2]
  [10] (51.4,59.8] (0.916,9.4] (51.4,59.8] (43,51.4]   (0.916,9.4] (9.4,17.8]  (0.916,9.4] (17.8,26.2] (9.4,17.8] 
  [19] (51.4,59.8] (34.6,43]   (17.8,26.2] (9.4,17.8]  (43,51.4]   (43,51.4]   (34.6,43]   (17.8,26.2] (43,51.4]  
  [28] (0.916,9.4] (51.4,59.8] (34.6,43]   (34.6,43]   (34.6,43]   (0.916,9.4] (17.8,26.2] (26.2,34.6] (51.4,59.8]
  [37] (9.4,17.8]  (26.2,34.6] (43,51.4]   (17.8,26.2] (0.916,9.4] (51.4,59.8] (9.4,17.8]  (26.2,34.6] (51.4,59.8]
  [46] (17.8,26.2] (34.6,43]   (51.4,59.8] (51.4,59.8] (0.916,9.4] (0.916,9.4] (0.916,9.4] (34.6,43]   (34.6,43]  
  [55] (0.916,9.4] (43,51.4]   (43,51.4]   (34.6,43]   (17.8,26.2] (43,51.4]   (51.4,59.8] (17.8,26.2] (17.8,26.2]




  
