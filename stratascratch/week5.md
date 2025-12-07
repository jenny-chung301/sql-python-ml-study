# Week 5 - Stratascratch SQL Problems

## Table of Contents

-   [10156 - Number Of Units Per Nationality](#question-1)
-   [Question 2](#question-2)
-   [Question 3](#question-3)
-   [Question 4](#question-4)
-   [Question 5](#question-5)
-   [Question 6](#question-6)
-   [Question 7](#question-7)
-   [Question 8](#question-8)
-   [Question 9](#question-9)
-   [Question 10](#question-10)

------------------------------------------------------------------------

## 10156 - Number Of Units Per Nationality {#question-1}

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

## Question 2 {#question-2}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 3 {#question-3}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 4 {#question-4}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 5 {#question-5}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 6 {#question-6}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 7 {#question-7}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 8 {#question-8}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 9 {#question-9}

**Problem:**

**Solution:**

``` sql
```

------------------------------------------------------------------------

## Question 10 {#question-10}

**Problem:**

**Solution:**

``` sql
```