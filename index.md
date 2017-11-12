---
title: "Practical Machine Learning Course"
subtitle: 'Peer-graded Assignment: Course Project'
author: "P. Duchesne"
date: "12 November 2017"
output: 
  html_document: 
    keep_md: yes
---



####Executive Summary
This project report will use data sets to predict the manner in which 6 participants, as part of a Human Activity Recognition experiment, did specific barbell lift exercises. 

The source data is composed of the measurements of accelerometers located on the belt, forearm, arm, and dumbell of 6 participants. Each were asked to perform barbell lifts correctly and incorrectly in 5 different ways.

The data for this project comes from the Human Activity Recognition - Weight Lifting Exercises Dataset (http://groupware.les.inf.puc-rio.br/har) made available by

*Velloso, E.; Bulling, A.; Gellersen, H.; Ugulino, W.; Fuks, H. Qualitative Activity Recognition of Weight Lifting Exercises. Proceedings of 4th International Conference in Cooperation with SIGCHI (Augmented Human '13) . Stuttgart, Germany: ACM SIGCHI, 2013.*

####Exploratory Data Analysis

The data is split over two data sets, a traing and testing set. 

The training set contains 19622 observations over 160 variables.  The "classe" variable in the training set is the outcome. This will be the variable to predict using the testing data set. 
The testing data set itself contains 20 observations over 160 variables. 

Both these sets were downloaded and placed in data frames for exploration after loading the required libraries. 

####Filtering Predictors

Initial observations show that many of the column variables contained large quantities of NA or blank values. If these columns had a high proportion of such values (over 97%), then I removed the column from the training set to be used to fit the model. These would bear little impact on the model as they were almost completly empty, see **Fig. 1**.


###### **Fig. 1**

  X  user_name    raw_timestamp_part_1   raw_timestamp_part_2  cvtd_timestamp     new_window    num_window   roll_belt   pitch_belt   yaw_belt   total_accel_belt  kurtosis_roll_belt   kurtosis_picth_belt   kurtosis_yaw_belt   skewness_roll_belt   skewness_roll_belt.1   skewness_yaw_belt    max_roll_belt   max_picth_belt  max_yaw_belt    min_roll_belt   min_pitch_belt  min_yaw_belt    amplitude_roll_belt   amplitude_pitch_belt  amplitude_yaw_belt    var_total_accel_belt   avg_roll_belt   stddev_roll_belt   var_roll_belt   avg_pitch_belt   stddev_pitch_belt   var_pitch_belt   avg_yaw_belt   stddev_yaw_belt   var_yaw_belt   gyros_belt_x   gyros_belt_y   gyros_belt_z   accel_belt_x   accel_belt_y   accel_belt_z   magnet_belt_x   magnet_belt_y   magnet_belt_z   roll_arm   pitch_arm   yaw_arm   total_accel_arm   var_accel_arm   avg_roll_arm   stddev_roll_arm   var_roll_arm   avg_pitch_arm   stddev_pitch_arm   var_pitch_arm   avg_yaw_arm   stddev_yaw_arm   var_yaw_arm   gyros_arm_x   gyros_arm_y   gyros_arm_z   accel_arm_x   accel_arm_y   accel_arm_z   magnet_arm_x   magnet_arm_y   magnet_arm_z  kurtosis_roll_arm   kurtosis_picth_arm   kurtosis_yaw_arm   skewness_roll_arm   skewness_pitch_arm   skewness_yaw_arm    max_roll_arm   max_picth_arm   max_yaw_arm   min_roll_arm   min_pitch_arm   min_yaw_arm   amplitude_roll_arm   amplitude_pitch_arm   amplitude_yaw_arm   roll_dumbbell   pitch_dumbbell   yaw_dumbbell  kurtosis_roll_dumbbell   kurtosis_picth_dumbbell   kurtosis_yaw_dumbbell   skewness_roll_dumbbell   skewness_pitch_dumbbell   skewness_yaw_dumbbell    max_roll_dumbbell   max_picth_dumbbell  max_yaw_dumbbell    min_roll_dumbbell   min_pitch_dumbbell  min_yaw_dumbbell    amplitude_roll_dumbbell   amplitude_pitch_dumbbell  amplitude_yaw_dumbbell    total_accel_dumbbell   var_accel_dumbbell   avg_roll_dumbbell   stddev_roll_dumbbell   var_roll_dumbbell   avg_pitch_dumbbell   stddev_pitch_dumbbell   var_pitch_dumbbell   avg_yaw_dumbbell   stddev_yaw_dumbbell   var_yaw_dumbbell   gyros_dumbbell_x   gyros_dumbbell_y   gyros_dumbbell_z   accel_dumbbell_x   accel_dumbbell_y   accel_dumbbell_z   magnet_dumbbell_x   magnet_dumbbell_y   magnet_dumbbell_z   roll_forearm   pitch_forearm   yaw_forearm  kurtosis_roll_forearm   kurtosis_picth_forearm   kurtosis_yaw_forearm   skewness_roll_forearm   skewness_pitch_forearm   skewness_yaw_forearm    max_roll_forearm   max_picth_forearm  max_yaw_forearm    min_roll_forearm   min_pitch_forearm  min_yaw_forearm    amplitude_roll_forearm   amplitude_pitch_forearm  amplitude_yaw_forearm    total_accel_forearm   var_accel_forearm   avg_roll_forearm   stddev_roll_forearm   var_roll_forearm   avg_pitch_forearm   stddev_pitch_forearm   var_pitch_forearm   avg_yaw_forearm   stddev_yaw_forearm   var_yaw_forearm   gyros_forearm_x   gyros_forearm_y   gyros_forearm_z   accel_forearm_x   accel_forearm_y   accel_forearm_z   magnet_forearm_x   magnet_forearm_y   magnet_forearm_z  classe 
---  ----------  ---------------------  ---------------------  -----------------  -----------  -----------  ----------  -----------  ---------  -----------------  -------------------  --------------------  ------------------  -------------------  ---------------------  ------------------  --------------  ---------------  -------------  --------------  ---------------  -------------  --------------------  ---------------------  -------------------  ---------------------  --------------  -----------------  --------------  ---------------  ------------------  ---------------  -------------  ----------------  -------------  -------------  -------------  -------------  -------------  -------------  -------------  --------------  --------------  --------------  ---------  ----------  --------  ----------------  --------------  -------------  ----------------  -------------  --------------  -----------------  --------------  ------------  ---------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  -------------  -------------  -------------  ------------------  -------------------  -----------------  ------------------  -------------------  -----------------  -------------  --------------  ------------  -------------  --------------  ------------  -------------------  --------------------  ------------------  --------------  ---------------  -------------  -----------------------  ------------------------  ----------------------  -----------------------  ------------------------  ----------------------  ------------------  -------------------  -----------------  ------------------  -------------------  -----------------  ------------------------  -------------------------  -----------------------  ---------------------  -------------------  ------------------  ---------------------  ------------------  -------------------  ----------------------  -------------------  -----------------  --------------------  -----------------  -----------------  -----------------  -----------------  -----------------  -----------------  -----------------  ------------------  ------------------  ------------------  -------------  --------------  ------------  ----------------------  -----------------------  ---------------------  ----------------------  -----------------------  ---------------------  -----------------  ------------------  ----------------  -----------------  ------------------  ----------------  -----------------------  ------------------------  ----------------------  --------------------  ------------------  -----------------  --------------------  -----------------  ------------------  ---------------------  ------------------  ----------------  -------------------  ----------------  ----------------  ----------------  ----------------  ----------------  ----------------  ----------------  -----------------  -----------------  -----------------  -------
  1  carlitos               1323084231                 788290  05/12/2011 11:23   no                    11        1.41         8.07      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.00           0.00          -0.02            -21              4             22              -3             599            -313       -128        22.5      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.00          0.00         -0.02          -288           109          -123           -368            337            516  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        13.05217        -70.49400      -84.87394  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02               0.00               -234                 47               -271                -559                 293                 -65           28.4           -63.9          -153  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.03              0.00             -0.02               192               203              -215                -17                654                476  A      
  2  carlitos               1323084231                 808298  05/12/2011 11:23   no                    11        1.41         8.07      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.02           0.00          -0.02            -22              4             22              -7             608            -311       -128        22.5      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.02         -0.02         -0.02          -290           110          -125           -369            337            513  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        13.13074        -70.63751      -84.71065  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02               0.00               -233                 47               -269                -555                 296                 -64           28.3           -63.9          -153  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.02              0.00             -0.02               192               203              -216                -18                661                473  A      
  3  carlitos               1323084231                 820366  05/12/2011 11:23   no                    11        1.42         8.07      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.00           0.00          -0.02            -20              5             23              -2             600            -305       -128        22.5      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.02         -0.02         -0.02          -289           110          -126           -368            344            513  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        12.85075        -70.27812      -85.14078  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02               0.00               -232                 46               -270                -561                 298                 -63           28.3           -63.9          -152  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.03             -0.02              0.00               196               204              -213                -18                658                469  A      
  4  carlitos               1323084232                 120339  05/12/2011 11:23   no                    12        1.48         8.05      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.02           0.00          -0.03            -22              3             21              -6             604            -310       -128        22.1      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.02         -0.03          0.02          -289           111          -123           -372            344            512  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        13.43120        -70.39379      -84.87363  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02              -0.02               -232                 48               -269                -552                 303                 -60           28.1           -63.9          -152  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.02             -0.02              0.00               189               206              -214                -16                658                469  A      
  5  carlitos               1323084232                 196328  05/12/2011 11:23   no                    12        1.48         8.07      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.02           0.02          -0.02            -21              2             24              -6             600            -302       -128        22.1      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.00         -0.03          0.00          -289           111          -123           -374            337            506  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        13.37872        -70.42856      -84.85306  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02               0.00               -233                 48               -270                -554                 292                 -68           28.0           -63.9          -152  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.02              0.00             -0.02               189               206              -214                -17                655                473  A      
  6  carlitos               1323084232                 304277  05/12/2011 11:23   no                    12        1.45         8.06      -94.4                  3  NA                   NA                    NA                  NA                   NA                     NA                              NA               NA  NA                         NA               NA  NA                               NA                     NA  NA                                      NA              NA                 NA              NA               NA                  NA               NA             NA                NA             NA           0.02           0.00          -0.02            -21              4             21               0             603            -312       -128        22.0      -161                34              NA             NA                NA             NA              NA                 NA              NA            NA               NA            NA          0.02         -0.03          0.00          -289           111          -122           -369            342            513  NA                  NA                   NA                 NA                  NA                   NA                            NA              NA            NA             NA              NA            NA                   NA                    NA                  NA        13.38246        -70.81759      -84.46500  NA                       NA                        NA                      NA                       NA                        NA                                      NA                   NA  NA                                 NA                   NA  NA                                       NA                         NA  NA                                          37                   NA                  NA                     NA                  NA                   NA                      NA                   NA                 NA                    NA                 NA                  0              -0.02               0.00               -234                 48               -269                -558                 294                 -66           27.9           -63.9          -152  NA                      NA                       NA                     NA                      NA                       NA                                    NA                  NA  NA                               NA                  NA  NA                                     NA                        NA  NA                                        36                  NA                 NA                    NA                 NA                  NA                     NA                  NA                NA                   NA                NA              0.02             -0.02             -0.03               193               203              -215                 -9                660                478  A      

Further subsetting was implemented during the load and included the elimination of columns with no motion related data (the first seven variables). 




## Building the Model 

After having completed the preparation of the large number potential variables being fitted down from 160 variables to 53 more probable variables, the next step was to fit a model. 

Using the caret package, the Random Forest (rf) method was recommended because of its accuracy as one of the top performing algorithms. It is also recommended to tune the model using the  cross-validation method for the traincontrol, in order to control the overfitting that can result from the rf method. 
Parallel processing was used to reduce the amount of time taken by running this technique.




Our model is fit with over a 99 % accuracy rate using mtry=27 as tuning parameter, see **Fig. 2**. The accuracy obtained was high enough to continue with this model.

###### **Fig. 2**

```
## Random Forest 
## 
## 19622 samples
##    52 predictor
##     5 classes: 'A', 'B', 'C', 'D', 'E' 
## 
## No pre-processing
## Resampling: Cross-Validated (5 fold) 
## Summary of sample sizes: 15697, 15698, 15698, 15697, 15698 
## Resampling results across tuning parameters:
## 
##   mtry  Accuracy   Kappa    
##    2    0.9948527  0.9934888
##   27    0.9946489  0.9932311
##   52    0.9892979  0.9864598
## 
## Accuracy was used to select the optimal model using the largest value.
## The final value used for the model was mtry = 2.
```

We can observe these graphically in **Fig. 3**.

###### **Fig. 3**

![](index_files/figure-html/resample-1.png)<!-- -->

We then apply the confusion matrix to allow us to visualize the classe distribution and related errors. As for the question of our expected out of sample error, the oob error rate is 0.43%. We consider this low enough to confirm our model selection, see **Fig. 4**. 

###### **Fig. 4**


```
## 
## Call:
##  randomForest(x = x, y = y, mtry = param$mtry) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 2
## 
##         OOB estimate of  error rate: 0.41%
## Confusion matrix:
##      A    B    C    D    E  class.error
## A 5579    1    0    0    0 0.0001792115
## B   10 3784    3    0    0 0.0034237556
## C    0   17 3403    2    0 0.0055523086
## D    0    0   39 3175    2 0.0127487562
## E    0    0    1    5 3601 0.0016634322
```

####Conclusion

The resulting accuracy and low OOB error rate obtained by training our model lead us to conlude that our model will be able to accurately predict the classe of exercise performed as part of the test data set. Thank you.