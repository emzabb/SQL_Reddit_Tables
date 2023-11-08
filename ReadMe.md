
# Project Description

## Introduction

In this project, I'll take on the role of a Data Analyst tasked with analyzing fictional data from Reddit, a popular social news aggregation and content rating platform. Reddit allows users to create posts containing various types of content, including text, media, and links to external websites. These posts are shared within specialized interest-based communities called "subreddits," each of which focuses on a particular topic or theme. Users engage with content by upvoting or downvoting it, resulting in a cumulative score for each post.

## Data Tables

For this task, I have access to three key data tables:

1. **Users Table:** id, username, email, join_date, score

2. **Posts Table:** id, title, user_id, subreddit_id, score, created_date

3. **Subreddits Table:** id, name, created_date, subscriber_count


## Project Goals

The primary goal of this project is to extract valuable insights from the provided data. These insights will help in understanding user interactions, subreddit preferences, or any other patterns that may be present in the Reddit community. 

As I embark on this project, I'll ensure that I maintain a structured approach to data analysis, with well-documented work and clear presentation of findings to convey the story within the data.

### My work:



  

    -- 1
    
    -- Let’s start by examining the three tables.
    
    SELECT *
    
    FROM users
    
    LIMIT  5;
    
      
    
    SELECT *
    
    FROM posts
    
    LIMIT  5;
    
      
    
    SELECT *
    
    FROM subreddits
    
    LIMIT  5;
    
### tables previews
![enter image description here](https://i.ibb.co/D4PsjcG/1.png)


    -- 2
    
    -- Identify primary keys in each table. Are there any foreign keys?
    
    SELECT id
    
    FROM users;
    
      
    
    SELECT id, user_id, subreddit_id
    
    FROM posts;
    
      
    
    SELECT id FROM subreddits;
    
      
    
    -- 3
    
    -- Write a query to count how many different subreddits there are.
    
    SELECT  COUNT(*)  AS  'subreddit_count'
    
    FROM subreddits;
### subreddit count
![enter image description here](https://i.ibb.co/L8ScyWy/subred-count.png)
    
      
    
    -- 4
    
    -- Write a few more queries to figure out the following information:
    
    -- What user has the highest score?
    
    -- What post has the highest score?
    
    -- What are the top 5 subreddits with the highest subscriber_count?
    
      
    
    SELECT id, username, MAX(score)  AS  'highest_score'
    
    FROM users;
    
      
    
    SELECT id, title, MAX(score)  AS  'highest_score'
    
    FROM posts;
    
      
    
    SELECT id, name, subscriber_count
    
    FROM subreddits
    
    ORDER  BY subscriber_count DESC
    
    LIMIT  5;
### results
![enter image description here](https://i.ibb.co/Gp2ZLzK/user-score-post-score-subred-subs.png)
    
      
    
    -- 5
    
    -- Join users and posts tables to find out how many posts each user has made.
    
    SELECT users.username, COUNT(*)  AS  'number_of_posts'
    
    FROM users
    
    LEFT  JOIN posts
    
    ON users.id = posts.user_id
    
    GROUP  BY users.id
    
    ORDER  BY  2  DESC;
### top 10 users w/ most posts
![enter image description here](https://i.ibb.co/vc2bfxg/users-most-posts.png)
    
      
    
    -- 6
    
    -- Over time, posts may be removed and users might delete their accounts.We only want to see existing posts where the users are still active.
    
    SELECT *
    
    FROM posts
    
    INNER  JOIN users
    
    ON posts.user_id = users.id;
    
      
    
    -- 7
    
    -- Some new posts have been added to Reddit! Stack the new posts2 table under the existing posts table to see them.
    
    SELECT *
    
    FROM posts
    
    UNION
    
    SELECT *
    
    FROM posts2;
    
      
    
    -- 8
    
    -- Find the most popular post in a subreddit (posts with a score of 5000 or more).
    
    WITH popular_posts AS  (
    
    SELECT *
    
    FROM posts
    
    WHERE score >= 5000
    
    )
    
    SELECT subreddits.name, popular_posts.title , popular_posts.score
    
    FROM subreddits
    
    INNER  JOIN popular_posts
    
    ON subreddits.id = popular_posts.subreddit_id
    
    GROUP  BY subreddits.name
    
    ORDER  BY popular_posts.score DESC;
### top 5 most popular posts
![enter image description here](https://i.ibb.co/KXHkHfw/highest-post-scores.png)
    
      
    
    -- 9
    
    -- Write a query to calculate the average score of all the posts for each subreddit.
    
    SELECT subreddits.name,
    
    ROUND(AVG(posts.score), 2)  AS  'average_socre'
    
    FROM subreddits
    
    INNER  JOIN posts
    
    ON subreddits.id = posts.subreddit_id
    
    GROUP  BY  1
    
    ORDER  BY  2  DESC;
### results
![enter image description here](https://i.ibb.co/dtzh7Wt/avg-score-subred.png)


In conclusion, this project has allowed for a deep dive into the world of Reddit, providing insights into user behavior, content engagement, and subreddit preferences.


