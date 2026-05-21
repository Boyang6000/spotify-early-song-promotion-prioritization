# Project II: Content-Based Early Song Promotion Prioritization

## Objective

Project II reframes the Spotify popularity task as a business prioritization problem. Music platforms and record labels often need to decide which new tracks deserve early recommendation, playlist, or promotional support before strong market feedback is available.

The goal is to build a content-based early promotion prioritization framework: rank tracks using information available near release time, then evaluate whether the top-ranked songs capture more true hits than a random promotion strategy.

## Baseline and Data

Project II keeps the Project I baseline as the reference point. It uses the Spotify track-level dataset with 113,999 cleaned observations and 20 original variables, including popularity, audio features, genre, duration, explicit indicator, artist, album, and track title.

The project evaluates:

- Regression: predict `popularity`.
- Classification: predict whether a track is a hit, defined using the training-set popularity threshold.
- Business ranking: measure how many true hits are captured in the top promoted fraction.

## Feature Engineering

Project II expands the original feature set with several groups of engineered predictors:

- Collaboration features: `num_artists` and `is_collab`.
- Duration features: `duration_min`, `duration_log`, and duration buckets.
- Audio interactions: `energy_loudness`, `danceability_energy`, and `valence_energy`.
- Genre-relative features: audio features compared against genre means.
- Title-level NLP features: VADER sentiment, title length, word count, collaboration wording, remix/version flags, love/number/exclamation indicators.
- PCA features: low-dimensional summaries of standardized audio variables.
- KMeans clusters: interpretable audio archetypes such as upbeat mainstream, acoustic emotional, and mid-profile blend.
- Last.fm artist signals: listener count, playcount, match flag, and play-per-listener features.

The notebook also includes a supplementary internal artist-prior model using artist-level historical averages. This model is treated as a benchmark or upper-bound signal rather than a fully deployable content-only model.

## Models

The project compares several model families:

- Project I baseline models.
- Content + NLP upgraded models.
- Content + NLP + Last.fm models.
- Supplementary artist-prior models.
- XGBoost robustness checks.

Random Forest models are central in the final comparison because they handle nonlinear relationships and mixed feature groups well.

## Key Results

The Project I Random Forest baseline performs well relative to simpler models, but Project II shows that additional features improve the promotion task.

Important reported results include:

- Baseline Random Forest regression: RMSE 15.44, MAE 10.45, R2 0.52.
- Content + NLP Random Forest regression: RMSE 15.08, MAE 10.42, R2 0.54.
- Content + NLP + Last.fm Random Forest regression: RMSE 13.03, MAE 8.42, R2 0.66.
- Content + NLP + Last.fm Random Forest classification: accuracy 0.882, F1 0.732, ROC-AUC 0.935.

For the business evaluation, the strongest main deployable model is the Content + NLP + Last.fm Random Forest classifier. In the top 10% promoted group, it captures 2,648 true hits with 92.9% precision and a lift of about 3.64 times compared with random selection.

The artist-prior supplement performs even higher in some metrics, but it depends on historical artist popularity from the same dataset and should be interpreted carefully because of deployment and leakage concerns.

## Interpretation

The main conclusion is that song content signals are useful, but artist-audience signals add substantial value. Audio features, engineered interactions, genre structure, title-level NLP, and Last.fm artist signals together create a more useful prioritization system than the Project I baseline.

Feature importance analysis shows that original Spotify audio features, engineered content features, Last.fm external artist features, genre/cluster features, NLP title features, and PCA components all contribute to the final model.

## Limitations and Future Work

Main limitations:

- The dataset is a static snapshot and lacks release-time dynamics.
- Popularity reflects past achievement rather than pure future potential.
- Last.fm history may be unavailable for new or cold-start artists.
- Internal artist-prior features are informative but not deployment-safe.
- One-hot genre representation is simple and may overfit.

Recommended future work includes time-series train/test splitting, early streaming and engagement signals, playlist-placement data, richer audio embeddings, and better multi-label or embedding-based genre representation.

