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
