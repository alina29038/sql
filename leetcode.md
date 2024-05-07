# 1907

```sql
select 'Low Salary' category, count(*) as accounts_count from Accounts where income < 20000
union
select 'Average Salary' category, count(*) as  accounts_count from Accounts where income between 20000 and 50000
union
select 'High Salary' category, count(*) as accounts_count from Accounts where income > 50000 
```

# 185

```sql
select Department, Employee, Salary from (
    select d.name as Department, e.name as Employee, e.salary as Salary,
    DENSE_RANK() OVER(partition by d.name order by e.salary desc) as rank
    from Employee e
    join Department d on d.id = e.departmentId
)
where rank in (1,2,3)
```
# 176

```sql
select (
    select salary as SecondHighestSalary
    from Employee
    ORDER BY 1
    limit 1
    offset 1
)
```

# 550

```sql
with _first as (
    select player_id, min(event_date) event_date 
    from activity 
    group by player_id
)
select round((count (1) * 1.0) / (select count (distinct player_id) from activity), 2) fraction
from _first f 
join activity a on f.player_id = a.player_id
where a.event_date = f.event_date + interval '1' day;
```
