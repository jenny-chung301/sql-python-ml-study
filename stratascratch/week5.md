# Week 5 - Stratascratch SQL Problems

## Table of Contents

-   [10156 - Number Of Units Per Nationality](#question-1)
-   [10142 - No Order Customers](#question-2)
-   [10141 - Apple Product Counts](#question-3)
-   [Question 4](#question-4)
-   [Question 5](#question-5)
-   [Question 6](#question-6)
-   [Question 7](#question-7)
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
## Question 4

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

<a id="question-5"></a>
## Question 5

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

<a id="question-6"></a>
## Question 6

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

<a id="question-7"></a>
## Question 7

**Problem:**

**Solution:**

``` sql
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