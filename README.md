# Movie Recommendation System

A data mining project that builds a movie recommendation engine using merged IMDb and MovieLens-style movie metadata, ratings, popularity signals, keywords, and genre information. The project combines recommendation modeling, feature engineering, clustering, and visualization to explore how movie similarity and popularity can be used to generate better recommendations. The presentation shows the merged dataset contains about 63,633 movies and includes features such as ratings, votes, runtime, language, keywords, and worldwide gross. :contentReference[oaicite:0]{index=0}

## Project Overview

This project develops and compares multiple approaches for movie recommendation and movie grouping:

- a standard content-based recommendation engine using cosine similarity
- a hybrid recommendation engine that combines similarity with normalized popularity-adjusted ratings
- clustering methods to identify natural movie groupings and genre-based neighborhoods

The overall goal is to recommend movies that are not only similar in content and characteristics, but also strong choices in practice based on rating quality and popularity. The hybrid recommender was introduced because standard similarity alone sometimes surfaced weak results for movies with very low vote counts, as highlighted in the presentation appendix. :contentReference[oaicite:1]{index=1}

## Dataset

The project uses a merged movie dataset built from:

- an IMDb dataset containing top films by year with production information, worldwide gross, ratings, votes, and release dates
- a movie metadata dataset containing plot keywords

These datasets were merged on IMDb ID, resulting in **63,633 movies** after cleaning and matching. :contentReference[oaicite:2]{index=2}

## Features Used

The recommendation engine uses a combination of structured numeric, categorical, and text-derived features. According to the slides, the main features include: duration, rating, number of ratings, English vs. non-English language, keywords, genre, worldwide gross, normalized rating, and the difference between raw rating and normalized rating. :contentReference[oaicite:3]{index=3}

## Data Cleaning and Feature Engineering

Key preprocessing and feature engineering steps included:

- converting vote counts from string format (for example, `"6.5K"`) into integer form
- converting movie duration into minutes
- converting genres into dummy variables
- converting worldwide gross into U.S. dollars and adjusting for inflation to 2025
- removing non-predictive columns such as descriptions, writers, directors, stars, and other metadata fields
- filtering keywords to retain only those appearing in at least 100 movies
- filtering genres to retain more informative genre indicators
- creating a normalized score to account for the outsized effect of very small vote counts on average ratings

The slides report that keyword filtering reduced **17,338 unique keywords** to **135 retained keywords**, leaving **11,909 movies** for that part of the modeling pipeline. They also report filtering genres from **192 unique genres** down to **104**. :contentReference[oaicite:4]{index=4}

## Recommendation Methods

### 1. Standard Recommendation Engine

The standard recommender is a movie-based similarity engine:

- represent each movie using engineered feature vectors
- compute cosine similarity between movies
- retrieve the top 50 most similar movies
- sort by similarity score

This approach focuses on content and feature similarity only. :contentReference[oaicite:5]{index=5}

### 2. Hybrid Recommendation Engine

The hybrid recommender extends the standard approach by incorporating popularity-adjusted quality:

- compute movie-to-movie cosine similarity
- retrieve the top 50 most similar movies
- rescale recommendations using normalized rating
- rank movies by both similarity and adjusted quality

The slides describe this as multiplying similarity by normalized rating and dividing by 10 so that the recommender returns movies that are both similar and stronger overall recommendations. This design helps reduce the influence of niche titles with very few votes. :contentReference[oaicite:6]{index=6}

## Clustering Analysis

In addition to recommendation, the project explores unsupervised learning to identify movie groupings.

### Hierarchical Clustering

The clustering workflow used:

- normalized score
- log-transformed vote counts
- duration
- one-hot encoded genre indicators

Because the dataset contained many genre variables, PCA was applied before clustering to reduce dimensionality and noise. The slides report the use of:

- feature standardization
- PCA with 20 components
- agglomerative hierarchical clustering with Ward linkage
- dendrogram analysis for cluster structure interpretation :contentReference[oaicite:7]{index=7}

### t-SNE Visualization

The project also visualized movie neighborhoods using t-SNE. The presentation highlights example clusters such as:

- Animated
- Western
- Popular Blockbuster
- Drama
- Sci-Fi

A 25-cluster setting was used in the t-SNE map to balance broad categories and more specific subgenres. :contentReference[oaicite:8]{index=8}

### PCA / K-Means Exploration

The appendix also explores naive K-Means and PCA-based K-Means clustering. The results suggest that naive clustering without dimensionality reduction did not produce meaningful structure, while PCA-based clustering revealed some genre-based segments but still showed substantial overlap across cluster boundaries. :contentReference[oaicite:9]{index=9}

## Example Recommendation Results

The presentation includes example outputs showing that the recommender is able to return intuitive nearest-neighbor style recommendations.

Examples shown in the slides include recommendation sets around films such as:

- **Toy Story**
- **Zero Dark Thirty**
- **Toy Story 3**

Recommended titles included movies such as:

- Monsters, Inc.
- Coco
- Toy Story 2
- The Post
- Thirteen Days
- Argo
- Bridge of Spies

These examples suggest the model captures both family-animation similarity and political thriller / historical drama similarity reasonably well. :contentReference[oaicite:10]{index=10}

## Tech Stack

- Python
- Jupyter Notebook
- Pandas
- NumPy
- scikit-learn
- matplotlib / visualization libraries
