## Hurricanes and Tropical Storms

My goal for this project was to use machine learning techniques to predict the highest category of a hurricane based on other measurements, including position, wind speed, and pressure. 

***

## Introduction 

Tropical storms and hurricanes are categorized according to the Saffir-Simpson Hurricane Wind Scale [1]. Each hurricane is given a rating from 1 to 5 depending on its sustained wind speeds. Categorizing tropical storms allows for the prediction of damage and hazards, so people living in an area in the path of the storm can prepare for the storm and evacuate if necessary. Tropical storms form over the ocean and then increase in intensity as they move away from their starting point. Therefore, it is difficult to predict what the storm will be like when it reaches inhabited areas. Currently, researchers at  National Aeronautics and Space Administration are working on a machine learning model that can be used to predict the intensity of hurricanes across its life cycle [2].


Fortunately, scientists have completed thorough records of every hurricane that they have observed, and I can use one of these datasets to apply my machine learning model to. In order to determine which method to use, I referred to the scikit-learn algorithm cheat sheet [2]. I decided to apply both ridge regression, multi-layer perceptron regression, and logistic regression to the dataset.

I found that ridge regression and MLP regression did not accurately predict the hurricane category; the Regression Error Characteristic (REC) curves for both the linear regression and the MLP regression converged at an accuracy less than 60%. However, when I used logistic regression to fit a model and then create a confusion matrix, I observed that this model was most successful in predicting category four hurricanes. From my results, I can conclude that machine learning can be very helpful in predicting the category of a hurricane based on the recorded measurements of the storm. 


## Data

For my project, I analyzed data collected by the National Oceanic and Atmospheric Administration. This dataset is on kaggle.com, and it includes various measurements of Atlantic Hurricanes that occurred between 1975 and 2021. I chose to focus specifically on the dates, longitude and latitude, wind speed, pressure, and category of each storm. There are 19,066 rows in the dataset that provide information for 258 different hurricanes that occurred over the 46 year timespan. 

When preprocessing the data, I removed the columns that I would not be using, and I replaced NA entries in the "category" column with the number 0. I wanted to look at the data for each individual hurricane, so I created a for-loop to iterate through a matrix that I defined as each unique hurricane name from the dataset. Within the for-loop, I cropped the data to focus on an individual hurricane. Next, I calculated the distance traveled by the hurricane from a distance function that I created (see Figure 1) and the maximum category for each hurricane. I then used another function that I had previously created (see Figure 2)  in order to calculate the minimum, average, and maximum values for the wind speed and the pressure of the hurricane. 

 <img align="center" src="/assets/IMG/Screenshot 2023-12-08 232642.png">
 
*Figure 1: Distance function*


  <img align="center" src="/assets/IMG/Screenshot 2023-12-08 232642.png">


*Figure 2: Mimimum, averages, and maximum values function*

To get a better understanding of the storm data, I created several different plots:

  <img align="center" src="/assets/IMG/AverageValues (1).png">

*Figure 3: Average pressure values and average wind speed values of tropical storms for each year.*

The graph in Figure 3 shows an inverse relationship between wind speed and pressure.


  <img align="center" src="/assets/IMG/distance1.png">

*Figure 4: Distance traveled by each storm*

  <img align="center" src="/assets/IMG/distance2.png">

*Figure 5: Distance traveled by storms each year*

Figure 4 shows variation but no significant trend. However, Figure 5 shows a slight increase in the distance traveled by hurricanes every year. The difference between these two charts would imply an increase in the number of storms each year.

  <img align="center" src="/assets/IMG/windspeedvalues.png">
  
*Figure 6: Average, minimum, and maximum wind speed values for each hurricane*

  <img align="center" src="/assets/IMG/pressurevalues.png">
  
*Figure 7: Average, minimum, and maximum pressure values for each hurricane*

Figure 6 and Figure 7 also show an inverse relationship between wind speed and pressure. There is minimal variation in minimum wind speeds and maximum pressures, and there is a larger variation in maximum wind speeds and minimum pressures. 

Before applying the regression model, I combined the values I had calculated from the original dataset into a [new dataset](dataset1.md).

## Modeling

Linear Regression

  <img align="center" src="/assets/IMG/RidgeRegression (2).png">
  
*Figure 8: REC Curve for Linear Regression*


MLP Regression

  <img align="center" src="/assets/IMG/MLPCurve (1).png">
  
*Figure 9: REC Curve for MLP Regression*


Confusion Matrix

  <img align="center" src="/assets/IMG/ConfusionMatrix.png">
  
*Figure 10: Confusion Matrix for Logistic Regression*

## Results



## Discussion


## Conclusion


## References
[1] “A Machine-Learning Assist to Predicting Hurricane Intensity.” NASA, NASA, 20 Sept. 2023, www.nasa.gov/centers-and-facilities/jpl/a-machine-learning-assist-to-predicting-hurricane-intensity/. 

[2] “Choosing the Right Estimator.” Scikit, scikit-learn.org/stable/tutorial/machine_learning_map/index.html. Accessed 8 Dec. 2023. 

[3] Saffir-Simpson Hurricane Wind Scale, www.nhc.noaa.gov/aboutsshws.php. Accessed 8 Dec. 2023. 


[back](./)

