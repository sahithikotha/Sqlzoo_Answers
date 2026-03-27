# 🌍 SQL Practice – SELECT within SELECT (SQLZoo)

This repository contains my solutions to the **SQLZoo – SELECT within SELECT** tutorial.
All problem statements are kept **exactly as given**, along with my solutions, explanations, and key learnings.

---

## 📌 Table Overview

| Column     | Description            |
| ---------- | ---------------------- |
| name       | Country name           |
| continent  | Continent              |
| area       | Area (sq. km)          |
| population | Population             |
| gdp        | Gross Domestic Product |

---

## 🧠 SQL Exercises

---

### ✅ 1. Bigger than Russia

**📖 Problem:**
List each country name where the population is larger than that of 'Russia'.

**💡 Query:**

```sql
SELECT name 
FROM world
WHERE population > (
  SELECT population 
  FROM world 
  WHERE name = 'Russia'
);
```

**🧾 Explanation:**
Used a subquery to get Russia’s population, then compared all countries against it.

**🎯 What I Learned:**

* Basics of subqueries
* Comparing values using nested SELECT

---

### ✅ 2. Richer than UK

**📖 Problem:**
Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

**💡 Query:**

```sql
SELECT name
FROM world
WHERE continent = 'Europe'
  AND gdp/population > (
    SELECT gdp/population
    FROM world
    WHERE name = 'United Kingdom'
  );
```

**🧾 Explanation:**
Compared calculated values (per capita GDP) using a subquery.

**🎯 What I Learned:**

* Using calculations inside subqueries
* Comparing derived values

---

### ✅ 3. Neighbours of Argentina and Australia

**📖 Problem:**
List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

**💡 Query:**

```sql
SELECT name, continent
FROM world
WHERE continent IN (
  SELECT continent
  FROM world
  WHERE name IN ('Argentina', 'Australia')
)
ORDER BY name;
```

**🧾 Explanation:**
Subquery finds continents, outer query fetches countries in those continents.

**🎯 What I Learned:**

* Using `IN` with subqueries
* Multi-step filtering

---

### ✅ 4. Between Canada and Poland

**📖 Problem:**
Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.

**💡 Query:**

```sql
SELECT name, population
FROM world
WHERE population > (
  SELECT population FROM world WHERE name = 'United Kingdom'
)
AND population < (
  SELECT population FROM world WHERE name = 'Germany'
);
```

**🧾 Explanation:**
Used two subqueries to define a range.

**🎯 What I Learned:**

* Combining multiple subqueries
* Range filtering with dynamic values

---

### ✅ 5. Percentages of Germany

**📖 Problem:**
Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

**💡 Query:**

```sql
SELECT name,
       CONCAT(ROUND(population * 100 / (
         SELECT population 
         FROM world 
         WHERE name = 'Germany'
       )), '%') AS percentage
FROM world
WHERE continent = 'Europe';
```

**🧾 Explanation:**
Calculated percentage using Germany’s population from a subquery.

**🎯 What I Learned:**

* Using subqueries in calculations
* Formatting output (`ROUND`, `CONCAT`)

---

### ✅ 6. Bigger than every country in Europe

**📖 Problem:**
Which countries have a GDP greater than every country in Europe? (Give the name only.)

**💡 Query:**

```sql
SELECT name
FROM world
WHERE gdp > ALL (
  SELECT gdp
  FROM world
  WHERE continent = 'Europe' AND gdp IS NOT NULL
);
```

**🧾 Explanation:**
`ALL` ensures the value is greater than every value in the subquery.

**🎯 What I Learned:**

* Using `ALL` with subqueries
* Handling NULL values

---

### ✅ 7. Largest in each continent

**📖 Problem:**
Find the largest country (by area) in each continent, show the continent, the name and the area.

**💡 Query:**

```sql
SELECT continent, name, area
FROM world x
WHERE area >= ALL (
  SELECT area
  FROM world y
  WHERE y.continent = x.continent
    AND area > 0
);
```

**🧾 Explanation:**
Used a correlated subquery to compare within each continent.

**🎯 What I Learned:**

* Correlated subqueries
* Comparing within groups

---

### ✅ 8. First country of each continent (alphabetically)

**📖 Problem:**
List each continent and the name of the country that comes first alphabetically.

**💡 Query:**

```sql
SELECT continent, name
FROM world x
WHERE name = (
  SELECT MIN(name)
  FROM world y
  WHERE y.continent = x.continent
);
```

**🧾 Explanation:**
Used `MIN()` with correlated subquery to get alphabetical first.

**🎯 What I Learned:**

* Combining aggregate functions with subqueries

---

### ✅ 9. Difficult Question

**📖 Problem:**
Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents.

**💡 Query:**

```sql
SELECT name, continent, population
FROM world
WHERE continent IN (
  SELECT continent
  FROM world
  GROUP BY continent
  HAVING MAX(population) <= 25000000
);
```

**🧾 Explanation:**
Used `GROUP BY` and `HAVING` inside subquery.

**🎯 What I Learned:**

* Combining aggregation with subqueries

---

### ✅ 10. Three time bigger

**📖 Problem:**
Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

**💡 Query:**

```sql
SELECT name, continent
FROM world x
WHERE population > 3 * ALL (
  SELECT population
  FROM world y
  WHERE y.continent = x.continent
    AND y.name <> x.name
);
```

**🧾 Explanation:**
Compared each country with all others in the same continent.

**🎯 What I Learned:**

* Advanced use of `ALL`
* Comparing rows within groups

---

## 🚀 Overall Learnings

* Writing nested queries (subqueries)
* Using `IN`, `ALL`, and correlated subqueries
* Performing calculations using subqueries
* Combining aggregation (`GROUP BY`, `HAVING`) with subqueries
* Solving complex real-world SQL problems

---

✨ *This module strengthened my understanding of subqueries — a key concept for advanced SQL and real-world data analysis.*
