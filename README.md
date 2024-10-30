# Movie Recommendation System
This project is a content-based movie recommendation system built using Python. The system suggests movies based on the similarity of features such as genres, keywords, tagline, cast, and director of movies in the dataset. The cosine similarity metric is used to measure the similarity between movies.

## Prerequisites
Make sure the following libraries are installed:
#### -> numpy
#### -> pandas
#### -> scikit-learn
#### -> matplotlib
#### -> difflib
#### -> A dataset in .csv format (e.g., movies.csv), containing columns such as title, genres, keywords, tagline, cast, director, and popularity.

## Code Overview
#### 1. Data Loading and Initial Setup:
####    -> Import required libraries.
####    -> Define the working directory and load the movies.csv dataset.
    #### import os
         import pandas as pd
         os.chdir("C:\\Users\\Ramakrishna Kadali\\Documents\\rudra\\")
         movies_data = pd.read_csv("movies.csv")

#### 2. Data Preprocessing:
####    -> Define selected_features as the list of columns relevant to the movie's content.
####    -> Check for missing values and replace them with empty strings.
     #### selected_features = ['genres', 'keywords', 'tagline', 'cast', 'director']
          for feature in selected_features:
              movies_data[feature] = movies_data[feature].fillna('')

#### 3. Combining Features:
####    -> Concatenate the selected_features columns into a single string per row to create a combined_features column, which will represent the textual content for each 
movie.

