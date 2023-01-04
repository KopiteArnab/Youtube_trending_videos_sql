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


