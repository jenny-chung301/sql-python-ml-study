# Week 5 - Stratascratch SQL Problems

## Table of Contents

-   [10156 - Number Of Units Per Nationality](#question-1)
-   [10142 - No Order Customers](#question-2)
-   [10141 - Apple Product Counts](#question-3)
-   [2007 - Rank Variance Per Country](#question-4)
-   [10049 - Reviews of Categories](#question-5)
-   [10090 - Find the percentage of shipable orders](#question-6)
-   [10078 - Matching Similar Hosts and Guests](#question-7)
-   [Question 8](#question-8)
-   [Question 9](#question-9)
-   [Question 10](#question-10)

------------------------------------------------------------------------

<a id="question-1"></a>
## 10156 - Number Of Units Per Nationality

**Solution:**

``` python
# Import your libraries
import pandas as pd

# Start writing code
pd.merge(airbnb_hosts[airbnb_hosts["age"] <= 30],
         airbnb_units[airbnb_units["unit_type"]=="Apartment"],
         on="host_id").groupby("nationality")["unit_id"].nunique().reset_index(name="apartment_count").sort_values("apartment_count", ascending=False).head(1)
```

------------------------------------------------------------------------

<a id="question-2"></a>
## 10142 - No Order Customers

**Solution:**

``` python
# Import your libraries
import pandas as pd

# Start writing code
customers.loc[~customers["id"].isin(orders.loc[orders["order_date"].between("2019-02-01", "2019-03-01"), "cust_id"]), "first_name"]
```

------------------------------------------------------------------------

<a id="question-3"></a>
## 10141 - Apple Product Counts

**Solution:**

``` python
# Import your libraries
import pandas as pd

# Start writing code
merged = pd.merge(playbook_events, playbook_users, on="user_id")
merged = merged[["language", "device", "user_id"]].drop_duplicates()
merged["apple_user"] = merged["device"].isin(["macbook pro", "iphone 5s", "ipad air"]).astype(int)
merged.groupby("language").agg({"apple_user":"sum","user_id":"nunique"}).reset_index()

```

------------------------------------------------------------------------

<a id="question-4"></a>
## 2007 - Rank Variance Per Country

**Solution:**

``` python

import pandas as pd

fb_comments_count["ym"] = fb_comments_count["created_at"].dt.strftime("%Y-%m")
merged = pd.merge(fb_comments_count[fb_comments_count["ym"].isin(["2019-12", "2020-01"])],fb_active_users, on="user_id")
merged = merged.groupby(["country", "ym"])["number_of_comments"].sum().reset_index()
pivoted = merged.pivot(index="country", columns="ym", values="number_of_comments").reset_index().fillna(0)
pivoted["rank_2019"] = pivoted["2019-12"].rank(ascending=False, method = "dense")
pivoted["rank_2020"] = pivoted["2020-01"].rank(ascending=False, method = "dense")
pivoted.loc[pivoted["rank_2019"] > pivoted["rank_2020"], "country"]
```

------------------------------------------------------------------------

<a id="question-5"></a>
## 10049 - Reviews of Categories

**Solution:**

``` python

# Import your libraries
import pandas as pd

# Start writing code
yelp_business["category"] = yelp_business["categories"].str.split(";")
df = yelp_business.explode("category")
df.groupby("category")["review_count"].sum().reset_index(name="review_cnt")
```

------------------------------------------------------------------------

<a id="question-6"></a>
## 10090 - Find the percentage of shipable orders

**Solution:**

``` python
# Import your libraries
import pandas as pd

# Start writing code
merged = pd.merge(orders, customers, how="left", left_on="cust_id", right_on="id")
percent_shipable = (merged.assign(percent_shipable=lambda x:x["address"].notna())["percent_shipable"].mean()*100)
pd.DataFrame({"percent_shipable":[percent_shipable]})
```

------------------------------------------------------------------------

<a id="question-7"></a>
## 10078 - Matching Similar Hosts and Guests

**Solution:**

``` python
# Import your libraries
import pandas as pd

# Start writing code
pd.merge(airbnb_hosts, airbnb_guests,on=["gender", "nationality"])[["host_id", "guest_id"]].drop_duplicates()

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