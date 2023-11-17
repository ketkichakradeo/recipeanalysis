# Recipe Analysis

**Authors**: Ketki Chakradeo (kchakradeo@ucsd.edu) and Kayanne Tran (kqtran@ucsd.edu)

---

## Project Overview

Food is a crucial aspect of human lives because it universally represents culture, family, and love. In this project, we chose to explore a dataset composed of various recipes with their ratings and reviews to uncover what factors contribute to an individual’s satisfaction and enjoyment for a meal.

Our dataset is a subset downloaded from [food.com](http://food.com), and it was originally scraped and used by the authors of [this](https://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19c.pdf) recommender systems paper. The data comes in two raw csv files: RAW_recipes.csv and RAW_interactions.csv. The former dataset contains recipe names, ingredients, nutritional facts, reviews, and more information regarding the recipes themselves, while the latter dataset contains user reviews and ratings for each recipe.


This is a data science project for UCSD's DSC80 class. In this project, we will first clean the data and explore the question of how the number of ingredients, number of steps, rating, and cooking time (in minutes) impact the overall success and user satisfaction of recipes. Then, we’ll assess the missingness of the columns and analyze any missingness dependencies. Finally, we will perform multiple permutation tests to evaluate if the average rating decreases due to time taken, number of steps, and number of ingredients. 

We categorize recipes with a duration exceeding the median value as 'longer' recipes, and 'more' steps are defined by a step count greater than the median within the respective column. Similarly, the definition of 'more' ingredients follows the same criterion based on quantities greater than the median in the corresponding column.

Understanding these dynamics has implications not only for the culinary world but also for fields such as nutrition, hospitality, and even artificial intelligence-driven recommendation systems. Through this exploration, we aim to contribute to a deeper comprehension of the multifaceted nature of human satisfaction and connection through the medium of food.

### Question Identification
We are exploring the following question: How does the number of ingredients, number of steps, rating, and cooking time (in minutes) impact the overall success and user satisfaction of recipes?

### Introduction to the Dataset
In our RAW_recipes.csv dataset, there are 83782 rows from 2008 to 2018, and 10 columns.

|Column	                 |Description|
|---                     |---        |
|`'name'	`            |Recipe name|
|`'id'`	                 |Recipe ID|
|`'minutes'`	         |Minutes to prepare recipe|
|`'contributor_id'`	     |User ID who submitted this recipe|
|`'submitted'`	         | Date recipe was submitted|
|`'tags'`	             |Food.com tags for recipe|
|`'nutrition'`	         |Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein    (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”|
|`'n_steps'`	         |Number of steps in recipe|
|`'steps'`	             |Text for recipe steps, in order|
|`'description'`	     | User-provided description|

The columns that are relevant to our study are: 

In the RAW_interactions.csv dataset, there are 731,927 rows and 5 columns.

|Column|Description|
|---|---|
|`'user_id'`	|User ID|
|`'recipe_id'`	|Recipe ID|
|`'date'`	|Date of interaction|
|`'rating'`	|Rating given|
|`'review'`	|Review text|

The columns that are relevant to our study are:

---

## Cleaning and EDA

### Data Cleaning
First we left-merged the two datasets on recipe ID and filled all ratings of 0 with np.nan. We chose to make this decision because it’s impossible to differentiate between genuine ratings of 0 and users who chose not to rate a recipe, so for simplicity and easier data handling, anything with a rating of 0 will be considered NaN. If we had decided to continue with 0 as a valid rating, it may have skewed any analysis or statistics involving the ratings. We also replaced all values of 0 in the minutes, n_steps, and n_ingredients columns with NaN, because it is not logical to have a value of 0 for those columns. 

Then we grouped the merged dataframe by recipe id to find average ratings for each recipe and added it as a new column.

For the minutes column, there were many values in the tens of thousands and it really skewed any box plot and histograms we were trying to make, so we created a new dataframe with the middle 50% of the minutes columns filtered out. The resulting df_filtered has 83782 rows and 6 columns. This was the dataframe we continued with and conducted all of our analysis on.


The relevant columns for our research question are avg_rating, minutes,  n_steps, and n_ingredients, so we did not need to process the other columns. Below is the head of our final cleaned dataframe. 



<iframe src="assets/10-80-enrollment.html" width=800 height=600 frameBorder=0></iframe>

---

### Univariate Analysis
To complete the univariate analysis, we removed the outliers from the dataset.

#### Distribution of Average Ratings
The following plot displays how many recipes recieved a certain rating. Based on the plot, we can see that majortiy of the recipes received a 5 star rating, as there is a singluar peak at the 5.0 rating mark. Additionally, the data is skewed left, indicating that majority of the recipes have a higher rating.

#### Distribution of Cooking Steps
The plot displays how many recipes have a certain number of steps. Based on the plot, we can see that there is a peak around 10 steps, and the graph is skewed right as most recipes tend to have 20 steps or less.

#### Distribution of Cooking Time
From the boxplot, we can see that the minutes column has a median of around 33 with the IQR laying in between about 0 and 110. The data is skewed right, indicating that most recipes have lower cooking times.

#### Distribution of Number of Ingredients
The histogram shows a slightly symmetric distribution. There is a peak around 7 or 8 ingredients, and a roughly equal amount of recipes with less than 7 ingredients and more than 7 ingredients.

---

### Bivariate Analysis

#### Number of Ingredients vs. Recipe Rating
When plotting the number of ingredients vs average rating, there is a slight positive trend, with higher density of points towards higher average ratings.

#### Number of Steps vs. Rating
There is a slightly positive trend. As the rating increases, the number of ingredients also is positively correlated.

---

### Interesting Aggregates
We were particularly interested in conducting a multidimensional analysis of this dataset to gain insights into the relationship between the number of ingredients, the number of steps, and their combined impact on the average rating of recipes. 

#### Recipe Count by Number of Ingredients and Number of Steps

From the pivot table, we can see that generally, recipes with more ingredients and more steps were more common.

#### Average Rating by Number of Ingredients and Number of Steps

We can see that recipes with less ingredients were more likely to have a higher rating. Majority of these recieps received a 5 star rating.

---

## Assessment of Missingness

### NMAR Analysis

---

### Missingness Dependency

---

## Hypothesis Testing
