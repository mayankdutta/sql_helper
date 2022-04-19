# sql_helper

#### Distinct + Even

```sql
select distinct city 
from station 
where (station.id % 2 = 0);
```

```sql
SELECT DISTINCT CITY FROM STATION WHERE MOD(ID,2)=0;
```

#### `IN` allows to check for the items _in a list._

#### `BETWEEN` allows range checking (range specified is inclusive of boundary values)

```sql
SELECT name, area FROM world
  WHERE area BETWEEN 250000 AND 300000
```
