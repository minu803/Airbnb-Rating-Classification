# Big Data Project - Airbnb Rating Classification

![image](https://github.com/jinoh0731/Big-Data-Project-Airbnb-Rating-Classification/assets/111295393/bae7c7cf-2f16-4ba0-8781-1fdddfeac5be)



## Introduction and Problem Statement:
Airbnb, an online marketplace established in 2008, revolutionized lodging by allowing hosts to rent out unused space or entire homes. This platform offered a cost-effective and unique alternative to traditional hotels and B&Bs. One challenge guests face is determining the quality of a listing without any firsthand experience. This issue has given rise to a phenomenon known as social proof, where potential guests rely heavily on reviews from others to assess the desirability of a listing. New listings, however, suffer from a lack of reviews, creating a "cold start" problem where both Airbnb and prospective guests struggle to evaluate the quality of these properties.

Therefore, this project aims to explore the potential of Airbnb listings with zero reviews, which might be overlooked due to the absence of feedback, yet could be promising options for travelers. Our goal is to assess these properties' value and enhance their visibility to potential guests by categorizing each zero-review listing as ‘Poor’, ‘Average’, or ‘Great’. Through this classification, Airbnb can better recommend specific listings to different users, addressing the initial challenge of the cold start problem for new listings on the platform.

## File Folder Structure:
Most of our files are broken up based on the milestone goals accomplished that particular week:
- data_for_modeling : Folder contains our final dataset that we used in pySpark to create our transformations and use in our models.
- milestone1 : Contains notebooks on doing EDA for each of our regions: East, Central, and West along with an example joining calendar and listings-detailed tables.
- milestone2 : Contains notebooks on resolving misisng values, doing initial feature engineering, conducting EDA on the aggregate 15 cities, and applying the table joins.
- milestone3 : Contains notebooks on creating an intiial modeling pipeline via pySpark, creating our finalized feature engineering dataset, and conducting an initial attempt on decision tree & random forest models.
- milestone4 : Contains notebooks on all of our baseline & fine-tuned models for various number of features. The models we conducted in this project are decision tree, logisitic regression, and random forest. Our final predicted zero-review results from the random forest model are in this folder as a zipped up parquet file.

## Data Preprocessing
In preparing our dataset for exploratory data analysis, we implemented specific strategies to address missing data, ensuring robust statistical analysis and effective model training:

#### Property Features
For attributes like 'Bathrooms', 'Bedrooms', and 'Beds', we used related features for imputation:
- **Bathrooms**: Imputed based on 'Bedrooms' count or half the number of 'Beds' if 'Bedrooms' data was missing.
- **Beds**: Defaulted to the number of 'Bedrooms'.
- In cases where all data ('Bathrooms', 'Bedrooms', 'Beds') were missing, we initially set values to zero, subject to further evaluation.

#### Host Features
We maintained data consistency and avoided speculation in missing host-related information:
- **Host Since**: Filled missing dates with the most recent date in our dataset.
- **Host Location**: Imputed as 'unknown' if missing.
- Boolean fields such as 'Host_is_superhost' and 'Host_identity_verified' were defaulted to 'false'.
- **Host Listings Count**: Assumed a single listing in the absence of data.
- **Host Verifications**: Categorized missing entries as 'None'.

#### Review Scores
Handling of 'Review_scores_value' was particularly nuanced:
- Absence of scores due to no reviews was documented, especially for newly listed properties.
- Entries missing 'Review_scores_value' despite having reviews were excluded due to limited data impacting quality assessment.

These approaches preserve the integrity and utility of our dataset, supporting detailed exploratory data analysis and machine learning outcomes.
## Exploratory Data Analysis
To conduct our Exploratory Data Analysis (EDA), we first divided our data into three distinct regions to conduct regional-specific EDA before doing EDA on all 15 cities at once. We decided to take this approach to get a granular understanding of whether there were specific regional differences in our datasets before aggregating all 15 of our cities together. 
For regional EDA, we have created three Python notebooks, each housed within the 'milestone1' folder. These notebooks facilitate a comprehensive examination of our entire dataset on a regional level, including identifying missing values, analyzing data types, assessing the general range of each column, and compiling essential statistics such as mean, median, and standard deviation.
Plots that we created within our region-specific notebooks can be grouped into the following broad categories:
- Price
- Reviews
- Geojson file to render each city’s geographic area
- General property listing information like availability, amenities, host sign-ups, and room type.

For the aggregate 15 cities, EDA can be found in our ‘milestone2’ folder on our Github repository. Plots that we created within our aggregate 15 cities EDA can be grouped into the following broad categories:
- Amenities
- Reviews
- Individual property features such as bedrooms and num_bath features
- Host related information


## Feature Engineering
In the feature engineering phase, we initially processed the 'Amenities' field by converting a list of amenities into a numerical 'num_amenities' count, enhancing the data's usability for machine learning applications in Spark. We also introduced 'Essential_amenities', scoring listings based on the presence of critical amenities like WiFi and air conditioning, to better reflect guest expectations. Additionally, we standardized descriptions of bathrooms into a 'Num_baths' feature and uniquely identified locations by merging neighborhood names with city names to correct ambiguities. Our dataset also included features like 'Full_time_host', categorizing hosts with 10 or more listings as full-time, and 'Host_verification', which was transformed into a concise encoded format to fit Spark’s requirements, thus enriching our data for more precise analysis.

## Target
Our primary goal in refining the ```review_scores_value``` field was to improve analytical clarity and enhance the model's predictive accuracy regarding the quality of Airbnb listings. Initially featuring continuous numeric values ranging from 0 to 5, this field was transformed into categorical variables with specific thresholds to better serve our analysis needs:

- **Poor**: Listings with scores from 0 to 4.
- **Average**: Listings scoring between 4 and 4.8.
- **Great**: Listings with scores from 4.8 to 5.
  
These categories were established with thoughtful consideration of Airbnb's criteria for awarding the 'Super Host' badge, which includes a rating threshold of 4.8 or higher, alongside other performance indicators like low cancellation rates and high response rates.



## Modeling
Our modeling phase tackled a multi-class classification problem using three different algorithms: Random Forest, Decision Tree, and Multinomial Logistic Regression, chosen for their suitability to handle the dataset's complexity and feature interactions. We constructed a comprehensive Spark ML pipeline, which included feature transformations like StringIndexer and VectorAssembler, to prepare the data for modeling. Initial models started with 18 features; however, computational limitations led us to optimize our feature set to 13, enhancing model performance and manageability. We employed hyperparameter tuning and feature importance analysis to refine the models further. Each model variant was rigorously tested, and their performance was quantified using standard metrics like accuracy and the confusion matrix.

## Conclusion
The project culminated in the selection of the Random Forest model as the most effective, achieving an accuracy of 60.01%. This model significantly aids Airbnb by predicting potential listing categories, particularly beneficial for new listings without user reviews. While the model demonstrates robust predictive power, it faces challenges like computational demands and limited training data diversity, which could affect its applicability to different regions or underrepresented property types. Despite these challenges, the model’s insights are invaluable for hosts to optimize listings and for customers to make informed decisions on properties without reviews. Future work will focus on expanding the model's training dataset and exploring more sophisticated algorithms to improve prediction accuracy and reduce bias in classifications.
























## Contact:
If you have any questions or issues, please feel free to reach out to Ji Noh, Minwoo Sohn, and Tiffany Lee:
- **Ji Noh**
  - Email: eun.ji.noh@Vanderbilt.Edu
  - GitHub: jinoh0731
- **Minwoo Sohn**
  - Email: minwoo.sohn@Vanderbilt.Edu
  - GitHub: minu803
- **Tiffany Lee**
  - Email: Tiffany.Lee@vanderbilt.edu
  - GitHub: Math1019
