# sql


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
