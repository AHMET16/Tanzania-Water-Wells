# Tanzania-Water-Wells




Authors: Ahmet Karaoglan

Tanzania is a developing country that struggles to get clean water to its population of 59 million people. According to WHO, 1 in 6 people in Tanzania lack access to safe drinking water and 29 million don't have access to improved sanitation. The focus of this project is to build a classification model to predict the functionality of waterpoints in Tanzania given data provided by Taarifa and the Tanzanian Ministry of Water. The model was built from a dataset containing information about the source of water and status of the waterpoint (functional, functional but needs repairs, and non functional) using an iterative approach and can be found here. The dataset contains 60,000 waterpoints in Tanzania and the following features will be used in our final model:

amount_tsh - Total static head (amount water available to waterpoint)
gps_height - Altitude of the well
installer - Organization that installed the well
longitude - GPS coordinate
latitude - GPS coordinate
basin - Geographic water basin
region - Geographic location
population - Population around the well
recorded_by - Group entering this row of data
construction_year - Year the waterpoint was constructed
extraction_type_class - The kind of extraction the waterpoint uses
management - How the waterpoint is managed
payment_type - What the water costs
water_quality - The quality of the water
quantity - The quantity of water
source_type - The source of the water
waterpoint_type - The kind of waterpoint
The first sections focus on investigating, cleaning, wrangling, and reducing dimensionality for modeling. The next section contains 6 different classification models and evaluation of each, ultimately leading to us to select our best model for predicting waterpoint status based on the precision of the functional wells in the model. Finally, I will make recommendations to the Tanzanian Government and provide insight on predicting the status of waterpoints.

Business Problem
The Tanzanian government has a severe water crisis on their hands as a result of the vast number of non functional wells and they have asked for help. They want to be able to predict the statuses of which pumps are functional, functional but need repair, and non functional in order to improve their maintenance operations and ensure that it's residents have access to safe drinking water. The data has been collected by and is provided by Taarifa and the Tanzanian Ministry of Water with the hope that the information provided by each waterpoint can aid understanding in which waterpoints will fail. I have partnered with the Tanzanian government to build a classification model to predict the status of the waterpoints using the dataset provided. I will use the precision of the functional wells as my main metric for model selection, as a non functional well being predicted as a functional well would be more detrimental to their case, but I will provide and discuss several metrics for each model.

## Data Understanding


The dataset used for this analysis can be found here. It contains a wealth of information about waterpoints in Tanzania and the status of their operation. The target variable has 3 different options for it's status:

functional - the waterpoint is operational and there are no repairs needed
functional needs repair - the waterpoint is operational, but needs repairs
non functional - the waterpoint is not operational



![function_dist](https://user-images.githubusercontent.com/5207341/185799948-b32d3a6f-ff28-4cf5-a19e-31db2b37bcc5.jpeg)





We have the most functional wells at ~29,000, followed by non functional wells at ~21,000, and the minority class, functional needs repair at ~3,500.



## Modeling


1-Logistic Regression


<img width="715" alt="Screen Shot 2022-08-21 at 12 02 28 PM" src="https://user-images.githubusercontent.com/5207341/185800081-cb83b073-afb3-4327-9cb5-1665c0bfe889.png">
Our logistic regression model is improved to 75% accuracy over the dummy model. This model struggled to predict wells that were functional but needed repairs, likely due to class imbalances. The precision of the functional class is 73%.



2-K Nearest Neighbors Model


<img width="641" alt="Screen Shot 2022-08-21 at 12 05 03 PM" src="https://user-images.githubusercontent.com/5207341/185800230-4c4d586e-9a68-4468-bb9a-638dff8ce978.png">
The K Nearest Neighbors model outperformed the Logistic Regression model. Number of neighbors was hypertuned by running and GridSearch and optimal parameters were put into our pipe. Our K Nearest Neighbors model is not overfitting as the accuracy of training and test sets are 80.23% and 76.03%, respectively. The precision of the functional class is 77%, which is a huge improvement from our Logistic Regression model at 73%.

3- Decision Tree Model


<img width="728" alt="Screen Shot 2022-08-21 at 12 08 00 PM" src="https://user-images.githubusercontent.com/5207341/185800331-b5aced5c-c18e-4030-9c18-b6eb6d126d4f.png">



4- Random Forests

<img width="660" alt="Screen Shot 2022-08-21 at 12 27 43 PM" src="https://user-images.githubusercontent.com/5207341/185801165-3a4e6eb4-e3ee-4bdb-9f4b-11d0e4efb3c9.png">


5- XG Boost

<img width="631" alt="Screen Shot 2022-08-21 at 12 30 49 PM" src="https://user-images.githubusercontent.com/5207341/185801263-69a4a789-1bef-407d-aea5-39f1abd1341d.png">


Our best performing model ended up being the XG Boost model with tuned hyperparameters, although the random forests model was not far behind with 80% precision for the functional wells class. The model has overfitted the training data with a training accuracy of 92.57% and test accuracy at 81.73%, but this model boasted the highest precision score for the functional wells class at 81%.
Recommendations

## Location

Target repairs in areas like Lindi and Mtwara that have a high rateof non functional wells
Make repairs to functional wells in Kignma to maximize cost effectivess

## Repairs

Prioritize non functional and functional wells which need repair and have enough water

##Payment

Payment provides incentive and means to keep ells functional

## Installers

Avoid using installers with a high rate of pump failure

### Conclusions

Random Forests was our top performing model, although XG Boost was not far behind. The poor performance of the Logistic Regression , KNN, and Decision Tree indicate that the data is not easily separable. Our Random Forests model performs with an 87% testing accuracy and precision for the functional class at 86%.

Several of our models showed one of it's most important features to be quantity for the waterpoint. There are over 8,000 waterpoints that have enough water in them but are non functional. These are a high priority to address as well since there is water present. Wells with no fees are more likely to be non functional. Payment provides incentive and means to keep wells functional. The Government, District Council, and Fini Water all have a high rate of pump failure. Investigate why these installers have such a high rate of failure or use other installers.

