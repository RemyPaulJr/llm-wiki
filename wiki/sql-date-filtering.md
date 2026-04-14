# SQL Date Filtering

**Summary**: Techniques for filtering data based on date and time, including using `BETWEEN` and `EXTRACT` functions, while accounting for edge cases.
**Tags**: #sql #data-analysis #date-time
**Created**: 2026-04-14

---

## Content

### Using `BETWEEN`
The `BETWEEN` operator is inclusive of both boundary values. For date filtering, it is commonly used to select a specific range.

```sql
WHERE date_column BETWEEN '2022-01-01' AND '2022-12-31'
```

### ⚠️ Edge Cases with Timestamps
When filtering **timestamp** columns, using `BETWEEN` with a simple date string (like `'2022-12-31'`) might miss records that occurred later that same day (e.g., `2022-12-31 23:59:59`), as the date string may default to `00:00:00`.

### Using `EXTRACT`
A safer alternative for filtering by year or month is the `EXTRACT` function.

```sql
WHERE EXTRACT(YEAR FROM date_column) = 2022
```

### Common Functions
- `EXTRACT(YEAR FROM date)`
- `EXTRACT(MONTH FROM date)`
- `CURRENT_DATE`: Returns today's date.
- `NOW()`: Returns the current timestamp.

## Related Notes
- [[sql-two-step-aggregation]]

## Sources
- `raw/transcripts/histogram-of-tweets.md`
