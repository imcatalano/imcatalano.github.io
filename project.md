## Hurricanes and Tropical Storms

My goal for this project was to use machine learning techniques to predict the highest category of a hurricane based on other measurements, including distance traveled, wind speed, and pressure. 

***

## Introduction 

Tropical storms and hurricanes are categorized according to the Saffir-Simpson Hurricane Wind Scale [4]. Each hurricane is given a rating from 1 to 5 depending on its sustained wind speeds. Categorizing tropical storms allows for the prediction of damage and hazards, so people living in an area in the path of the storm can prepare for the storm and evacuate if necessary. Tropical storms form over the ocean and then increase in intensity as they move away from their starting point. Therefore, it is difficult to predict what the storm will be like when it reaches inhabited areas. Currently, researchers at  National Aeronautics and Space Administration are working on a machine learning model that can be used to predict the intensity of hurricanes across its life cycle [1].


Fortunately, scientists have completed thorough records of every hurricane that they have observed, and I can use one of these datasets to apply my machine learning model to. In order to determine which method to use, I referred to the scikit-learn algorithm cheat sheet [2]. I decided to apply both ridge regression, multi-layer perceptron regression, and logistic regression to the dataset.

I found that ridge regression and MLP regression did not accurately predict the hurricane category; the Regression Error Characteristic (REC) curves for both the linear regression and the MLP regression converged at an accuracy less than 60%. However, when I used logistic regression to fit a model and then create a confusion matrix, I observed that this model was most successful in predicting category four hurricanes. From my results, I can conclude that machine learning can be very helpful in predicting the category of a hurricane based on the recorded measurements of the storm. 


## Data

For my project, I analyzed [data](/assets/storms.csv) collected by the National Oceanic and Atmospheric Administration. This dataset is on [kaggle.com](https://www.kaggle.com/datasets/utkarshx27/noaa-atlantic-hurricane-database), and it includes various measurements of Atlantic Hurricanes that occurred between 1975 and 2021. I chose to focus specifically on the dates, longitude and latitude, wind speed, pressure, and category of each storm. There are 19,066 rows in the dataset that provide information for 258 different hurricanes that occurred over the 46 year timespan. 

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

I used another for-loop to plot the wind speed and pressure of each individual hurricane. Some storms had insufficient data to create a clear graph, but the results of the other hurricanes can be seen [here](/hurricaneplots.md). 

Before applying the regression model, I combined the values I had calculated from the original dataset into a [new dataset](/dataset2.csv).


## Modeling

The goal was to apply a machine learning model that would make a prediction based on known data, so I used supervised machine learning. The dataset was large and I was predicting one variable (hurricane category) from seven other variables. I also wanted to determine the accuracy of a machine learning model. Therefore, I applied ridge regression and MLP regression, which would yield a REC curve, and I applied logistic regression, which would produce a confusion matrix. For both models, I set the maximum number of iterations to be 5000 to allow for model optimization. For the ridge regression, I minimized the root mean square error (RMSE) by defining alpha as 0.01. To create the REC curve for ridge regression (Figure 8), I tried various values for the maximum tolerance in an attempt to increase the accuracy of the model's prediction. However, the REC curve converged to a value below 60% regardless of the tolerance. I decided on a tolerance of 75, which would show enough of this convergence in order to understand the graph's behavior. Next, I applied MLP regression and compared the REC curve for this model to the curve for ridge regression. For the first MLP regressor, I did not define the size of the hidden layers, but for the second MLP regressor, I defined the perceptron as having three hidden layers with 100 neurons in each layer. 


## Results

### Linear Regression

  <img align="center" src="/assets/IMG/RidgeRegression (4).png">
  
*Figure 8: REC Curve for Ridge Regression*

Figure 8 shows the REC curve for ridge regression converging below a value of 60 for the percentage of correct predictions. The ridge regression model produced a RMSE of about 0.4005.


### Multi-Layer Preceptron Regression

  <img align="center" src="/assets/IMG/MLPCurve (3).png">
  
*Figure 9: REC Curve for MLP Regression*

Figure 9 presents a comparison between the ridge regression REC curve, MLP regression with the default value of one hidden layer with 100 perceptrons, and MLP regression with a hidden layer with 10 perceptrons. The RMSE for the first MLP regression model was about 0.3842, and the RMSE for the second MLP regression model was about 0.2927.


### Confusion Matrix

  <img align="center" src="/assets/IMG/ConfusionMatrix (2).png">
  
*Figure 10: Confusion Matrix for Logistic Regression*

Figure 10 shows the confusion matrix for the logistic regression model. The highest values on the confusion matrix are 14 correct predictions of a hurricane with no category assigned, and 16 correct predictions of category four hurricanes. The model never predicted category 2 or category 5 -- the two category 2 hurricanes were predicted by the model to be category 1, and the five category 5 hurricanes were predicted to be category 4. 



## Discussion

In Figure 8, one can see that the accuracy of the ridge regression model reaches its maximum value at around 55%, so I can conclude that the ridge regression model is correct only half of the time. Figure 9 shows that the REC curves for both MLP regressors converge to the same maximum accuracy, but both models show a greater increase in accuracy within the first 25 iterations. The RMSE for the linear regressor, MLP regressor 1, and MLP regressor 2 are 0.4005, 0.3842, and 0.2927 respectively, so I can conclude that using the MLP regressor produces a more accurate model. Additionally, a MLP regressor model with three hidden layers of 100 neurons will be more accurate than a MPL regressor with only one hidden layer of 100 neurons. However, none of these three models are able to predict the hurricane category with higher than 60% accuracy. While this value is greater than the 20% chance someone has of randomly guessing a hurricane’s category, the model can still be improved. 


I applied logistic regression to the hurricane data in order to predict the target variable, which in this case was the category of the hurricane. For the 52 samples in the test data set, the model correctly predicted the category of 34 hurricanes, which corresponds to 65.38% accuracy. This value is still not ideal, but it is at least 10% greater than the accuracy shown by the REC curves for ridge regression and MLP regression. 



## Conclusion

From applying these machine learning techniques, the highest accuracy of a model that I could get was 65%. I believe this was partly because of the way I processed the dataset before applying the machine learning methods. The initial dataset had 19,000 rows of data, but I wanted to look at each individual hurricane. There were measurements for 258 hurricanes in the data, so this was my sample size. This sample size resulted in a training data set with only 52 rows. To adjust for this, I could use hurricane data from 1851 [3] and make calculations for every recorded hurricane since that year. I could also use the full data set, and I could incorporate the year, day, and time data into the model. 

I can conclude that machine learning methods can be used to create a model that can predict the category of a hurricane. However, there are several variables besides the ones that I used that need to be considered in the model. I think that the ideal model will be able to predict the maximum wind speed, the distance traveled, and the category of a hurricane depending on its starting position and its initial wind speed, as well as factors unrelated to the hurricane such as atmospheric conditions. 


## References
[1] “A Machine-Learning Assist to Predicting Hurricane Intensity.” NASA, NASA, 20 Sept. 2023, www.nasa.gov/centers-and-facilities/jpl/a-machine-learning-assist-to-predicting-hurricane-intensity/. 

[2] “Choosing the Right Estimator.” Scikit, scikit-learn.org/stable/tutorial/machine_learning_map/index.html. Accessed 8 Dec. 2023. 

[3] Re-analysis Project, https://www.aoml.noaa.gov/hrd/data_sub/re_anal.html. Accessed 8 Dec. 2023.

[4] Saffir-Simpson Hurricane Wind Scale, www.nhc.noaa.gov/aboutsshws.php. Accessed 8 Dec. 2023. 


[back](./)

