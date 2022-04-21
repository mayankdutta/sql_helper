# Select in select 

#### List each country name where the population is larger than that of 'Russia'.

```sql
select name from world 
where 
population > 
(select population from world where name = 'Russia');
```


### OR in Select in select

```sql
select name, continent from world 
where continent = 
(select continent from world where name = 'Argentina') 
or continent = 
(select continent from world where  name = 'Australia')
order by name;
```

OR 

```sql
select name , continent from world where continent in 
((select continent from world where name = 'Argentina'),(select continent from world where name = 'Australia')) 
order by name 
```


### Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
> Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.

```sql
select 
  name, 
  concat (
    round(
      population /(
        select 
          population 
        from 
          world 
        where 
          name = 'Germany'
      )* 100, 
      0
    ), 
    '%'
  ) as 'percentage' 
from 
  world 
where 
  continent = 'Europe';

```

OR 

```sql
select name , round((population/(select population from world where name = 'Germany'))*100) || '%' from world where continent = 'Europe'; 
```

### ALL 
> compare with all values in select query.

```sql
select name from world where gdp >
all(select gdp from world where continent = 'Europe' and gdp > 0);
```
