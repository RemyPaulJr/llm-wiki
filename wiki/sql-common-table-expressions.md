# SQL Common Table Expressions

**Summary**: Common Table Expressions (CTEs) are temporary result sets defined within a single SQL statement that improve code readability and maintainability by breaking complex logic into named steps.
**Tags**: #sql #query-writing #cte
**Created**: 2026-04-14

---

## Content

A Common Table Expression (CTE) is defined using the `WITH ... AS (...)` syntax. It allows you to name a temporary result set that you can then reference in your main `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.

### Benefits
- **Readability**: Breaks down complex nested queries into logical, named sections.
- **Maintainability**: Easier to debug and understand compared to nested subqueries.
- **Reusability**: Can be referenced multiple times within the same query.

### Syntax
```sql
WITH cte_name AS (
  -- Query that produces the temporary result set
  SELECT column1, column2
  FROM table
  WHERE condition
)
SELECT *
FROM cte_name
WHERE another_condition;
```

### Common Patterns
- **[[sql-two-step-aggregation|Two-Step Aggregation]]**: First aggregating data in a CTE and then performing a second aggregation on those results.
- **Hierarchical Queries**: Using recursive CTEs to traverse parent-child relationships (advanced topic).

## Related Notes
- [[sql-two-step-aggregation]]

## Sources
- `raw/transcripts/histogram-of-tweets.md`
