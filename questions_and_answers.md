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
        GROUP  BYvideo_id,
                  title,
                  country) a
WHERE  no_of_days_trended > 5
       AND country = 'US'
GROUP  BY country 
````
