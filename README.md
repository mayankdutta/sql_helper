# sql_helper

## General syntax 

```sql
SELECT attribute-list
   FROM table-name
   WHERE condition
```

### attribute-list
- This is usually a comma separated list of attributes (field names)
Ex- pressions involving these attributes may be used. The normal mathematical operators +, -, *, / may be used on numeric values. String values may be concatenated using ||
- To select all attributes use *
- The attributes in this case are: name, region, area, population and gdp

### table-name
- In these examples the table is always bbc.

### condition
- This is a boolean expression which each row must satisfy.
- Operators which may be used include AND, OR, NOT, >, >=, =, <, <=
- The LIKE operator permits strings to be compared using 'wild cards'. The symbols _ and % are used to represent a single character or a sequence of characters. Note that MS Access SQL uses ? and * instead of _ and % .
- The IN operator allows an item to be tested against a list of values.
- There is a BETWEEN operator for checking ranges.

<hr>

### Distinct + Even

```sql
select distinct city 
from station 
where (station.id % 2 = 0);
```

```sql
SELECT DISTINCT CITY FROM STATION WHERE MOD(ID,2)=0;
```

### `IN` allows to check for the items _in a list._

### `BETWEEN` allows range checking (range specified is inclusive of boundary values)

```sql
SELECT name, area FROM world
  WHERE area BETWEEN 250000 AND 300000
```

### The word LIKE permits pattern matching - % is the wildcard.
```sql
SELECT name FROM bbc
  WHERE name LIKE 'D%'
```

### XOR
```sql
select name, population, area from world 
where (area > 3000000 XOR population > 250000000); 
```

_Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area._

### Round.

> Round till 2 digits. <br>
> Population must be in millions. <br>
> GDP must be in billions. <br>

```sql
select name, round(population/1000000, 2), round(gdp/1000000000, 2) from world
where continent='South America';
```

#### Round upto nearest 1000

```sql
select name, round(gdp/population, -3) from world
where gdp >= 1000000000000;
```

> 3 is for the numbers after decimal <br>
> -3 is for the numbers before decimal <br>

### Length

```sql
SELECT name, LENGTH(name), continent, LENGTH(continent), capital, LENGTH(capital)
  FROM world
 WHERE name LIKE 'G%'
```
