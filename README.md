
# Movie Recommender System

## Overview
This Movie Recommender System provides movie recommendations based on the content of the movies. The system uses a content-based filtering approach to recommend movies by analyzing their metadata, such as genres, keywords, cast, and crew. The project leverages machine learning techniques like **Cosine Similarity** to measure the similarity between movies and generate recommendations.

## Dataset
The dataset used in this project is the **TMDb Movie Metadata** dataset, which contains information about 5,000 movies, including attributes like genres, keywords, cast, crew, and more. The dataset can be downloaded from Kaggle:

[TMDb Movie Metadata Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

## Project Workflow

1. **Data Collection**: 
   - The project uses two datasets: `tmdb_5000_movies.csv` (movie details) and `tmdb_5000_credits.csv` (cast and crew information).
   
2. **Data Preprocessing**:
   - The two datasets are merged based on the `title` column.
   - Missing values are handled by dropping rows with null values.
   - Columns like `genres`, `keywords`, `cast`, and `crew` are processed to extract relevant information (e.g., genre names, top 3 actors, director).
   - The `overview`, `genres`, `keywords`, `cast`, and `crew` columns are concatenated to create a new column, `tags`, which serves as the primary input for generating recommendations.

3. **Text Processing**:
   - The `tags` column is processed by converting text to lowercase, removing spaces, and applying stemming (using Porter Stemmer) to reduce words to their root form.

4. **Feature Extraction**:
   - **CountVectorizer** is used to transform the `tags` column into a vectorized format, representing the movies in a high-dimensional feature space.

5. **Similarity Calculation**:
   - **Cosine Similarity** is used to calculate the similarity between movies based on their vectorized representations (tags).

6. **Movie Recommendation**:
   - A function is implemented to recommend movies similar to a given movie title, based on the calculated cosine similarity.

7. **Saving the Model**:
   - The preprocessed data and similarity matrix are saved as pickle files for easy loading and reuse.

## Requirements

To run this project, you'll need the following libraries:

- numpy
- pandas
- matplotlib
- nltk
- scikit-learn
- ast
- pickle

You can install the required libraries using:

```
pip install numpy pandas matplotlib nltk scikit-learn
```

## How to Use

1. Download the dataset from Kaggle and place it in the `dataset/` directory.
2. Run the Python script to preprocess the data, create the movie similarity matrix, and save the necessary files.
3. Use the `recommender(movie_name)` function to get movie recommendations. Simply pass the movie title as a string to receive the top 5 similar movies.(Make sure to use the correct title, as the function is case-sensitive)

Example:

```python
recommender('The Avengers')
```

## Conclusion

The Movie Recommender System successfully uses content-based filtering to recommend similar movies based on their metadata. By using techniques like **Cosine Similarity** and **CountVectorizer**, the system provides effective recommendations that can help users discover new movies they may enjoy.
