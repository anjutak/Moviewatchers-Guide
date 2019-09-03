
# Movie watchers assignment.
The assignment reads three datasets - movies.dat, ratings.dat, users.dat - from the MovieLens dataset. The python code generates different reports based on Movie Ratings.

# Generated metrics.
## Top 20 movies list.
First, merge the three datasets - movies, users, ratings - into one dataset called “combine” and select all the records where movie rating is 5. The records are grouping on “MovieID” and count the number of users who rated 5 per movie. Then the records are sorted in descending order based on the number of users count and select the first 20 movies. 

movie_review_5 = ratings[ratings["Rating"] == 5]
movies_ratings_5 = pd.merge(movies, movie_review_5, on = "MovieID")
movies_ratings_5_groupby = movies_ratings_5.groupby(["MovieID", "Title", "Genres", "Rating"], as_index=False)["UserID"].count()
movies_ratings_5_groupby.rename(columns={"UserID":"User_Count"}, inplace=True)
movies_ratings_5_sort_df = movies_ratings_5_groupby.sort_values(["User_Count"], ascending=False)
movies_ratings_5_reindex_df = movies_ratings_5_sort_df.reset_index(drop=True)
movies_ratings_5_reindex_df.to_csv("Ratings_5_movies_records.csv")


top_20_movies = movies_ratings_5_reindex_df.head(20)
top_20_movies.to_csv("top_20_movies.csv")


The graph for the top 20 movies is below.

![]

## The number of ratings on each rating.
First, create a new DataFrame with two columns - Rating, Number of ratings. From the combine DataFrame, select the records for each rating and count the number of ratings by using a For loop. The values for rating and number of ratings are inserted into the new DataFrame. 


df = pd.DataFrame(columns=["Rating", "Number of ratings"])
index = 0
for i in range(1,6):
    rating = combine[combine["Rating"]==i].count()[0]
    print(rating)
    df.loc[index, ["Rating"]] = i
    df.loc[index, ["Number of ratings"]] = rating
    index+= 1
df.to_csv("rating_with_number_of_ratings.csv")

The data in the visual form is below.



## The number of ratings on MovieID.
From the combine DataFrame, the records are grouping on “MovieID” and count the number of rating records. 

movieid_rating = combine.groupby(["MovieID"])["Rating"].count()
movieid_rating.to_frame().to_csv("movieid_rating.csv")























The graph for the number of ratings on MovieID is below.

![Screenshot%202019-09-03%20at%2011.45.10.png](attachment:Screenshot%202019-09-03%20at%2011.45.10.png)







The number of ratings by UserID.
From the combine DataFrame, the records are grouping on “UserID” and count the number of rating records. 

# Number of ratings by UserID.
userid_rating = combine.groupby(["UserID"])["Rating"].count()
userid_rating.to_frame().to_csv("userid_rating.csv")

The graph for the number of ratings by UserID is below.



Dataset
https://grouplens.org/datasets/movielens/1m/ 
Author
Anjuta Khongbantabam

References
http://rpubs.com/Jango/486734



```python

```
