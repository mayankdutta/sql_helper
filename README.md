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
