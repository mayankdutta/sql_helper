# Select in select 

#### List each country name where the population is larger than that of 'Russia'.

```sql
select name from world 
where 
population > 
(select population from world where name = 'Russia');
```

