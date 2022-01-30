# Recommender system

There is no consulting project, since actual challenge is not in coding, but rather in setting up a recommender system.

Two most common recommender system types are...

- Content-based recommender system which recommend items based on the similariy to other items (its attributes).
- Collaborative-filtering recommender systems which use the "wisdom of the crowd" to recommend items. <- more often used because easier and often better results

`spark.ml` supports collaborative filtering. It...

- describes items as well as users by a set of latent factors (?).
- predicts missing entries of a user-item associtation matrix.
- learns thes latent factors using alternativ least squares (ALS) algorithm.
- needs data in a specific ALS format (this is the difficult part!)

ALS...

- is a matrix factorization approach
- decomposes larger user-item matrices into lower ones

The code along projects...

- uses a subset of the [movielens](https://grouplens.org/datasets/movielens/100k/) dataset with three columns:
  - userID
  - movieID
  - rating
- uses the ALS trainer, which...
  - takes in exactly these columns (user, item, rating)
  - predicts linear float ratings (may be outside [0,5] range)
- evaluates the predictions using a RegressionEvaluator (using RMSE metric)
