# Spotify_Hit_Prediction

A machine learning project to predict the popularity of songs on Spotify using audio features and artist-level insights.

## Overview

With millions of songs uploaded to Spotify, identifying which tracks will become hits is both a business priority and a data challenge. This project explores whether we can predict song popularity using metadata and audio attributes—helping platforms like Spotify enhance discoverability, boost engagement, and support emerging artists.

## Problem Statement

Promotional efforts in the music industry often rely on intuition, past trends, or marketing budgets rather than objective characteristics of the music itself. This results in missed opportunities to identify high-potential tracks early, especially for new or independent artists. Our project aims to develop a data-driven hit prediction model that evaluates both musical and artist-level factors to uncover what truly makes a song successful.

## Dataset

The dataset used in this project is publicly available on Kaggle:

**[Spotify Dataset (114k Songs)](https://www.kaggle.com/datasets/priyamchoksi/spotify-dataset-114k-songs)**  
Created by **Priyam Choksi**

The dataset contains **114,000 Spotify tracks** across **125 genres** with:
- Audio features (e.g., danceability, energy, valence, loudness, tempo)
- Metadata (e.g., artist, album, genre, explicit content)
- Popularity scores ranging from 0 to 100

## Preprocessing

To prepare the data for modeling, we performed the following steps:
- Filtered songs with popularity < 5 to remove outliers and noise.
- Applied log transformation to reduce skew in the popularity distribution.
- Segmented songs into **Hit (popularity ≥ 50)** and **Non-Hit (popularity < 50)** categories.
- For greater granularity, we used hierarchical clustering to further divide the Hit class into:
  - Moderate Hit  
  - Strong Hit  
  - Super Hit  
  - Blockbuster Hit  

## Modeling Approach

We explored two different approaches to predict song popularity:

### Method 1: Music-Only Features

Focused exclusively on audio-based attributes of each song to assess whether musical qualities alone can indicate hit potential—especially valuable for evaluating new or unknown artists.

### Method 2: Music + Artist-Level Insights

Incorporated additional engineered artist-level features such as:
- Average energy and danceability across an artist’s songs  
- Artist’s track count  
- Shrunk popularity score based on the artist’s historical success  

## Models Tried

We experimented with several models for both approaches:
- Random Forest  
- XGBoost  
- Logistic Regression  
- Support Vector Classifier (SVC)  

## Results

### Method 1 (Music-Only)

| Model               | Accuracy | Precision | Recall | F1 Score |
|--------------------|----------|-----------|--------|----------|
| Random Forest       | **81.4%** | **0.88**    | **0.56** | **0.65**   |
| XGBoost             | 70.5%    | 0.69      | 0.27   | 0.29     |
| Logistic Regression | 68.4%    | 0.19      | 0.20   | 0.16     |
| SVC                 | 68.5%    | 0.14      | 0.20   | 0.16     |

### Method 2 (Music + Artist-Level Insights)


| Model                                    | Accuracy | Precision | Recall | F1-Score | Blockbuster Hit Recall |
|------------------------------------------|----------|-----------|--------|----------|-------------------------|
| Random Forest (Permutation + Blockbuster Focus) | **0.90**   | **0.81**    | **0.79** | **0.80**   | **0.86**                  |
| Random Forest (GridSearchCV)            | 0.89     | 0.81      | 0.77   | 0.79     | 0.81                    |
| XGBoost                                  | 0.86     | 0.75      | 0.70   | 0.72     | 0.75                    |
| SVM                                      | 0.68     | 0.14      | 0.20   | 0.16     | 0.00                    |

## Key Takeaways

- Including artist-level insights significantly boosts predictive performance by adding valuable context to the song's success.
- Even with just musical features, the model performs well—highlighting how data-driven tools can support emerging or lesser-known artists without relying on reputation.
- Permutation-based feature selection helped balance overall accuracy with improved recall for high-stakes categories like Blockbuster Hits.
