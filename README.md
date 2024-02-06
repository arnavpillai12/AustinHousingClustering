# Austin Houses K-Means Clustering Project
## Arnav Pillai


[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Note: This file contains the background, methodology, and insights from this project. The full annotated jupyter notebook file is found in the file titled "AustinHousingKMeansClustering.ipynb"
# 1. Executive Summary

- One of the most important attributes of houses from a consumer standpoint is house attributes, such as area and distance to schools in the area.
-   This project uses data from Austin area houses in 2021 to  create the best cluster solution to cluster Austin houses based on characteristics that consumers can care about.
- By understanding the differences between house attributes, houses can be more effectively marketed and split up

# 2. Data Overview
- Data was downloaded from Kaggle and originally was made by aggregating data from Zillow of 2021 Austin area homes for sale by Eric Pierce (https://www.kaggle.com/datasets/ericpierce/austinhousingprices/versions/2)
- Data contains useful information about Austin area houses, including but not limited to:  zip code, property tax rate, year built, average distance to school (in miles), average school ratings in the area average distance to school, lot size (in square feet), living area size (in square feet), average school size in area, number of house price changes, and latest house price changes.
- Original dataset used contains data on 15,171 Austin area houses
# 3. Exploratory Data Analysis
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/boxplot.png">
  </body>
</html>

- The numeric variables in the data were explored using a boxplot as shown above in order to briefly examine the medians and outliers of all the variables
- Due to the wide range of values and numbers of outliers in both living area and lot area, the box plot was not a great visual representation of this data, so further analysis using histograms was used.
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/Lvingarea.png">
  </body>
</html>
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/lotareabefore.png">
  </body>
</html>

- As shown in histograms above, the data of living area square feet is skewed right and the distribution of lot size is very skewed with many more outliers affecting the shape of distribution.
- In order to do K-means clustering without losing too much essential data, it is necessary to investigate and treat outliers in lot size effectively without losing too much data, so that k-means clustering can be performed using these variables as these are 2 of the most important attributes of the Austin housing data.
# 4. Outlier Treatment: Lot Size
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/lotsizeafter.png">
  </body>
</html>

- First outliers were investigated using the Interquartile range, and there were a lot of outliers found using this method (9% of the data) which would be too much useful data that could potentially remove.
- A histogram comparison approach was determined to be a better approach where one distribution contained values above 100,000 square feet removed and another contained values above 1 acre (43560 square feet) removed.
- The number of outliers in both approaches were measured
- Overall, both distributions still had outliers but resembled a better shape than the original, and removing values greater than 100,000 kept 98.98% of original Austin house data

# 5. Variable Selection for CLustering
- The variables selected for clustering were: Lot Area (In Square Feet), Living Area (In Square Feet), and average distance to schools, as only a few variables could be selected for a more interpretable clustering approach.
- Lot Area and Living Area made the most sense as these are the most important characteristics of a house, as buyers care deeply about Area.
- Average distance to schools was determined to be the 3rd and final variable used in this analysis, because typically houses are purchased by families, so it would make sense to assess some characteristic about the house that is related to schools in the area.

# 6. Methods: Train-test and VAF
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/VAF.png">
  </body>
</html>

- Randomly split data in to 70-30 ratio train and test set, so that k-means clustering variables of relevance can be tested on the test set and compared with the train set to see if they match.
- Generated a solution which tested performance of 2-12 K-means clusters using 150 random starts for each number of clusters to deal with the problem of local optima.
- Given that this is an unsupervised learning method and no standard performance metrics compared to supervised learning methods, the best approach to measure model performance was determined to be: Variance accounted for.
- At each number of clusters, variance-accounted for was calculated and plotted as shown above.

# 7. Methods: Determining Best Number of Clusters
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/Scree%20plot.png">
  </body>
</html>

- A scree plot was used to determine the best number of clusters from the solution which tested 2-12 clusters
- Given that the elbow (turning point of curve) of the graph shown above is at 4 clusters, this is the ideal number of clusters.

# 8. Comparisons between Metrics of Train and Test
**Train:**
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/Train%20data.png">
  </body>
</html>

**Test:**
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/test%20data%20new.png">
  </body>
</html>

- As seen above,the test and training set VAF are almost identical and the respective proportions of the size of each cluster are approximately similar in each.
- The centroids/means which are the defining attributes of each cluster are extremely close across all means and their respective ranks in each column are mostly the same with exception of average school distance in the test set
- Overall, the train/test comparison shows that a random split of the data still shows similar clusters being formed, which gives greater confidence in using this cluster model for the population of  Austin area houses

# 9. Business Insights and Recommendations
<html>
  <body>
    <img src="https://github.com/amp123code/Pictures/blob/main/Austin%20House%20Data%20Clusters.png">
  </body>
</html>

**Insights:**
- Since the 4 cluster model for Austin, TX area houses (shown above) was chosen, above is the table representation of the 4 clusters in terms of its 4 variables and centers to represent important characteristics that consumers will care about in buying houses.
- The model had an overall Variance accounted for of approximately 64 % and showed very similar means and Variance accounted for when using the test set.
- The model is very interpretable and is likely representative of Austin housing data
  
**Cautions:**
- Very large lot size outliers were removed from model, so this missing data could create additional clusters, but given the small % they make of houses, it is likely that they don’t make a big percentage of Austin houses on market.
- Another caution is this data is in 2021 and the Austin housing market is constantly changing in terms of available houses, Maybe houses available have gotten smaller due to land constraints.
- Model will probably need to be updated periodically to reflect new housing market data.
- Use this cluster model as a starting point to fit new data.

**Recommendations:**
- Using the clusters shown above, cluster Austin houses on the market in to the 4 clusters based on the characteristics and means
- Assign houses to cluster based on overall closeness to the means to find the best fit for a house
- Because this cluster model segments houses, advertise each cluster of houses differently based on characteristics and determine appropriate pricing to maximize house sales.
- Ultimately, breaking up the Austin area houses in to clusters based on select important characteristics is an important way to group houses in the Austin area market, and can help to determine each segment of houses and strategies to sell different types of houses.

  







