## MUST-HAVE SQL Queries

* Running Totals

```sql
SELECT id, month
        , Amount
        , SUM (Amount) OVER (ORDER BY id) as total_sum
FROM table_name
```

* Common Table Expression

```sql
WITH tempdata as (
    SELECT id as id
    FROM some_table
    WHERE (1 = 1) /*some condition*/
)
SELECT *
FROM table_name1
WHERE id in (SELECT id from tempdata)
```

* Ranking the Data

```sql
SELECT id,
       Amount,
       RANK() OVER (ORDER BY Amount desc)
FROM table_name
```

```sql
SELECT id,
       Amount,
       DENSE_RANK() OVER (ORDER BY Amount desc)
FROM table_name
```

* Adding Subtotals
*

```sql
SELECT Type,
       id,
       SUM(Amount) AS total_amount
FROM table_name
GROUP BY Type, id WITH ROLLUP
```

* Temporary Functions
*

```sql
CREATE
TEMPORARY FUNCTION get_gender(type varchar) AS (
   CASE WHEN type = "M" THEN "male"
        WHEN type = "F" THEN "female"
        ELSE "N/A"
   END
)

SELECT name,
       get_gender(Type) as gender
FROM table_name
```

### ROWS versus default RANGE in analytic window clause
* If you are doing analytic on the entire partition (or entire result set), then skip the window clause ( it means "do not write ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING"):
```sql
sum(sal) over (
   partition by deptno
)
```

* But once you have an ORDER BY, do not rely on default window clause, but rather explicitly write either ROWS or RANGE BETWEEN:
```sql
sum(sal) over (
   partition by deptno
   order by empno
   rows between unbounded preceding and current row
)
```
* (!) Analytic functions that only support the order-by clause and not a windowing clause - like for example ROW_NUMBER() - are of course exceptions from this rule of thumb. 
But if a function supports both order-by clause and windowing clause, then do not write an order-by clause without adding the windowing clause.
```sql
select s.*
     , sum(sal) over (
          partition by deptno
          order by empno
          rows between unbounded preceding and current row
       ) sum_sal_2
  from (
   select deptno
        , empno
        , ename
        , sal
        , sum(sal) over (
             partition by deptno
             order by empno
             rows between unbounded preceding and current row
          ) sum_sal
     from scott.emp
       ) s
 where sum_sal > 5000
 order by deptno
        , empno
/

```
