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
#### Import required libraries.
#### Define the working directory and load the movies.csv dataset.
    #### import os
         import pandas as pd
         os.chdir("C:\\Users\\Ramakrishna Kadali\\Documents\\rudra\\")
         movies_data = pd.read_csv("movies.csv")

#### 2. Data Preprocessing:
#### Define selected_features as the list of columns relevant to the movie's content.
#### Check for missing values and replace them with empty strings.
     #### selected_features = ['genres', 'keywords', 'tagline', 'cast', 'director']
          for feature in selected_features:
              movies_data[feature] = movies_data[feature].fillna('')

#### 3. Combining Features:
#### Concatenate the selected_features columns into a single string per row to create a combined_features column, which will represent the textual content for each movie.
     #### combined_features = movies_data['genres'] + ' ' + movies_data['keywords'] + ' ' + movies_data['tagline'] + ' ' + movies_data['cast'] + ' ' + movies_data['director']

#### 4. Feature Extraction Using TF-IDF:
#### Use TfidfVectorizer to convert combined_features into a matrix of TF-IDF features.
     #### from sklearn.feature_extraction.text import TfidfVectorizer
          vectorizer = TfidfVectorizer()
          feature_vectors = vectorizer.fit_transform(combined_features)

#### 5. Similarity Calculation:
#### Compute cosine similarity between the feature vectors of all movies.
     #### from sklearn.metrics.pairwise import cosine_similarity
          similarity = cosine_similarity(feature_vectors)

#### 6. Popularity Plot:
#### Define a function to plot the top 10 movies based on popularity using a horizontal bar chart.
     #### import matplotlib.pyplot as plt
          def plot():
              popularity = movies_data.sort_values("popularity", ascending=False)
              plt.figure(figsize=(12, 6))
              plt.barh(popularity["genres"].head(10), popularity["popularity"].head(10), align="center", color="skyblue")
              plt.gca().invert_yaxis()
              plt.title("Top 10 Movies by Popularity")
              plt.xlabel("Popularity")
              plt.show()
          plot()

#### 7. Movie Recommendation:
#### Prompt the user for a movie name, find the closest match, and generate a list of recommended movies based on similarity scores.
#### Display the top 30 most similar movies to the user.
     #### import difflib
          movie_name = input('Enter your favourite movie name: ')
          list_of_all_titles = movies_data['title'].tolist()
          find_close_match = difflib.get_close_matches(movie_name, list_of_all_titles)
          close_match = find_close_match[0]
          index_of_the_movie = movies_data[movies_data.title == close_match]['index'].values[0]
          similarity_score = list(enumerate(similarity[index_of_the_movie]))
          sorted_similar_movies = sorted(similarity_score, key=lambda x: x[1], reverse=True)

          print('Movies suggested for you:\n')
          i = 1
          for movie in sorted_similar_movies:
              index = movie[0]
              title_from_index = movies_data[movies_data.index == index]['title'].values[0]
              if i < 30:
                 print(i, '.', title_from_index)
                 i += 1

# Summary
This content-based recommendation system leverages cosine similarity on TF-IDF vectors derived from movie features. By inputting a movie title, users receive a ranked list of similar movies based on selected textual features.
