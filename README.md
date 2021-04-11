# Movie ETL

## Overview of project

I’ve got 3 datasets:
-	movie data scrapped from Wikipedia in JSON file
-	The Kaggle dataset in CSV file with details about the movies from The Movie Database (TMDb) 
-	MovieLens dataset as CSV file of over 20 million reviews
The goal of project was to clean data, merge all three datasets together and upload final result to SQL database by using SQLAlchemy library in Python.

## Results

The Kaggle and MovieLens datasets were clean enough. I’ve made just few adjustments: changed data types and sorted movies to select only non-adult films.
However, Wikipedia data required a lot of work to be done. After importing JSON file to a dataframe, the dataframe had 193 columns. Most of them had similar data but with different column name or had only few values in a column.

I merged similar columns and got rid off columns with more than 90% NaN values. That reduced number of columns to 22.

The data about box office, budget, release date, running time had inconsistent format. Using regex I extracted values and converted them to appropriate data type (date or float).

![](https://github.com/angkohtenko/Movies-ETL/blob/main/Resources/release_date_origin.png)

![](https://github.com/angkohtenko/Movies-ETL/blob/main/Resources/release_date_clean.png)

After merging Kaggle and Wikipedia datasets I got redundant columns and had to decide whether delete columns or merge them. For numeric columns I used scatter plot to figure out how similar the columns are to each other and which of them has more missed data.

![](https://github.com/angkohtenko/Movies-ETL/blob/main/Resources/running_time_scatter.png)

![](https://github.com/angkohtenko/Movies-ETL/blob/main/Resources/competing_data_decisions.png)

Next, I transformed reviews data by creating a pivot dataframe to get the rating counts for each movie and merged it to the rest.

At the end, I’ve created connection to database and uploaded the merged dataset and ratings dataset to SQL database.
![](https://github.com/angkohtenko/Movies-ETL/blob/main/Resources/ratings_query.png)
