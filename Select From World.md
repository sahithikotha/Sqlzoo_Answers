# 🌍 SQL Practice – SELECT from WORLD (SQLZoo)

This repository contains my solutions to the **SQLZoo – SELECT from WORLD** tutorial.
It focuses on building strong fundamentals in SQL querying, filtering, calculations, and string operations.

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

### ✅ 1. Basic SELECT

**📖 Problem:**
Show name, continent, and population of all countries.

**💡 Query:**

```sql
SELECT name, continent, population 
FROM world;
```

**🧾 Explanation:**
Retrieves specific columns from the table.

**🎯 What I Learned:**

* Basic `SELECT` usage
* Fetching multiple columns

---

### ✅ 2. Large Countries

**📖 Problem:**
Countries with population ≥ 200 million.

**💡 Query:**

```sql
SELECT name 
FROM world
WHERE population >= 200000000;
```

**📊 Result (Sample):**

```text
Brazil
China
India
Indonesia
Nigeria
Pakistan
United States
```

**🧾 Explanation:**
Uses `WHERE` with comparison operator to filter large populations.

**🎯 What I Learned:**

* Numeric filtering with `WHERE`
* Using comparison operators (`>=`)

---

### ✅ 3. Per Capita GDP

**📖 Problem:**
Show per capita GDP for large countries.

**💡 Query:**

```sql
SELECT name, gdp/population 
FROM world
WHERE population >= 200000000;
```

**🧾 Explanation:**
Per capita GDP = `gdp / population`.

**🎯 What I Learned:**

* Performing calculations in SQL
* Derived columns

---

### ✅ 4. South America Population (Millions)

**💡 Query:**

```sql
SELECT name, population/1000000 
FROM world
WHERE continent = 'South America';
```

**🧾 Explanation:**
Dividing values to convert into millions.

**🎯 What I Learned:**

* Data transformation using arithmetic
* Filtering with text values

---

### ✅ 5. France, Germany, Italy

**💡 Query:**

```sql
SELECT name, population 
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

**🧾 Explanation:**
`IN` is used to match multiple values.

**🎯 What I Learned:**

* Efficient multi-value filtering

---

### ✅ 6. Countries Containing "United"

**💡 Query:**

```sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

**🧾 Explanation:**
`LIKE` with `%` is used for pattern matching.

**🎯 What I Learned:**

* String searching in SQL
* Wildcards (`%`)

---

### ✅ 7. Two Ways to be Big

**💡 Query:**

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 OR population > 250000000;
```

**🧾 Explanation:**
Uses `OR` to combine conditions.

**🎯 What I Learned:**

* Logical operators (`OR`)

---

### ✅ 8. Exclusive OR (XOR)

**💡 Query:**

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 XOR population > 250000000;
```

**🧾 Explanation:**
Returns rows where only one condition is true.

**🎯 What I Learned:**

* XOR logic in SQL

---

### ✅ 9. Rounding Values

**💡 Query:**

```sql
SELECT 
    name, 
    ROUND(population/1000000.00, 2), 
    ROUND(gdp/1000000000.00, 2)
FROM world
WHERE continent = 'South America';
```

**🧾 Explanation:**
`ROUND()` formats numbers to 2 decimal places.

**🎯 What I Learned:**

* Data formatting
* Handling decimals

---

### ✅ 10. Trillion Dollar Economies

**💡 Query:**

```sql
SELECT name, ROUND(gdp/population, -3)
FROM world
WHERE gdp >= 1000000000000;
```

**🧾 Explanation:**
Rounds to nearest thousand using negative precision.

**🎯 What I Learned:**

* Advanced rounding techniques

---

### ✅ 11. Same Length Name & Capital

**💡 Query:**

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

**🧾 Explanation:**
Compares string lengths.

**🎯 What I Learned:**

* String functions (`LENGTH`)

---

### ✅ 12. Matching First Letters

**💡 Query:**

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1)
  AND name <> capital;
```

**🧾 Explanation:**

* `LEFT()` extracts first character
* `<>` means NOT equal

**🎯 What I Learned:**

* String comparison
* Combining conditions

---

### ✅ 13. All Vowels (No Spaces)

**💡 Query:**

```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
  AND name LIKE '%e%'
  AND name LIKE '%i%'
  AND name LIKE '%o%'
  AND name LIKE '%u%'
  AND name NOT LIKE '% %';
```

**🧾 Explanation:**
Checks presence of all vowels and excludes spaces.

**🎯 What I Learned:**

* Complex filtering using multiple conditions
* Pattern matching

---

## 🚀 Overall Learnings

* Writing efficient `SELECT` queries
* Filtering using `WHERE`, `IN`, `LIKE`
* Logical operators (`AND`, `OR`, `XOR`)
* Performing calculations in SQL
* Using string functions (`LENGTH`, `LEFT`)
* Formatting results with `ROUND()`

---

✨ *This is part of my journey toward mastering SQL.*
