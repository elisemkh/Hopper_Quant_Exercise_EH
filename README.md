# Hopper Quantitative Exercise

## Summary of Findings and Future Work
An F1 score of 94.6% and accuracy of 94.8% were achieved on the test data with a Random Forest Classifier when predicting between three recommendation categories: "Wait", "Wait or Buy", and "Buy". This accuracy was improved to 96.3% when reducing the categories to "Wait" or "Buy", but the F1 score went down to 91.4%. PCA was performed on the train data, but the accuracy went down when it was used to train the RF model. Future work could include improving the process of data preparation by experimenting with the numerical or categorical treatment of the dates in the features, and by experimenting with methods other than one hot encoding for the treatment of categorical variables. There are also ways to improve random forest algorithms, like using XGBoost.

More details can be found in the ipython notebooks.

## Methodology
The methodology is organized by ipython notebook.

### EDA, Label Creation, Data prep.ipynb

#### Data Exploration:
I performed exploratory data analysis (EDA) on the dataset to analyze the main characteristics of the dataset. I explored characteristics like search and departure dow, average fare vs. advance, and how the difference carriers differ in fare behavior.

#### Label Creation:
I created categorical labels to prepare the dataset for a classification algorithm. The labels were "Buy", "Buy or Wait" and "Wait". These were assigned according to if a lower price or the same price occurred for the same travels dates closer to the departure date. I visualized an example to confirm that the label creation makes logical sense.

#### Data Preparation:
I prepared the data by changing the categorical data into numerical data by one hot encoding. I also changed all the dates in the dataset (search date, departure date, return date) into two variables each- week number and day of week. I performed a 75%, 25% train/test split, and saved the files for use in the next notebook.

### PCA.ipynd

I chose to use Principle Component Analysis (PCA) because this dataset ended up having 52 components when all the categorical variables were encoded. PCA reduces the dimensionality of the data without eliminating too much of the variance of the dataset. 

#### Standardizing the Data:
I standardized the data using sklearn standard scaler in preparation for principal component analysis. 

#### Applying PCA:
I applied the PCA and then plotted the explained variance vs. the number of components. I found that the explained variance doesn't seem to get any higher after 35 components. I also calculated the number of components to retain 99%, 95%, and 90% explained variance. 

### RF Classifier.ipynd

#### Establishing a Baseline F1 score and Accuracy:
I established a baseline F1 score and accuracy by randomly picking labels from the train labels for the test labels. I did this because there is some class imbalance- the most common recommendation is "Wait", so I didn't want to randomly assign all three labels equally. The F1 score was 61.5% and the accuracy was 61.9%.

#### Training and Testing the model:
I trained the random forest model with 1000 trees first on the entire train features set. The F1 score and accuracy for the test set were 94.6% and 94.8% respectively. This is nearly a 33 point improvement over the baseline accuracy. I plotted a confusion matrix and explored the 15 most important features for the prediction. I also measured the accuracy of the test set if I combined the labels "Wait or Buy" and "Buy" into one label - "Buy". When I did this, my accuracy was improved to 96.3% and my F1 score dropped to 91.4%.

#### Training and Testing the model with the PCA data:
I trained and tested the model with 4 different PCA data sets- 52, 34, 29, and 25 components. These numbers of components represent all the features (52), and then retaining 99%, 95%, and 90% of the explained variance respectively. The F1 scores and accuracies went down significantly when I used any of the PCA data. This happens when the collinearity of the data helps the model. More explained variance of a model doesn't necessarily mean that there is more variance between the features with different labels.  
