# STAT 5243 Spotify Projects

This repository collects two STAT 5243 projects about Spotify song popularity and early hit prediction.

## Repository Structure

- `notebooks/project1_spotify_hit_prediction.ipynb`: Project I code for Spotify chart data collection and baseline hit-prediction preparation.
- `notebooks/project2_content_based_promotion.ipynb`: Project II notebook for content-based early song promotion prioritization.
- `data/dataset.csv`: Spotify track-level dataset moved from the original dataset-only repository.
- `docs/project1.md`: Summary of Project I.
- `docs/project2.md`: Summary of Project II.
- `reports/project1/`: Project I presentation PDF.
- `reports/project2/`: Project II final report and presentation PDF.

## Projects

### Project I: Spotify Song Popularity Analysis and Hit Prediction

Project I frames the question "Will a song be popular?" as both a regression and classification problem. The work uses a public Spotify track-level dataset with 113,999 songs and 20 variables, including audio features such as danceability, energy, loudness, tempo, valence, acousticness, and speechiness.

The project includes exploratory analysis of popularity distribution, feature correlations, genre-level popularity differences, and baseline modeling. The main goal is to test whether Spotify audio and metadata features can partially predict popularity and identify likely hit songs.

Read more: [docs/project1.md](docs/project1.md)

### Project II: Content-Based Early Song Promotion Prioritization

Project II extends the baseline into a business-oriented ranking framework for early song promotion. Instead of only asking whether popularity can be predicted, it asks whether song-level content features can help platforms or labels prioritize a limited promotion budget.

The notebook adds engineered content features, title-level NLP features, PCA audio components, KMeans clusters, Last.fm external artist signals, and supplementary artist-prior benchmarks. The strongest deployable model in the final comparison is the Content + NLP + Last.fm Random Forest model, which improves both statistical performance and top-decile hit capture.

Read more: [docs/project2.md](docs/project2.md)

## Reproducibility Notes

The public notebook copies in this repository have been sanitized. API credentials are not committed. To rerun API-related cells, set the following environment variables:

```bash
SPOTIFY_CLIENT_ID=your_spotify_client_id
SPOTIFY_CLIENT_SECRET=your_spotify_client_secret
LASTFM_API_KEY=your_lastfm_api_key
```

The Project II notebook expects the Spotify dataset and, for the full Last.fm workflow, a cached Last.fm artist feature file. Some paths in the original notebooks were written for Google Colab and may need to be adjusted for a local environment.
