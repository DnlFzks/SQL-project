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
where no_of_games = 29
````
