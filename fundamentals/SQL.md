# How to Write SQL?
## The Way
1. Correctness
2. Readability
3. Optimization

## Order of query execution

1. **FROM (and JOIN)**: limit the the search space here
2. **WHERE** : filter the data 
3. **GROUP BY** : Aggregates the data
4. **HAVING**: Filters data after aggregation
5. **SELECT**: grabs the columns and then deduplicates if DISTINCT is invoked
6. **UNION**: merges elected data
7. **ORDER BY**: sorts the results

## Tips

1. Get to know your Data
2. Minimise the data as much as possible
3. Use limit till you have finalised the query
4. Use **ON** (explicit, takes advantage of db index) to join table instead of **WHERE**
5. Use aliases to refer to tables to avoid ambiguity
6. Avoid fns in WHERE clause (the fn in run for every row) it prevent db from using an Index.
7. Avoid wildcards in the beginning of a string, it will lead to full table search.
   Ex: Avoid
   `SELECT column FROM table WHERE col LIKE "%wizar%"`
   Prefer
   `SELECT column FROM table WHERE col LIKE "wizar%"`
8. Prefer **EXISTS** to **IN**. EXISTS returns as soon as a value is found IN scans the whole table
9. SELECT columns, not stars
10. Prefer **UNION ALL** to **UNION** the first will not remove duplicates and will be faster
11. Avoid **SORTING** if possible as its expensive

## Index

If you are usually filtering by a column the it should probably be indexed (ex timestamp, main_event) 

### Partial Indexes

You can create index for a part of data using WHERE clause. Ex if you want to index only last weeks data.

### Composite Index

For the columns which typically go together

Ex: `CREATE INDEX full_name_index ON customers (last_name, first_name)`

### EXPLAIN

Some DBs support **EXPLAIN ANALYZE** which shows the execution of a query

Ex:

```sql
EXPLAIN ANALYZE SELECT title, release_year
FROM film
WHERE release_year > 2000;
```

Output:

```sql
Seq Scan on film  (cost=0.00..66.50 rows=1000 width=19) (actual time=0.008..0.311 rows=1000 loops=1)
  Filter: ((release_year)::integer > 2000)
Planning Time: 0.062 ms
Execution Time: 0.416 ms
```

## WITH

Use this to encapsulate Logic, like creating a View

```sql
ITH product_orders AS (
  SELECT o.created_at AS order_date,
          p.title AS product_title,
          (o.subtotal / o.quantity) AS revenue_per_unit
   FROM orders AS o
   LEFT JOIN products AS p ON o.product_id = p.id
   WHERE o.quantity > 0
)
SELECT product_title AS product,
       AVG(revenue_per_unit) AS avg_revenue_per_unit,
       MAX(revenue_per_unit) AS max_revenue_per_unit,
       MIN(revenue_per_unit) AS min_revenue_per_unit
FROM product_orders
WHERE order_date BETWEEN '2019-01-01' AND '2019-12-31'
GROUP BY product
ORDER BY avg_revenue_per_unit DESC
```

[Source](https://www.metabase.com/learn/building-analytics/sql-templates/sql-best-practices)

