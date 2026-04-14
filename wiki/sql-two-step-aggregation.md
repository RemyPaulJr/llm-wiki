# SQL Two-Step Aggregation

**Summary**: A common SQL pattern used to "summarize summaries," typically implemented with a CTE or subquery to aggregate data at one level and then aggregate those results again.
**Tags**: #sql #aggregation #data-analysis
**Created**: 2026-04-14

---

## Content

Two-step aggregation is a core pattern in SQL for answering "count of counts" questions, such as creating histograms or finding the number of customers who placed a specific number of orders.

### The Pattern
The logic is broken into two distinct steps:
1.  **First Aggregation**: Summarize data at the individual or granular level (e.g., count items per user).
2.  **Second Aggregation**: Summarize the results of the first step (e.g., count users per item count).

### Implementation with CTEs
Using a [[sql-common-table-expressions|Common Table Expression (CTE)]] is the preferred method for this pattern as it improves readability and makes the logic transparent.

```sql
WITH first_agg AS (
  SELECT
    user_id,
    COUNT(item_id) AS item_bucket
  FROM table
  GROUP BY user_id
)
SELECT
  item_bucket,
  COUNT(*) AS value_num
FROM first_agg
GROUP BY item_bucket;
```

### Use Cases
- **Histograms**: Counting how many users fall into specific activity buckets (e.g., [[histogram-of-tweets]]).
- **Order Frequency**: Number of customers who placed exactly N orders.
- **Salary Bands**: Number of employees within specific salary ranges.

## Related Notes
- [[sql-common-table-expressions]]
- [[sql-date-filtering]]

## Sources
- `raw/transcripts/histogram-of-tweets.md`
