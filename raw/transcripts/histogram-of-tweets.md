QL Study Notes — Histogram of Tweets

**Source:** DataLemur | Also Problem #6 in *Ace the Data Science Interview* (SQL Chapter)  
**Difficulty:** Easy  
**Topic:** Aggregation, CTEs, Histogramming

---

## Problem Summary

Given a table of tweet data, write a query that produces a **histogram** of tweets posted per user in 2022.

- **Bucket:** The number of tweets a user posted in 2022
- **Value:** The number of users who fall into that bucket

---

## Table Schema

**`tweets`**

| Column Name    | Type      |
|----------------|-----------|
| tweet_id       | integer   |
| user_id        | integer   |
| msg            | string    |
| tweet_date     | timestamp |

---

## Example

### Input

| tweet_id | user_id | msg                                                         | tweet_date          |
|----------|---------|-------------------------------------------------------------|---------------------|
| 214252   | 111     | Am considering taking Tesla private at $420. Funding secured. | 12/30/2021          |
| 739252   | 111     | Despite the constant negative press covfefe                 | 01/01/2022          |
| 846402   | 111     | Following @NickSinghTech on Twitter changed my life!        | 02/14/2022          |
| 241425   | 254     | If the salary is so competitive why won't you tell me...    | 03/01/2022          |
| 231574   | 148     | I no longer have a manager. I can't be managed              | 03/23/2022          |

### Output

| tweet_bucket | users_num |
|--------------|-----------|
| 1            | 2         |
| 2            | 1         |

### Explanation

- User `111` posted **2** tweets in 2022 → falls into bucket 2
- User `254` posted **1** tweet in 2022 → falls into bucket 1
- User `148` posted **1** tweet in 2022 → falls into bucket 1
- → 2 users in bucket 1, 1 user in bucket 2

---

## My Solution

```sql
WITH tweeter AS (
  SELECT
    user_id,
    COUNT(user_id) AS tweet_bucket
  FROM tweets
  WHERE tweet_date BETWEEN '01-01-2022' AND '12-31-2022'
  GROUP BY user_id
)
SELECT
  tweet_bucket,
  COUNT(*) AS users_num
FROM tweeter
GROUP BY tweet_bucket;
```

---

## Technique Breakdown

### 1. Two-Step Aggregation (The Core Pattern)
This problem requires **aggregating twice** — a very common interview pattern:

| Step | What it does |
|------|-------------|
| **Step 1 (CTE)** | Count tweets **per user** → produces one row per user with their tweet count |
| **Step 2 (outer query)** | Count users **per tweet count** → groups those results into histogram buckets |

> Think of it as: first summarize at the individual level, then summarize those summaries.

### 2. CTE (Common Table Expression)
Using `WITH ... AS (...)` breaks the logic into readable, named steps rather than nesting subqueries. This is preferred in interviews for clarity.

```sql
WITH tweeter AS (
  -- First aggregation: one row per user
  ...
)
-- Second aggregation: group those rows
SELECT ...
FROM tweeter
```

### 3. Date Filtering with `BETWEEN`
Filters to only 2022 tweets before grouping, which is critical — without this, the counts would include all years.

```sql
WHERE tweet_date BETWEEN '01-01-2022' AND '12-31-2022'
```

> ⚠️ **Watch out:** `BETWEEN` is **inclusive** on both ends. For timestamp columns, `'12-31-2022'` may miss tweets later in that day (e.g., `12-31-2022 23:59:59`). A safer alternative:
> ```sql
> WHERE EXTRACT(YEAR FROM tweet_date) = 2022
> ```

### 4. `COUNT(*)` vs `COUNT(column)`
- In the CTE: `COUNT(user_id)` counts non-null user_id values per group — works correctly here.
- In the outer query: `COUNT(*)` counts all rows in each bucket group — also correct.

---

## Key Takeaways for Interviews

- **Histogram = two-step aggregation.** When you see "group by the result of a group," reach for a CTE or subquery immediately.
- **CTEs improve readability** and make your thought process transparent to the interviewer.
- **Always filter before aggregating** when the problem is time-scoped.
- **Mind date edge cases** — timestamp columns and `BETWEEN` can have subtle boundary issues.
- This pattern (count of counts) appears in many forms: number of customers who placed exactly N orders, number of employees in each salary band, etc.

---

## Related Patterns to Review

- [ ] Count of counts (this problem)
- [ ] Running totals / window functions
- [ ] Percentile bucketing with `NTILE()`
- [ ] `CASE WHEN` for custom bucket ranges

---

*Documented for interview prep and reproducibility.*
