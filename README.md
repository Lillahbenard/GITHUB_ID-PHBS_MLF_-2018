# PHBS_MLF_2018

[Arianna MISERICORDIA](https://github.com/ariannamisericordia) 1802010234

[Ewa GERUS](https://github.com/ewagerus)  1802010260

[Noam PELEG](https://github.com/Noam-Peleg) 1802010275

[Lillah BENARD](https://github.com/Lillahbenard) 1802010264

# _Prediction of Automotive Accident Severity_ 

**MOTIVATION**:

The motivation behind our research is the understanding of specific conditions that affect the severity of an automotive accident. The purpose of this project is to highlight impactful variables while operating a vehicle in order to improve accident prevention.

**GOAL**: 

We executed a classification based on U.K. road accidents ranging from 2014 to 2016 using the methodologies covered in class (Ordered Logistic Regression, Neural network, KNN, Decision tree). Our classification specifies the impact of certain features on car wreckage. 

**DATA SOURCE**: 

The data collected comes from the U.K. government who amassed traffic data based on police reports. 
The analysis of data executed here is composed of the U.K. road accidents from 2014 to 2016. 

Accidents are recorded according to these features:
*  Reference Number
*  Grid Ref: Easting
*  Grid Ref: Northing
*  Expr1
*  Severity 
*  Day of the week 
*  Time (24hr)
*  1st Road Class
*  Road surface
*  Accident date
*  Weather condition 
*  Lighting conditions
*  Number of vehicles 
*  Casualty class
*  Sex of casualty
*  Age of casualty
*  Type of vehicle

**DATASET SOURCE**:

https://data.gov.uk/dataset/6efe5505-941f-45bf-b576-4c1e09b579a1/road-traffic-accidents

**METHODOLOGY**: 

**_I. Data preprocessing_**:

![data preprocessing](https://user-images.githubusercontent.com/43052624/48182461-2b741f80-e366-11e8-8ceb-9b13cd1b1f66.png)

*  Merging datasets

*  Dropping columns containing references (Reference number, Grid Ref: Easting, Grid Ref: Northing) and correlated variables (Lighting conditions, Accident Date).

*  Dealing with missing data by deleting observations that are labeled with NaNs.

*  Listing variables:
   *  Time (24hr): Day-time, Night-time
   *  Weather conditions: Fine, Snowing, Raining, Fog, Other
   *  Type of Vehicle: Car, Bus, Goods vehicles, Motorcycle, Other
   *  Day: Weekday, Weekend
   *  Casualty class: Passenger, Pedestrian, Driver

*  Creating dummies and dropping variables containing the same information (Sex of casualty_Female, Day_Weekday, Time (24hr)_Day-time)
    
* Resampling unbalanced data

  *  Slight: 6739, Serious: 957, Fatal: 48
     * Undersampling from slight to serious
     
  *  Slight: 957, Serious: 957, Fatal: 48
     * Oversampling from fatal to serious
     
  *  Slight: 957, Serious: 957, Fatal: 957
  
**_II. Standardization and PCA_**:

 * Standardization
  
 * PCA

 ![pca](https://user-images.githubusercontent.com/43052624/48190945-ef00ed80-e37e-11e8-9d02-4dfffc4967c1.png)

We utilize the first 12 components as they make up approximately 90% of the variance.

**_III. Prediction_**:

Accuracy of each of the following methods were examined to choose the best classifier for reaching our goal. To implement the methods mentioned below, scikit-learn and Keras were used. 

To avoid overfitting, we used K-fold cross-validation method with ten splits. 

*  **Decision Tree**

Our graph shows the depth that returns the best accuracy based on the number of features that we have in the dataset.

![kfold decision tree](https://user-images.githubusercontent.com/43052624/48170888-87be4b80-e334-11e8-8302-7c8437f7903f.png)

K-fold best mean accuracy is 73.95% for a decision tree depth equal to six.

![decision tree](https://user-images.githubusercontent.com/43052624/48113500-116b0c00-e296-11e8-8a0f-52ce61ae41cc.png)

The three most important features in the decision tree model are: Casualty Class_Pedestrian, Road Surface_Dry, Road Surface_Wet or Damp.

*  **Neural Network**

Using standarized data after PCA.

Two hidden layers each containing 24 nodes.

The mean accuracy is equal to 72.41% (standard deviation 2.46%).

*  **KNN**

Using standarized data after PCA.

Our graph shows the number of neighbors that returns the best accuracy based on the number of features that we have in the dataset.

![kfold knn](https://user-images.githubusercontent.com/43052624/48171438-dcfb5c80-e336-11e8-82e7-7f259129e643.png)

K-fold best mean accuracy is 71.37% (standard deviation 2.77%) for n_neighbors equal to five.

*  **Ordered Logistic Regression**

_With PCA_

The mean accuracy is equal to 53.12% (standard deviation 2.32%)

_Without PCA_

Drop reference variable

Plotting correlation matrix

Drop 'Road Surface' due to its high correlation with 'Weather Condition'

The mean accuracy is equal to 53.54% (standard deviation 2.67%)

![logistic regression](https://user-images.githubusercontent.com/43052624/48114206-1ed5c580-e299-11e8-80b8-1e1cc922a2a0.png)

**CONCLUSION**: 

![summary](https://user-images.githubusercontent.com/43052624/48114312-8724a700-e299-11e8-86e6-2bc53ce08bbf.png)

The best model is the decision tree with a mean accuracy of 73.95%. 

We can conclude that the three most important features that affect the severity of an automotive accident are: Casualty Class_Pedestrian, Road Surface_Dry, Road Surface_Wet or Damp.
