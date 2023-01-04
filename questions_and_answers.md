# YouTube trending videos
## Questions and Answers
#### by arnabdey1996420@gmail.com


#### How many videos have trended for more than 5 days in the US?

````sql
SELECT country,
       Count(video_id) AS no_of_videos
FROM   (SELECT video_id,
               title,
               country,
               Count(trending_date) AS no_of_days_trended
        FROM   yt_trending_videos
        GROUP  BY video_id,
                  title,
                  country) a
WHERE  no_of_days_trended > 5
       AND country = 'US'
GROUP  BY country 
````

**Results:**

country|no_of_videos|
-------|------------|
US     |         388|

#### Which category has the highest average trending period?

````sql
SELECT snippettitle            AS category_title,
       Avg(no_of_days_trended) AS avg_trending_days
FROM   (SELECT video_id,
               title,
               snippettitle,
               Count(trending_date) AS no_of_days_trended
        FROM   yt_trending_videos a
               INNER JOIN yt_category_map b
                       ON a.category_id = b.id
        GROUP  BY video_id,
                  title,
                  snippettitle) a
GROUP  BY snippettitle
ORDER  BY avg_trending_days DESC 
````

**Results:**

category_title|avg_trending_days|
--------------|-----------------|
Music         |             7.37|

#### How many distinct videos trended from the category ‘Music’ on weekdays (Monday - Friday)?

````sql
SELECT snippettitle,
 Count(DISTINCT video_id) AS no_of_videos
FROM   yt_trending_videos a
       INNER JOIN yt_category_map b
               ON a.category_id = b.id
WHERE  Weekday(trending_date) BETWEEN 0 AND 4
       AND snippettitle = 'Music'
GROUP  BY snippettitle 
````

**Results:**


snippettitle|no_of_videos|
------------|------------|
Music       |         299|

#### Normally it is believed if the video trends for more number of days, then the video views, likes and comments also is higher. We need to check whether this is true for all the videos.

#### What are the total views for category sports in ‘Canada’?

````sql
SELECT snippettitle AS category_title,
       country,
       Sum(total_views)  AS total_views,
       Sum(total_likes)  AS total_likes,
       Avg(no_of_days_trended) AS avg_trending_days
FROM   (SELECT video_id,
               title,
               snippettitle,
               country,
               Sum(views) AS total_views,
       	    Sum(likes) AS total_likes,
               Count(trending_date) AS no_of_days_trended
        FROM   yt_trending_videos a
               INNER JOIN yt_category_map b
                       ON a.category_id = b.id
        GROUP  BY video_id,
                  title,
                  snippettitle,
                  country ) c
WHERE  country = 'Canada'
       AND snippettitle = 'Sports'
GROUP  BY snippettitle,
          country
ORDER  BY country,
          avg_trending_days DESC 
````

**Results:**


category_title|country|total_views|total_likes|avg_trending_days|
--------------|-------|-----------|-----------|-----------------|
Sports        | Canada| 33,007,445|  1,069,155|             1.29|

#### Which country has the highest number of videos with rank for views and rank of likes both in top 20?

````sql
SELECT country,
       Count(video_id) AS no_of_videos
FROM   (SELECT video_id,
               title,
               country,
               views,
               likes,
               Rank()
                 OVER (
                   partition BY country
                   ORDER BY views DESC) AS rank_views,
               Rank()
                 OVER (
                   partition BY country
                   ORDER BY likes DESC) AS rank_likes
        FROM   yt_trending_videos) a
WHERE  rank_views <= 20
       AND rank_likes <= 20
GROUP  BY country
ORDER  BY no_of_videos DESC 
````

**Results:**


country         |no_of_videos|
----------------|------------|
Great Britain   |          14|


#### We have determined that the Likes to dislikes ratio is a good indicator of popularity. We have to come up with a rating framework to the videos based on the available metrics, which would help us recommend videos better.

#### What is the average rating of the category Music?

````sql
SELECT category_title,
       Avg(rating) AS avg_rating
FROM   (SELECT c.*,
               Round(( ( views - min_views ) * 100 ) / ( max_views - min_views )
               , 0) AS
                      rating
        FROM   (SELECT DISTINCT video_id,
                                title,
                                snippettitle                  AS category_title,
                                views,
                                Max(views)
                                  OVER (
                                    partition BY category_id) AS max_views,
                                Min(views)
                                  OVER (
                                    partition BY category_id) AS min_views
                FROM   yt_trending_videos a
                       INNER JOIN yt_category_map b
                               ON a.category_id = b.id) c) d
GROUP  BY category_title 
````

**Results:**

category_title     |avg_rating|
-------------------|----------|
Film & Animation   |      6.87|









