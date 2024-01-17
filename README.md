# SQL-project#1 - Olympics

### 1. What sport was played during all summper olympics?
````sql
with t1 as
	(select count(distinct games) as total_summer_games
	from athlete_events
	where season = 'summer'),
t2 as
	(select distinct sport, games
	from athlete_events
	where season = 'summer'),
t3 as
	(select sport, count(games) as no_of_games
	from t2
	group by sport)
select *
from t3
where no_of_games = 29;
````
### 2. Top 5 athletes with most gold medals won
````sql
<!--  used dense_rank so no rank number will be skipped
order by added at the end of the query, not within the CTE so it will run in SSMS -->

with t1 as
	(select name, count(1) as total_medals
	from athlete_events
	where medal = 'Gold'
	group by name),
t2 as
	(select *, dense_rank() over(order by total_medals desc) as rnk
	from t1)
select *
from t2
where rnk <= 5
order by total_medals desc;
````
