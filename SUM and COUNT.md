# 🌍 SQL Practice – SUM and COUNT (SQLZoo)

This repository contains my solutions to the **SQLZoo – SUM and COUNT** tutorial.
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

### ✅ 1. Total world population

**📖 Problem:**
Show the total population of the world.

**💡 Query:**

```sql
SELECT SUM(population)
FROM world;
```

**🧾 Explanation:**
`SUM()` adds all population values to return a single total.

**🎯 What I Learned:**

* Using aggregate functions (`SUM`)
* Aggregating data into a single result

---

### ✅ 2. List of continents

**📖 Problem:**
List all the continents - just once each.

**💡 Query:**

```sql
SELECT DISTINCT continent
FROM world;
```

**🧾 Explanation:**
`DISTINCT` removes duplicate values.

**🎯 What I Learned:**

* Eliminating duplicates using `DISTINCT`

---

### ✅ 3. GDP of Africa

**📖 Problem:**
Give the total GDP of Africa.

**💡 Query:**

```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa';
```

**🧾 Explanation:**
Filtered rows first, then aggregated GDP.

**🎯 What I Learned:**

* Combining `WHERE` with aggregate functions

---

### ✅ 4. Count the big countries

**📖 Problem:**
How many countries have an area of at least 1000000.

**💡 Query:**

```sql
SELECT COUNT(*)
FROM world
WHERE area >= 1000000;
```

**🧾 Explanation:**
`COUNT(*)` counts number of rows matching condition.

**🎯 What I Learned:**

* Counting rows using `COUNT`

---

### ✅ 5. Baltic states population

**📖 Problem:**
What is the total population of ('Estonia', 'Latvia', 'Lithuania').

**💡 Query:**

```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

**🧾 Explanation:**
Used `IN` to filter multiple countries, then summed population.

**🎯 What I Learned:**

* Combining `IN` with aggregation

---

### ✅ 6. Counting the countries of each continent

**📖 Problem:**
For each continent show the continent and number of countries.

**💡 Query:**

```sql
SELECT continent, COUNT(*)
FROM world
GROUP BY continent;
```

**🧾 Explanation:**
`GROUP BY` groups rows, `COUNT` counts within each group.

**🎯 What I Learned:**

* Grouping data using `GROUP BY`

---

### ✅ 7. Counting big countries in each continent

**📖 Problem:**
For each continent show the continent and number of countries with populations of at least 10 million.

**💡 Query:**

```sql
SELECT continent, COUNT(*)
FROM world
WHERE population >= 10000000
GROUP BY continent;
```

**🧾 Explanation:**
Filtered first, then grouped and counted.

**🎯 What I Learned:**

* Combining `WHERE` + `GROUP BY`

---

### ✅ 8. Counting big continents

**📖 Problem:**
List the continents that have a total population of at least 100 million.

**💡 Query:**

```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000;
```

**🧾 Explanation:**
`HAVING` filters groups after aggregation.

**🎯 What I Learned:**

* Difference between `WHERE` and `HAVING`
* Filtering aggregated results

---

## 🚀 Overall Learnings

* Using aggregate functions: `SUM`, `COUNT`
* Removing duplicates with `DISTINCT`
* Grouping data using `GROUP BY`
* Filtering groups using `HAVING`
* Combining filtering and aggregation effectively

---

✨ *This module strengthened my understanding of aggregation — a key concept in SQL.*
