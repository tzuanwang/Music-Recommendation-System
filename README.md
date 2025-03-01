# Music Recommendation System

## Introduction
* Purpose: Help user to discover new music that they will like
* Objectives: Build a system combining personalization (content-based) and trend detection (collaborative filtering)

## Data Source
* Data Source: Spotify Million Playlist Dataset & Spotify API
* Include playlist_id, playlist_name, track_id, album_name, etc.
* Pick 4000 out of 1000,000 playlists whose number of songs are less than 40 songs and create playlists.csv
* Use track_id for each song in the playlist to retrieve more information (audio features such as ‘Acousticness', 'Instrumentalness', 'Liveness', 'Valence', 'Tempo', etc.) through Spotify API and create tracks.csv

## Data Pre-Processing
* Use MinMaxScaler to transform the numeric audio features in the tracks dataset
* Playlists were split into train and test sets by 80% and 20%
* The recommendation system is trained on the playlists in the train set and recommend tracks that were not in the train set. We evaluate the model by comparing the results to the test set

## Approach
**Content-Based Filtering** - Focuses on track features to find tracks with similar characteristics. Recommend tracks similar to those the user already likes
* Build User Profile - Aggregate the features of tracks in the user's playlist to represent their preferences
* Compute Similarity - Use cosine similarity to compare the user profile with candidate tracks

**Collaborative Filtering** - Focuses on relationships between tracks based on their co-occurrence in playlists. Tracks frequently appearing together are likely to be recommended
* Co-Occurrence Analysis - Build a matrix showing how often pairs of tracks appear in the same playlist
* Score Computation - Assign higher scores to tracks that co-occur more often with the user’s playlist tracks

**Hybrid Method**
* Combination of content-based and collaborative filtering
* Recommends both familiar (content-based) and new (collaborative) tracks
* Hybrid Score = 𝜶 * Content Score + (1 - 𝜶 ) * Collaborative Score, 𝜶 is the weight parameter to control the balance

## Result and Evaluation
* For each test case, the system recommended the same number of tracks as those withheld in the test set, ensuring a fair comparison between predicted and actual preferences
* The best **𝜶** to control the balance of collaborative filtering and content-based filtering is **0.60**
* The system's recommendation accuracy shows positive correlation with playlist size, suggesting the model performs better for users with larger playlists
