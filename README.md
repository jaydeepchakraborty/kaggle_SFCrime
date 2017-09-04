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

2) we have done the same process for all other columns except X, Y : coordinates. Now it looks like following.
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/DataScreenShotUpdated.png"/>

--Following is bar chart of frequency of target(Category) of the dataset. From the figure, we can see the data is imbalanced. We will use <b>SMOTE</b> to balance it. We should not use SMOTE on testing set and it will be used only once.
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/data_freq.png"/>


--Most of the data in the dataset are categorical.It is hard to plot histogram or box plot for each column. Standardization does not make sense here. We can plot a scatter plot for different Categories to under stand the pattern of the data.

--Now we did not change the co-ordinates value, so we have to do normalize those columns only.<br>
[Normalization: rescaling data into range of [0,1]]
<img width="600" height="200" alt="data_screenshot" src="https://github.com/jaydeepchakraborty/kaggle_SFCrime/blob/master/img/DataScreenShotNormalized.png"/>


