# Youtube_trending_videos_sql
SQL Project: YouTube Trending Videos

## Introduction
YouTube’s trending videos vary by location across the world. The impact of likes, dislikes, comments may differ based on the countries. The demographics of countries itself is a big factor in the way videos are consumed in various countries. The videos can be trending if video views are above a certain level. Your manager wants to present an analysis how average trending periods of videos vary across countries. How the likes, dislikes, comments impact the duration of trending videos. Your manager has also asked for some interesting insights from the data which could be done through exploratory data analysis.

* [Data Analysis Question & Answers](https://github.com/KopiteArnab/Youtube_trending_videos_sql/blob/400e1d35e4ac99b6cc741bf2b63d8c60fbbd4860/questions_and_answers.md)

## Datasets used
There are 3 tables available for the analysis
- [YT_trending_videos.csv](https://github.com/KopiteArnab/Youtube_trending_videos_sql/blob/359de9d5f813821b2a7b70bb70400c24807775b9/YT_trending_videos.csv):    YT_trending_videos: This table has video level information along with dates on which videos were trending along with metrics such as comments, likes, views, etc.
- [YT_channel_map.csv](https://github.com/KopiteArnab/Youtube_trending_videos_sql/blob/400e1d35e4ac99b6cc741bf2b63d8c60fbbd4860/YT_channel_map.csv):
YT_channel_map: This table has channel_id mapping with the channel title which is also interpreted as channel name
- [YT_category_map.csv](https://github.com/KopiteArnab/Youtube_trending_videos_sql/blob/d050acda7e27b27464e18d4178d8a9be7767910d/YT_category_map.csv):    YT_category_map: This table has category_id mapping. The videos on YouTube are mapped to a category based on the type of video such as Movie, trailer, animation, etc.

## Data Dictionary

YT_trending_videos
![sqlp1](https://user-images.githubusercontent.com/93368813/210611558-2e8a416a-bdd6-4c77-a01e-8ef9c2b5919b.png)
YT_channel_map
![sqlp2](https://user-images.githubusercontent.com/93368813/210611795-280cd92c-3a47-48db-b029-8f69d0b401db.png)
YT_category_map
![sqlp3](https://user-images.githubusercontent.com/93368813/210611875-aead0f56-1d93-4ea9-a78a-8307018e10a4.png)


## Entity Relationship Diagram
![alt text](https://github.com/KopiteArnab/Youtube_trending_videos_sql/blob/d050acda7e27b27464e18d4178d8a9be7767910d/ERD.jpg)
