# Week 5 - Stratascratch SQL Problems

## Table of Contents

-   [10156 - Number Of Units Per Nationality](#question-1)
-   [10142 - No Order Customers](#question-2)
-   [10141 - Apple Product Counts](#question-3)
-   [2007 - Rank Variance Per Country](#question-4)
-   [10547 - Actor Rating Difference Analysis](#question-5)
-   [10171 - Find the genre of the person with the most number of oscar winnings](#question-6)
-   [10548 - Top Actor Ratings by Genre](#question-7)
-   [Question 8](#question-8)
-   [Question 9](#question-9)
-   [Question 10](#question-10)

------------------------------------------------------------------------

<a id="question-1"></a>
## 10156 - Number Of Units Per Nationality

**Solution:**

``` sql
SELECT h.nationality
     , COUNT(DISTINCT u.unit_id) AS apartment_count
FROM airbnb_hosts h
JOIN airbnb_units u
ON h.host_id = u.host_id
WHERE h.age < 30
AND u.unit_type = 'Apartment'
GROUP BY h.nationality
ORDER BY apartment_count DESC
```

------------------------------------------------------------------------

<a id="question-2"></a>
## 10142 - No Order Customers

**Solution:**

``` sql
SELECT first_name
FROM customers
WHERE id NOT IN (SELECT cust_id
                 FROM orders
                 WHERE order_date BETWEEN '2019-02-01' AND '2019-03-01')
```

------------------------------------------------------------------------

<a id="question-3"></a>
## 10141 - Apple Product Counts

**Solution:**

``` sql
SELECT u.language
     , COUNT(DISTINCT CASE WHEN e.device IN ('macbook pro', 'iphone 5s', 'ipad air') THEN u.user_id ELSE NULL END) AS n_apple_user
     , COUNT(DISTINCT u.user_id) AS n_total_users
FROM playbook_events e
LEFT JOIN playbook_users u
ON e.user_id = u.user_id
GROUP BY u.language
ORDER BY n_total_users DESC
```

------------------------------------------------------------------------

<a id="question-4"></a>
## 2007 - Rank Variance Per Country

**Solution:**

``` sql

WITH monthly AS (
    SELECT u.country
         , DATE_FORMAT(c.created_at, '%Y-%m') AS ym
         , SUM(number_of_comments) AS total_comments
    FROM fb_comments_count c
    JOIN fb_active_users u
    ON c.user_id = u.user_id
    WHERE DATE_FORMAT(c.created_at, '%Y-%m') BETWEEN '2019-12' AND '2020-01'
    GROUP BY u.country, ym
)
SELECT t1.country
FROM (SELECT *
           , DENSE_RANK() OVER(ORDER BY total_comments DESC) AS rank_2019
        FROM monthly
        WHERE ym = '2019-12') t1
JOIN (SELECT *
           , DENSE_RANK() OVER(ORDER BY total_comments DESC) AS rank_2020
        FROM monthly
        WHERE ym = '2020-01') t2
ON t1.country = t2.country
WHERE t1.rank_2019 > t2.rank_2020
```

------------------------------------------------------------------------

<a id="question-5"></a>
## 10547 - Actor Rating Difference Analysis

**Solution:**

``` sql

WITH ranks AS (
    SELECT *
         , RANK() OVER(PARTITION BY actor_name ORDER BY release_date DESC) AS rk
         , COUNT(*) OVER(PARTITION BY actor_name) AS total_flim
    FROM actor_rating_shift
)
SELECT actor_name
     , AVG(CASE WHEN total_flim > 1 AND rk <> 1 THEN film_rating 
              WHEN total_flim = 1 THEN film_rating ELSE NULL END) AS avg_rating
    , SUM(CASE WHEN rk = 1 THEN film_rating ELSE NULL END) AS latest_rating
    , ROUND((SUM(CASE WHEN rk = 1 THEN film_rating ELSE NULL END)) - (AVG(CASE WHEN total_flim > 1 AND rk <> 1 THEN film_rating 
              WHEN total_flim = 1 THEN film_rating ELSE NULL END)), 2) AS rating_difference
FROM ranks
GROUP BY actor_name
```

------------------------------------------------------------------------

<a id="question-6"></a>
## 10171 - Find the genre of the person with the most number of oscar winnings

**Solution:**

``` sql

WITH winner AS (
    SELECT nominee
         , COUNT(*) OVER(PARTITION BY nominee) AS wins
    FROM oscar_nominees n
    WHERE winner = 1
)
SELECT i.top_genre
FROM winner w
JOIN nominee_information i
ON w.nominee = i.name
ORDER BY w.wins DESC
       , w.nominee
LIMIT 1

```

------------------------------------------------------------------------

<a id="question-7"></a>
## 10548 - Top Actor Ratings by Genre

**Solution:**

``` sql

WITH rating AS (
    SELECT actor_name
         , genre
         , COUNT(*) AS genre_cnt
         , AVG(movie_rating) AS avg_rating
         , DENSE_RANK() OVER(PARTITION BY actor_name ORDER BY COUNT(*) DESC, AVG(movie_rating) DESC) AS drank
    FROM top_actors_rating
    GROUP BY actor_name
           , genre
), ranks AS (
    SELECT actor_name
         , genre
         , avg_rating
         , DENSE_RANK() OVER(ORDER BY avg_rating DESC) AS actor_rank
    FROM rating
    WHERE drank = 1
)
SELECT *
FROM ranks
WHERE actor_rank <=3
ORDER BY actor_rank
       , genre


```

------------------------------------------------------------------------

<a id="question-8"></a>
## Question 8

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

<a id="question-9"></a>
## Question 9

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

<a id="question-10"></a>
## Question 10

**Problem:**

**Solution:**

``` sql
```