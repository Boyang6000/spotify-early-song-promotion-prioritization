# Project I: Spotify Song Popularity Analysis and Hit Prediction

## Objective

Project I studies whether Spotify song-level features can help predict song popularity and identify potential hit songs. The project is motivated by practical music-industry needs: platforms can use hit prediction for recommendation and playlist allocation, labels can use it to decide where to invest resources, and artists or producers can better understand what observable song characteristics relate to popularity.

## Data

The project uses a public Spotify track-level dataset accessed through Kaggle. Each row represents one song. The final dataset contains 113,999 observations and 20 variables.

Main variables include:

- Target: `popularity`, used as a proxy for song success.
- Classification target: a hit-song indicator derived from a popularity threshold.
- Audio predictors: `danceability`, `energy`, `loudness`, `tempo`, `valence`, `acousticness`, `speechiness`, `instrumentalness`, and `liveness`.
- Metadata predictors: duration, explicit indicator, and genre.

## Exploratory Analysis

The analysis first examines the distribution of popularity. Popularity is skewed: many songs have low popularity, while a smaller subset reaches high popularity. This supports the later decision to treat hit prediction as an imbalanced classification problem.

The project also explores feature correlations and genre-level differences. Popularity has weak linear correlation with most individual audio features, but some predictors are strongly related to each other, such as energy and loudness. Genre also matters: genres such as pop and metal show higher popularity ranges than several lower-performing genres.

## Modeling

Project I compares baseline models for two tasks:

- Regression: predict continuous Spotify popularity from 0 to 100.
- Classification: predict whether a song is a hit.

The modeling setup includes common interpretable and tree-based methods, including Ridge Regression, Logistic Regression, Decision Tree, and Random Forest models. The baseline uses Spotify audio features and metadata such as genre.

## Main Findings

Spotify audio and metadata features contain useful information, but they do not fully explain song popularity. Single audio variables are not enough on their own, while more flexible models can capture nonlinear relationships and interactions better than simple linear baselines.

The project concludes that song success can be partially predicted from Spotify features, but external factors such as artist popularity, marketing, playlist exposure, release timing, and social-media momentum are missing from the baseline dataset.

## Limitations and Next Steps

Main limitations:

- Spotify popularity is an imperfect proxy for true song success.
- The dataset is mostly static and lacks time-series dynamics.
- Audio features alone cannot capture market exposure, artist fanbase, playlist placement, or promotional activity.

Future improvements proposed in the project include adding API-based artist-level variables, time-based features, richer feature engineering, and extending the task toward ranking or recommendation.

