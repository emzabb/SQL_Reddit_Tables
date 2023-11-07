# Project Description

## Introduction

In this project, I'll take on the role of a Data Analyst tasked with analyzing fictional data from Reddit, a popular social news aggregation and content rating platform. Reddit allows users to create posts containing various types of content, including text, media, and links to external websites. These posts are shared within specialized interest-based communities called "subreddits," each of which focuses on a particular topic or theme. Users engage with content by upvoting or downvoting it, resulting in a cumulative score for each post.

## Data Tables

For this task, I have access to three key data tables:

1. **Users Table:** This table contains information about the platform's users, including data such as usernames, user IDs, registration details, and potentially more user profile information.

2. **Posts Table:** The posts table provides data related to the posts created on Reddit, encompassing information about the posts themselves, such as content type, post IDs, creation dates, and interaction metrics like upvotes and downvotes.

3. **Subreddits Table:** This table offers insights into the subreddits, or communities, present on Reddit, including details about subreddit names, topics, and potentially metadata about each community.

## Project Tasks

My role as a Data Analyst will involve a series of tasks related to data exploration, analysis, and the generation of insights from this Reddit data. These tasks may include:

- **Data Cleaning:** Cleaning and preparing the data for analysis, addressing missing values, and handling data inconsistencies.

- **Exploratory Data Analysis (EDA):** Conducting EDA to understand the distribution of key variables, identifying trends or patterns in user behavior, post engagement, and subreddit popularity.

- **Data Visualization:** Creating data visualizations such as charts and graphs to present key findings in a visually appealing manner.

- **Descriptive Analysis:** Generating summary statistics and insights about user behavior, popular subreddits, or trends over time.

- **Hypothesis Testing:** Formulating and testing hypotheses to answer specific questions or explore relationships within the data.

- **Reporting and Presentation:** Preparing reports or presentations summarizing findings and recommendations, and effectively communicating these to relevant stakeholders.

## Project Goals

The primary goal of this project is to extract valuable insights from the provided data. These insights will help in understanding user interactions, subreddit preferences, or any other patterns that may be present in the Reddit community. The analysis conducted here will inform decision-making and potentially guide strategic actions within this fictional Reddit environment.

As I embark on this project, I'll ensure that I maintain a structured approach to data analysis, with well-documented work and clear presentation of findings to convey the story within the data.

### Here is my result:



  

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
    
      
    
    -- 5
    
    -- Join users and posts tables to find out how many posts each user has made.
    
    SELECT users.username, COUNT(*)  AS  'number_of_posts'
    
    FROM users
    
    LEFT  JOIN posts
    
    ON users.id = posts.user_id
    
    GROUP  BY users.id
    
    ORDER  BY  2  DESC;
    
      
    
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
    
      
    
    -- 9
    
    -- Write a query to calculate the average score of all the posts for each subreddit.
    
    SELECT subreddits.name,
    
    ROUND(AVG(posts.score), 2)  AS  'average_socre'
    
    FROM subreddits
    
    INNER  JOIN posts
    
    ON subreddits.id = posts.subreddit_id
    
    GROUP  BY  1
    
    ORDER  BY  2  DESC;

