# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
<!-- Copy solution here -->
SELECT * FROM matches where season = 2017;

```

2) Find all the matches featuring Barcelona.

```sql
<!-- Copy solution here -->
SELECT * FROM matches where hometeam = 'Barcelona' OR awayteam = 'Barcelona';

```

3) What are the names of the Scottish divisions included?

```sql
<!-- Copy solution here -->
SELECT * FROM divisions where code LIKE 'SC%' ;

```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql


SELECT * FROM divisions WHERE name = 'Bundesliga';

SELECT * FROM matches WHERE division_code = 'D1' AND hometeam = 'Freiburg' OR awayteam = 'Freiburg';
```

5) Find the teams which include the word "City" in their name. 

```sql

SELECT team
FROM (
    SELECT hometeam AS team FROM matches
    UNION
    SELECT awayteam AS team FROM matches)AS all_teams 
    WHERE team LIKE '%City%';
```

6) How many different teams have played in matches recorded in a French division?

```sql

SELECT COUNT(DISTINCT team) AS total_teams
FROM (
    SELECT hometeam AS team FROM matches Where division_code LIKE 'F%') AS all_teams;

```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql

SELECT COUNT(*) AS match_count
FROM matches
WHERE (hometeam = 'Huddersfield' AND awayteam = 'Swansea')
   OR (hometeam = 'Swansea' AND awayteam = 'Huddersfield');

```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql

SELECT COUNT(*) AS draw_count
FROM matches
WHERE division_code = 'N1'
AND season BETWEEN 2010 AND 2015
AND ftr = 'D';

```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql

SELECT *, (fthg + ftag) AS total_goals
FROM matches   
WHERE division_code = 'E0'
ORDER BY total_goals DESC, fthg DESC;

```

10) In which division and which season were the most goals scored?

```sql

SELECT division_code, divisions.name, season, SUM(fthg+ftag) FROM matches INNER JOIN divisions ON divisions.code = matches.division_code GROUP BY season, division_code, divisions.name ORDER BY SUM(fthg + ftag) DESC LIMIT 1;

```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)