San Francisco Crime Classification (https://www.kaggle.com/c/sf-crime)
==================================

DataSet:
---------
This dataset contains incidents derived from SFPD Crime Incident Reporting system. 

Goal:
------
Find the category of the Crime.

Dates - timestamp of the crime incident<br>
Category - category of the crime incident (only in train.csv). This is the target variable you are going to predict.<br>
Descript - detailed description of the crime incident (only in train.csv)<br>
DayOfWeek - the day of the week<br>
PdDistrict - name of the Police Department District<br>
Resolution - how the crime incident was resolved (only in train.csv)<br>
Address - the approximate street address of the crime incident <br>
X - Longitude<br>
Y - Latitude<br>


Project Modules:

Module1:
--------------------------------------------
a) Data analysis

--There are total 878049 obs.(rows) of  9 variables(cols)</br>

--Following is the screenshot of the dataset.
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/DataScreenShot.png"/>

From the figure it is visible that most of the columns are String. We have changed the followings in dataset.
1) The date-time range is 2003-01-06 00:01:00 - 2015-05-13 23:53:00
We are replacing the datetime into two categories 00-12: 1, 12-24:2. Here we are not considering the date as the time span is 2003-01-06 - 2015-05-13. We can represent the date or month or year for increasing the feature values but for the time being we stick to the time of the day.

2) We converted all the data into numeric from string except X, Y : coordinates.

3) X, Y (coordinate) are normalized as they have high values. Now the dataset looks like the following.

<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/DataScreenShotUpdated.png"/>


--Most of the data in the dataset are categorical.It is hard to plot histogram or box plot for each column. Standardization does not make sense here. We can plot a scatter plot for different Categories to under stand the pattern of the data. Now this dataset contains all factor features except (X,Y). we have used PCA to plot the scatter plot based on the primary component1(X,Y).

<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/pca_.jpeg"/>

-- Now we plot corelation matrix between X-Y. So it is clear X and Y are highly positive-corelated. We can remove any one of the column.
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/corr_.jpeg"/>


--Following is bar chart of frequency of target(Category) of the dataset. From the figure, we can see the data is imbalanced. We will use <b>SMOTE</b> to balance it. We should not use SMOTE on testing set and it will be used only once.
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/df_.jpeg"/>

- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) It seems SMOTE can work on binomial cases. working on this issue.

Module2:
------------------------------
a) Data split:

train:70%
test:30%

We have used 10 fold cross fold validation to find out the best hyper parameter for SVM algo.<br>

<b>
Parameter tuning of ‘svm’:

- sampling method: 10-fold cross validation 

- best parameters:
 gamma cost
   0.1    1

- best performance: 0.2448718 </b>

Module3:
------------------------------
a) Evaluation:

<b>
Confusion Matrix and Statistics
         
  <table>
    <tr>
      <td colspan=4 align="right">Reference</td>
    </tr>
    <tr>
      <td>Prediction</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  <tr>
      <td>1</td>
      <td>34</td>
      <td>0</td>
      <td>2</td>
    </tr>
  <tr>
      <td>2</td>
      <td>0</td>
      <td>28</td>
      <td>12</td>
    </tr>
  <tr>
      <td>3</td>
      <td>1</td>
      <td>10</td>
      <td>23</td>
    </tr>
  
  </table>

Overall Statistics
                                         
               Accuracy : 0.7727         
                 95% CI : (0.683, 0.8472)
    No Information Rate : 0.3455         
    P-Value [Acc > NIR] : < 2.2e-16      
                                         
                  Kappa : 0.6589         
 Mcnemar's Test P-Value : NA             

Statistics by Class:


<table>
    <tr>
      <td></td>
      <td>Class: 1</td>
      <td>Class: 2</td>
      <td>Class: 3</td>
    </tr>
    <tr>
      <td>Sensitivity</td>
      <td>0.9714</td>
      <td>0.7368</td>
      <td>0.6216</td>
    </tr>
   <tr>
      <td>Specificity</td>
      <td>0.9733</td>
      <td>0.8333</td>
      <td>0.8493</td>
    </tr>
   <tr>
      <td>Pos Pred Value</td>
      <td>0.9444</td>
      <td>0.7000</td>
      <td>0.6765</td>
    </tr> <tr>
      <td>Neg Pred Value</td>
      <td>0.9865</td>
      <td>0.8571</td>
      <td>0.8158</td>
    </tr> <tr>
      <td>Prevalence</td>
      <td>0.3182 </td>
      <td>0.3455</td>
      <td>0.3364</td>
    </tr> <tr>
      <td>Detection Rate</td>
      <td>0.3091</td>
      <td>0.2545</td>
      <td>0.2091</td>
    </tr> <tr>
      <td>Detection Prevalence</td>
      <td>0.3273</td>
      <td>0.3636</td>
      <td>0.3091</td>
    </tr> <tr>
      <td>Balanced Accuracy</td>
      <td>0.9724</td>
      <td>0.7851</td>
      <td>0.7355</td>
    </tr>
  
  </table>

Resources and Links
------------------------------------
[1] https://machinelearningmastery.com/tune-machine-learning-algorithms-in-r/
