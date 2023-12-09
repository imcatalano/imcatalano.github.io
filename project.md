## Hurricanes and Tropical Storms

My goal for this project was to use machine learning techniques to highest category of a hurricane based on other measurements, including position, wind speed, and pressure. 

***

## Introduction 

Tropical storms and hurricanes are categorized according to the Saffir-Simpson Hurricane Wind Scale [1]. Each hurricane is given a rating from 1 to 5 depending on its sustained wind speeds. Categorizing tropical storms allows for the prediction of damage and hazards, so people living in an area in the path of the storm can prepare for the storm and evacuate if necessary. Tropical storms form over the ocean and then increase in intensity as they move away from their starting point. Therefore, it is difficult to predict what the storm will be like when it reaches inhabitied areas. Currently, reserachers at  National Aeronautics and Space Administration are working on a machine learning model that can be used to predict the intensity of hurricanes across its life cycle [2].


Fortunately, scientists have completed thorough records of every hurricane that they have observed, and I can use one of these datasets to apply my machine learning model to. In order to determine with method to use, I referred to the scikit-learn algorithm cheat sheet [2]. I decided to apply both ridge regression, multi-layer perceptron regression, and logistic regression to the dataset.

I found that ridge regression and MLP regression did not accurately predict the hurricane category; the Regression Error Characteric (REC) curves for both the linear regression and the MLP regression converged at an accuracy less than 60%. However, when I used logistic regression to fit a model and then create a confusion matrix, I observed that this model was most successful in predicting category four hurricanes. From my results, I can conclude that machine learning can be very helpful in predicting the category of a hurricane based on the recorded measurents of the storm. 

## Data

For my project, I analyzed data collected by the National Oceanic and Atmospheric Administration. This dataset is on kaggle.com, and it includes various measurements of Atlantic Hurricanes that occured between 1975 and 2021. I chose to focus specifically on the dates, longitude and latitude, wind speed, pressure, and category of each storm. There are 19,066 rows in the dataset that provide information for 258 different hurricanes that occured over the 46 year timespan. 

When preprocessing the data, I removed the columns that I would not be using, and I replaced NA entries in the "category" column with the number 0. I wanted to look at the data for each individual hurricane, so I created a for loop


[](assets/IMG/datapenguin.png){: width="500" }

*Figure 1: Here is a caption for my diagram. This one shows a pengiun [1].*

## Modeling

Here are some more details about the machine learning approach, and why this was deemed appropriate for the dataset. 

The model might involve optimizing some quantity. You can include snippets of code if it is helpful to explain things.

```python
from sklearn.ensemble import ExtraTreesClassifier
from sklearn.datasets import make_classification
X, y = make_classification(n_features=4, random_state=0)
clf = ExtraTreesClassifier(n_estimators=100, random_state=0)
clf.fit(X, y)
clf.predict([[0, 0, 0, 0]])
```

This is how the method was developed.

## Results

Figure X shows... [description of Figure X].

## Discussion

From Figure X, one can see that... [interpretation of Figure X].

## Conclusion

Here is a brief summary. From this work, the following conclusions can be made:
* first conclusion
* second conclusion

Here is how this work could be developed further in a future project.

## References
[1] “A Machine-Learning Assist to Predicting Hurricane Intensity.” NASA, NASA, 20 Sept. 2023, www.nasa.gov/centers-and-facilities/jpl/a-machine-learning-assist-to-predicting-hurricane-intensity/. 

[2] “Choosing the Right Estimator.” Scikit, scikit-learn.org/stable/tutorial/machine_learning_map/index.html. Accessed 8 Dec. 2023. 

[3] Saffir-Simpson Hurricane Wind Scale, www.nhc.noaa.gov/aboutsshws.php. Accessed 8 Dec. 2023. 


[back](./)

