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
> compare with all values in select query. <br> 
> We can use the word ALL to allow >= or > or < or <=to act over a list. For example, you can find the largest country in the world, by population with this query: <br> 
> You need the condition gdp > 0 in the sub-query as some countries have null for gdp. <br> 


```sql
select name from world where gdp >
all(select gdp from world where continent = 'Europe' and gdp > 0);
```


### synchronized query 

> The above example is known as a correlated or synchronized sub-query. <br> 

> Using correlated subqueries <br>
> A correlated subquery works like a nested loop: the subquery only has access to rows related to a single record at a time in the outer query. The technique relies on table aliases to identify two different uses of the same table, one in the outer query and the other in the subquery. <br>

> One way to interpret the line in the WHERE clause that references the two table is “… where the correlated values are the same”.

> In the example provided, you would say “select the country details from world where the population is greater than or equal to the population of all countries where the continent is the same”. <br>

```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND population>0)

```

#### question 2
> List each continent and the name of the country that comes first alphabetically.

```sql
select continent, name from world x 
where name <= all
(select name from world y
where x.continent = y.continent
); 
```


#### Question
> Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

```sql
SELECT NAME,
       continent
FROM   world x
WHERE  population >= ALL (SELECT 3 * population
                          FROM   world y
                          WHERE  x.continent = y.continent
                                 AND x.NAME <> y.NAME); 
```


#### Question 
> Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

```sql
SELECT NAME,
       continent,
       population
FROM   world z
WHERE  continent IN (SELECT DISTINCT( continent )
                     FROM   world x
                     WHERE  25000000 >= ALL (SELECT population
                                             FROM   world y
                                             WHERE  x.continent = y.continent)) 
```
