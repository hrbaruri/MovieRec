# Movie Recommender System

## Overview
This Movie Recommender System provides movie recommendations based on the content of the movies using a **content-based filtering** approach. It analyzes movie metadata such as the overview, genres, keywords, cast, and crew. 

The project initially used a basic bag-of-words model (`CountVectorizer`), but has now been significantly improved using a **pre-trained Sentence-BERT model** to extract **contextual semantic embeddings**. These embeddings allow the system to better understand the meaning behind movie descriptions, resulting in more accurate and meaningful recommendations.

## Dataset
The dataset used in this project is the **TMDb Movie Metadata** dataset, which contains information about 5,000 movies, including attributes like genres, keywords, cast, crew, and more. The dataset can be downloaded from Kaggle:

[TMDb Movie Metadata Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

## Project Workflow

1. **Data Collection**: 
   - The project uses two datasets: `tmdb_5000_movies.csv` (movie details) and `tmdb_5000_credits.csv` (cast and crew information).

2. **Data Preprocessing**:
   - The two datasets are merged based on the `title` column.
   - Missing values are dropped to ensure clean data.
   - The `genres`, `keywords`, `cast`, and `crew` columns are parsed to extract relevant information such as genre names, top 3 actors, and the director.
   - The `overview`, `genres`, `keywords`, `cast`, and `crew` are combined into a single column `tags`, which represents the core content of the movie.

3. **Feature Extraction**:
   - A **pre-trained Sentence-BERT model** (`all-MiniLM-L6-v2`) from the `sentence-transformers` library is used to convert the `tags` text into **dense semantic vectors**.
   - These vectors capture the meaning and context of the movie content beyond simple keyword overlap.

4. **Similarity Calculation**:
   - **Cosine Similarity** is applied to the Sentence-BERT embeddings to compute semantic similarity between movies.
   - This allows the system to recommend movies based on how contextually similar they are, rather than just shared words.

5. **Movie Recommendation**:
   - A function `recommend(movie_name)` returns the top 5 movies that are most similar to the input title based on the computed embeddings.
   - Recommendations are more meaningful and nuanced thanks to contextual embeddings.

6. **Saving the Model**:
   - The preprocessed movie data and similarity matrix are saved using `pickle`, allowing the system to be reused without reprocessing the entire dataset.

