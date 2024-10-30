# Movie Recommendation System
This project is a content-based movie recommendation system built using Python. The system suggests movies based on the similarity of features such as genres, keywords, tagline, cast, and director of movies in the dataset. The cosine similarity metric is used to measure the similarity between movies.

### Prerequisites
Make sure the following libraries are installed:
#### -> numpy
#### -> pandas
#### -> scikit-learn
#### -> matplotlib
#### -> difflib
#### -> A dataset in .csv format (e.g., movies.csv), containing columns such as title, genres, keywords, tagline, cast, director, and popularity.

### Code Overview
#### 1. Data Loading and Initial Setup:
####    -> Import required libraries.
####    -> Define the working directory and load the movies.csv dataset.
    #### import os
         import pandas as pd
         os.chdir("C:\\Users\\Ramakrishna Kadali\\Documents\\rudra\\")
         movies_data = pd.read_csv("movies.csv")
