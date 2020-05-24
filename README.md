# sql
[SQL Query Order of Execution](https://www.sisense.com/blog/sql-query-order-of-operations/)


# sqlzoo

## select basics
https://sqlzoo.net/wiki/SELECT_basics
```
SELECT population FROM world
  WHERE name = 'Germany'
```

```
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

```
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

quiz

```
SELECT name, population
  FROM world
 WHERE population BETWEEN 1000000 AND 1250000
```

```
SELECT name, population
      FROM world
      WHERE name LIKE "Al%"
```

```
SELECT name FROM world
 WHERE name LIKE '%a' OR name LIKE '%l'
```

```
SELECT name,length(name)
FROM world
WHERE length(name)=5 and region='Europe'
```

```
SELECT name, area*2 FROM world WHERE population = 64000
```

```
SELECT name, area, population
  FROM world
 WHERE area > 50000 AND population < 10000000
```

```
SELECT name, population/area
  FROM world
 WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

## SELECT from WORLD Tutorial
```
SELECT name, continent, population FROM world
```

```
SELECT name FROM world
WHERE population >= 200000000
```

```
SELECT name, gdp/population
FROM world
WHERE population >= 200000000
```

```
SELECT name, population/1000000
FROM world
WHERE continent = 'South America'
```

```
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

```
SELECT name
FROM world
WHERE name LIKE '%United%'
```

```
SELECT name, population, area
FROM world
WHERE area > 3000000 OR population > 250000000
```

```
SELECT name, population, area
FROM world
WHERE (area > 3000000 AND population <= 250000000) OR
              (area <= 3000000 AND population > 250000000)
`` seems also works:
WHERE area > 3000000 XOR population > 250000000
WHERE (area > 3000000) <> (population > 250000000)
WHERE (area > 3000000) != (population > 250000000)
```

```
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America'
```

```
SELECT name, ROUND(gdp/population/1000,0)*1000
FROM world
WHERE gdp >= 1000000000000
```

```
SELECT name, capital
  FROM world
 WHERE LENGTH(name) = LENGTH(capital)
```

```
SELECT name, capital
FROM world
WHERE (LEFT(name,1) = LEFT(capital,1)) AND (name <> capital)
```

```
SELECT name
   FROM world
WHERE name LIKE '%a%' AND
              name LIKE '%e%' AND
              name LIKE '%i%' AND
              name LIKE '%o%' AND
              name LIKE '%u%' AND
              name NOT LIKE '% %'
```

## SELECT from Nobel Tutorial
```
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

```
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```

```
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

```
SELECT winner
FROM nobel
WHERE yr >= 2000 AND subject = 'Peace'
```

```
SELECT *
FROM nobel
``WHERE yr >= 1980 AND yr <= 1989 AND subject = 'Literature'
WHERE yr BETWEEN 1980 AND 1989 AND subject = 'Literature'
```

```
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```

```
SELECT winner 
FROM nobel
WHERE winner LIKE 'John %'
```

```
SELECT *
FROM nobel
WHERE (yr = 1980 AND subject = 'Physics') OR (yr = 1984 AND subject = 'Chemistry')
```

```
SELECT *
FROM nobel
WHERE (yr = 1980) AND (NOT (subject IN ('Chemistry', 'Medicine') ))
```

```
SELECT *
FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910) OR 
               (subject = 'Literature' AND yr >= 2004)
```

```
SELECT *
FROM nobel 
WHERE winner = 'PETER GRÜNBERG'
```

```
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL'
```

```
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```

```
SELECT winner, subject
  FROM nobel
 WHERE yr=1984 
 ORDER BY subject IN ('Chemistry','Physics') ASC, subject, winner
```

quiz

```
SELECT winner FROM nobel
 WHERE winner LIKE 'C%' AND winner LIKE '%n'
```

```
SELECT COUNT(subject) FROM nobel
 WHERE subject = 'Chemistry'
   AND yr BETWEEN 1950 and 1960
```

```
SELECT COUNT(DISTINCT yr) FROM nobel
 WHERE yr NOT IN (SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')
```

```
SELECT subject, winner FROM nobel WHERE winner LIKE 'Sir%' AND yr LIKE '196%'
```

```
SELECT yr FROM nobel
 WHERE yr NOT IN(SELECT yr 
                   FROM nobel
                 WHERE subject IN ('Chemistry','Physics'))
```

```
SELECT DISTINCT yr
  FROM nobel
 WHERE subject='Medicine' 
   AND yr NOT IN(SELECT yr FROM nobel 
                  WHERE subject='Literature')
   AND yr NOT IN (SELECT yr FROM nobel
                   WHERE subject='Peace')
```

```
SELECT subject, COUNT(subject) 
   FROM nobel 
  WHERE yr ='1960' 
  GROUP BY subject
```

## SELECT within SELECT Tutorial
```
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

```
SELECT name 
FROM world
WHERE continent = 'Europe' AND gdp/population > 
( 
SELECT gdp/population
FROM world
WHERE name = 'United Kingdom'
)
```

```
SELECT name, continent
FROM world
WHERE continent IN
(
SELECT continent
FROM world
WHERE name IN ('Argentina', 'Australia')
)
ORDER BY name
```

```
SELECT name, population
FROM world
WHERE population >
(
SELECT population
FROM world
WHERE name = 'Canada'
)
AND population <
(
SELECT population
FROM world
WHERE name = 'Poland'
)
```

```
SELECT name, CONCAT(ROUND(population/(SELECT population FROM world WHERE name = 'Germany') * 100,0), '%')
FROM world
WHERE continent = 'Europe'
```

```
SELECT name
  FROM world
 WHERE population >= ALL(SELECT population
                           FROM world
                          WHERE population>0)
```

```
SELECT name
FROM world
WHERE gdp >
ALL(
SELECT gdp
FROM world
WHERE continent = 'Europe' AND gdp > 0
)
```

```
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)
```

```
SELECT continent, name
FROM world x
WHERE name <= 
ALL(
select name 
FROM world y
WHERE y.continent = x.continent
)
```

```
SELECT name, continent, population
FROM world y
WHERE 25000000 >= 
ALL(
SELECT population
FROM world x
WHERE x.continent = y.continent
)
```

```
SELECT name, continent
FROM world y
WHERE population >= 
ALL(
SELECT 3*population
from world x
WHERE x.continent = y.continent AND NOT (x.name = y.name)
)
```

quiz

```
SELECT region, name, population FROM bbc x WHERE population <= ALL (SELECT population FROM bbc y WHERE y.region=x.region AND population>0)
```

```
SELECT name,region,population FROM bbc x WHERE 50000 < ALL (SELECT population FROM bbc y WHERE x.region=y.region AND y.population>0)
```

```
SELECT name, region FROM bbc x
 WHERE population < ALL (SELECT population/3 FROM bbc y WHERE y.region = x.region AND y.name != x.name)
```

```
SELECT name FROM bbc
 WHERE population >
       (SELECT population
          FROM bbc
         WHERE name='United Kingdom')
   AND region IN
       (SELECT region
          FROM bbc
         WHERE name = 'United Kingdom')
```

```
SELECT name FROM bbc
 WHERE gdp > (SELECT MAX(gdp) FROM bbc WHERE region = 'Africa')
```

```
SELECT name FROM bbc
 WHERE population < (SELECT population FROM bbc WHERE name='Russia')
   AND population > (SELECT population FROM bbc WHERE name='Denmark')
```

```
SELECT name FROM bbc
 WHERE population > ALL
       (SELECT MAX(population)
          FROM bbc
         WHERE region = 'Europe')
   AND region = 'South Asia'
```

## SUM and COUNT
### Using SUM, Count, MAX, DISTINCT and ORDER BY
### Using GROUP BY and HAVING
```
SELECT SUM(population)
FROM world
```

```
SELECT DISTINCT continent 
FROM world
```

```
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```

```
SELECT COUNT(name)
FROM world
WHERE area >= 1000000
```

```
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

```
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```

```
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```

```
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```

quiz

```
SELECT SUM(population) FROM bbc WHERE region = 'Europe'
```

```
SELECT COUNT(name) FROM bbc WHERE population < 150000
```

Select the list of core SQL aggregate functions:\
AVG(), COUNT(), MAX(), MIN(), SUM()

```
SELECT AVG(population) FROM bbc WHERE name IN ('Poland', 'Germany', 'Denmark')
```

```
SELECT region, SUM(population)/SUM(area) AS density FROM bbc GROUP BY region
```

```
SELECT name, population/area AS density FROM bbc WHERE population = (SELECT MAX(population) FROM bbc)
```

```
SELECT region, SUM(area) 
   FROM bbc 
  GROUP BY region 
  HAVING SUM(area)<= 20000000
```

## The JOIN operation
```
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER'
```

```
SELECT id,stadium,team1,team2
  FROM game
where id = 1012
```

```
SELECT player,teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
WHERE teamid = 'GER'
```

```
SELECT team1, team2, player
FROM game JOIN goal ON (id = matchid)
WHERE player LIKE 'Mario%'
```

```
SELECT player, teamid, coach, gtime
  FROM goal JOIN eteam ON teamid = id
 WHERE gtime<=10
```
 
``` 
SELECT mdate, teamname
FROM game JOIN eteam ON team1 = eteam.id
WHERE coach = 'Fernando Santos'
```

```
SELECT player
FROM game JOIN goal ON id = matchid
WHERE stadium = 'National Stadium, Warsaw'
```

```
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id 
    WHERE (team1='GER' OR team2='GER') AND teamid != 'GER'
```

```
SELECT teamname, COUNT(matchid)
  FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
```

```
SELECT stadium, COUNT(id)
FROM game JOIN goal ON id = matchid
GROUP BY stadium
```

```
SELECT matchid,mdate, COUNT(matchid)
  FROM game JOIN goal ON id = matchid
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```

```
SELECT matchid, mdate, COUNT(matchid)
FROM game JOIN goal ON id = matchid
WHERE teamid = 'GER'
GROUP BY matchid, mdate
```

```
SELECT mdate,
  team1, 
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
team2, 
SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
  FROM game JOIN goal ON id = matchid
GROUP BY mdate, matchid, team1, team2
ORDER BY mdate, matchid, team1, team2
```

quiz

```
SELECT player, teamid, COUNT(*)
  FROM game JOIN goal ON matchid = id
 WHERE (team1 = "GRE" OR team2 = "GRE")
   AND teamid != 'GRE'
 GROUP BY player, teamid
```

```
SELECT DISTINCT teamid, mdate
  FROM goal JOIN game on (matchid=id)
 WHERE mdate = '9 June 2012'
```

```
SELECT DISTINCT player, teamid 
   FROM game JOIN goal ON matchid = id 
  WHERE stadium = 'National Stadium, Warsaw' 
 AND (team1 = 'POL' OR team2 = 'POL')
   AND teamid != 'POL'
```

```
SELECT DISTINCT player, teamid, gtime
  FROM game JOIN goal ON matchid = id
 WHERE stadium = 'Stadion Miejski (Wroclaw)'
   AND (( teamid = team2 AND team1 != 'ITA') OR ( teamid = team1 AND team2 != 'ITA'))
```

```
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON teamid = id
 GROUP BY teamname
HAVING COUNT(*) < 3
```

## More JOIN operations
```
SELECT id, title
 FROM movie
 WHERE yr=1962
```

```
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```

```
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
```

```
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```

```
SELECT id FROM movie
WHERE title = 'Casablanca'
```

```
SELECT name
FROM actor
WHERE id in
(
SELECT actorid
FROM casting
WHERE movieid = 
(
SELECT id
FROM movie
WHERE title = 'Casablanca'
)
)
```

```
SELECT name
FROM actor
WHERE id in
(
SELECT actorid
FROM casting
WHERE movieid = 
(
SELECT id
FROM movie
WHERE title = 'Alien'
)
)
```

```
SELECT title
FROM movie
WHERE id IN
(
SELECT movieid
FROM casting
WHERE actorid = 
(
SELECT id
FROM actor
WHERE name = 'Harrison Ford'
)
)
```

```
SELECT title
FROM movie
WHERE id IN
(
SELECT movieid
FROM casting
WHERE actorid = 
(
SELECT id
FROM actor
WHERE name = 'Harrison Ford'
) AND ord != 1
)
```

```
SELECT title, name
FROM (movie JOIN casting ON id = movieid) JOIN actor ON actorid=actor.id
WHERE yr = 1962 AND ord = 1
```

```
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```

```
SELECT title, name
FROM (movie JOIN casting ON id = movieid) JOIN actor ON actorid = actor.id
WHERE movieid IN
(
SELECT movieid FROM casting
WHERE actorid IN (
  SELECT id FROM actor
  WHERE name='Julie Andrews')
)
AND ord = 1
```

```
SELECT name FROM actor JOIN casting ON id = actorid
WHERE ord = 1
GROUP BY name
HAVING COUNT(*) >= 15
ORDER BY name ASC
```

```
SELECT title, COUNT(*)
FROM movie JOIN casting ON id = movieid
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(*) DESC, title
```

```
SELECT DISTINCT name 
FROM actor JOIN casting ON id = actorid
WHERE name != 'Art Garfunkel' AND movieid IN
(
SELECT movieid FROM casting JOIN actor ON actorid = id
WHERE name = 'Art Garfunkel'
)
```

## Using Null
```
SELECT name FROM teacher
WHERE dept IS NULL
```

```
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```

```
SELECT teacher.name, dept.name
FROM teacher LEFT JOIN dept ON teacher.dept = dept.id
```

```
SELECT teacher.name, dept.name
FROM teacher RIGHT JOIN dept ON teacher.dept = dept.id
```

```
SELECT name, COALESCE(mobile, '07986 444 2266')
FROM teacher
```

```
SELECT teacher.name, COALESCE(dept.name, 'None')
FROM teacher LEFT JOIN dept on dept = dept.id
```

```
SELECT COUNT(name), COUNT(mobile)
FROM teacher
```

```
SELECT dept.name, COUNT(teacher.dept)
FROM teacher RIGHT JOIN dept ON dept = dept.id
GROUP BY dept.name
```

```
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci' ELSE 'Art' END
FROM teacher
```

```
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci' WHEN dept = 3 THEN 'Art' ELSE 'None' END
FROM teacher
```
