# Movie Recommendation System using Item-Based Collaborative Filtering

## Overview

This project implements an item-based collaborative filtering recommender system using the MovieLens dataset. The system identifies similar movies based on user ratings and generates personalized movie recommendations.

Two similarity measures were compared:

- Cosine Similarity
- Pearson Correlation

The performance of both methods was evaluated using RMSE and MAE.

---

## Dataset

Source: MovieLens Dataset

Files used:

- ratings.csv
- movies.csv

Dataset statistics:

| Metric | Value |
|----------|----------|
| Users | 610 |
| Movies | 9,742 |
| Ratings | 100,836 |
| Rating Scale | 0.5 - 5.0 |

---

## Data Preprocessing

To reduce sparsity and improve recommendation quality:

- Movies with fewer than 10 ratings were removed.
- Users with fewer than 10 ratings were removed.

After filtering:

| Metric | Value |
|----------|----------|
| Users | 610 |
| Movies | 2,269 |
| Ratings | 81,116 |
| Sparsity | 94.14% |

A user-item utility matrix was then created where:

- Rows represent users.
- Columns represent movies.
- Cell values represent ratings.
- Missing values indicate unrated movies.

---

## Methodology

### 1. Utility Matrix Construction

The ratings data was transformed into a user-movie matrix:

```
Users × Movies
```

This matrix forms the basis for item-item similarity calculations.

### 2. Similarity Computation

Two similarity measures were implemented:

#### Cosine Similarity

Measures the angle between movie rating vectors.

Characteristics:

- Range: 0 to 1
- Works well with sparse data
- Often favors popular co-rated movies

#### Pearson Correlation

Measures similarity in rating patterns.

Characteristics:

- Range: -1 to 1
- Focuses on rating behaviour
- Uses only overlapping ratings

### 3. Similar Movie Retrieval

For a selected movie, the system identifies the most similar movies using the computed similarity matrices.

### 4. Rating Prediction

Predicted ratings are calculated using a weighted average of ratings from similar movies:

```
Predicted Rating = Σ(Similarity × Rating)
                   ----------------------
                      Σ|Similarity|
```

### 5. Recommendation Generation

For each user:

1. Identify unrated movies.
2. Predict ratings.
3. Rank movies by predicted rating.
4. Return the top recommendations.

---

## Example: Similar Movies to Toy Story (1995)

### Cosine Similarity

- Toy Story 2 (1999)
- Jurassic Park (1993)
- Independence Day (1996)
- Star Wars: Episode IV (1977)
- Forrest Gump (1994)

### Pearson Correlation

- Toy Story 2 (1999)
- Brave (2012)
- The Incredibles (2004)
- Finding Nemo (2003)
- Aladdin (1992)

Observation:

- Cosine similarity tended to recommend highly popular movies.
- Pearson correlation identified movies with similar audience preferences.

---

## Personalized Recommendations

A demonstration user with 1,634 ratings was selected.

### Cosine Similarity Recommendations

- Psycho (1960)
- 12 Angry Men (1957)
- The Shining (1980)
- The Third Man (1949)
- Life Is Beautiful (1997)

### Pearson Correlation Recommendations

- Persepolis (2007)
- All Quiet on the Western Front (1930)
- Jean de Florette (1986)
- The 400 Blows (1959)
- Wild Tales (2014)

Observation:

The two methods produced completely different recommendation lists, highlighting the impact of the chosen similarity measure.

---

## Evaluation

Prediction accuracy was evaluated using a sample of 200 known ratings.

### Metrics

#### RMSE (Root Mean Squared Error)

Measures the average prediction error while penalizing large errors.

#### MAE (Mean Absolute Error)

Measures the average absolute prediction error.

### Results

| Similarity Measure | RMSE | MAE |
|-------------------|------|------|
| Cosine Similarity | 0.642 | 0.502 |
| Pearson Correlation | 0.502 | 0.386 |

### Interpretation

Lower values indicate better performance.

Pearson correlation achieved lower RMSE and MAE values, indicating more accurate rating predictions than cosine similarity.

---

## Key Findings

- The utility matrix remained highly sparse after filtering.
- Cosine and Pearson similarity produced different neighbourhood structures.
- Both methods identified Toy Story 2 as the closest neighbour to Toy Story.
- Pearson correlation generated recommendations that better reflected user preference patterns.
- Pearson correlation achieved the best prediction accuracy.
- Similarity measure selection significantly affects recommendation quality.

---

## Tools

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

---

## Author

**Hermela Seltanu Gizaw**
