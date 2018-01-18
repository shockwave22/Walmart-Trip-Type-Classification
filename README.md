# Walmart-Trip-Type-Classification

[![N|Solid](https://kaggle2.blob.core.windows.net/competitions/kaggle/4654/media/walmart_triptypes640.png)]

Improve Walmart’s segmentation process by classifying the customer trip types based on the product purchased in that visit, so that it creates the best shopping experience for every customer.


# Dataset information!

  - Kaggle competition - https://www.kaggle.com/c/walmart-recruiting-trip-type-classification
  - Number of records - 647,054 with 38 trip types

# Challenges

  - Each record was representing an item instead of a visit. We grouped the records by their visit number to classify the trip.
  - Records with missing values - removed the records with NULL, Blank values
  - Dummy variables(Categorical) - Weekday; Converted qualitative values to quantitative. Eg: Monday =1, Tuesday =2.
  - Duplicate department labels. Eg: “MENSWEAR” and“MENS WEAR”.

# Inferences and assumptions

-  Trip Type Class 3 - Financial Services, impulse merchandise.
-  Trip Type Class 5 - Pharmacy, Personal care 
- Trip Type Class 36 - Personal care, beauty, pharmacy 
- Trip Type Class 37 - Produce,grocery dry,Meat, Dairy 
- Trip Type Class 38 - Dairy, bread, breakfast foods,grocery dry

# Approach
- Initial model were Decision Trees (40%), KNN(61%), Random forest(54.77%). Analysis produced low accuracies for all three models.
- We performed feature engineering.
- - Multidimensional data (several rows per customer visit).
- - From the data visualization, the trip type is more dependent on department description. Hence feature engineering from long to wide format.
- - From 7 dimensions to 71 dimensions.
- - Added individual departments as additional columns.
- - Aggregated total number of products bought on each visit.
- - Aggregated total number of products bought in each department on each visit.
- - Added a Return column representing product returns.
- - Dimensions of resulting data: 15195 x 71.

# Result after feature engineering

| Model | Training accuracy | Testing accuracy |
| ------ | ------ | ------ |
| Random Forest | 98% | 88% |
| KNN (k=5) | 89% | 86% |
| Linear Discriminant Analysis | 86% | 86% |
| Support Vector Machines | 90% | 89% |
| Logistic Regression | 91% | 90% |


# Fine tuning
- 71 features can be reduced and sparsity can be handled using fine tuning.
- PCA - Experimented with different number of components: 1, 5, 10, 25, 30,70, yielding the same accuracy for both train and test sets.
- Recursive Feature Elimination - Experimented ranking different number of features: 10, 20, 30, 40, 60 and found that models produced a very low testing and training accuracy - underfitting
- L1 Regularization - Performed Cross-Validated Logistic Regression to get best (C) lambda [1,1,74,15,1] for classes[3,5,36,37,38]. 
- This selected 63 important features for all classes.

# Conclusion
- Transforming the raw data into features influenced the accuracy of the model on unseen data.
- Feature engineering and L1 Regularization helped fine tune the Logistic Regression model. 
- PCA and Recursive Feature Selection failed to improve the selected models. 



