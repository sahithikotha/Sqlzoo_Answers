# 🌍 SQL Practice – SELECT basics (SQLZoo)

This repository contains my solutions to the **SQLZoo – SELECT basics** tutorial.
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

### ✅ 1. Introducing the world table of countries

**📖 Problem:**
The example uses a WHERE clause to show the population of 'France'. Note that strings should be in 'single quotes';

Modify it to show the population of Germany.

**💡 Query:**

```sql
SELECT population 
FROM world
WHERE name = 'Germany';
```

**🧾 Explanation:**
Used the `WHERE` clause to filter rows where the country name is Germany.

**🎯 What I Learned:**

* Basic use of `SELECT`
* Filtering data using `WHERE`
* Using single quotes for string values

---

### ✅ 2. Scandinavia

**📖 Problem:**
Checking a list The word IN allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.

Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

**💡 Query:**

```sql
SELECT name, population 
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

**🧾 Explanation:**
Used `IN` to filter multiple values instead of writing multiple `OR` conditions.

**🎯 What I Learned:**

* Using `IN` for multiple conditions
* Writing cleaner queries

---

### ✅ 3. Just the right size

**📖 Problem:**
Which countries are not too small and not too big? BETWEEN allows range checking (range specified is inclusive of boundary values).

Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

**💡 Query:**

```sql
SELECT name, area 
FROM world
WHERE area BETWEEN 200000 AND 250000;
```

**🧾 Explanation:**
Used `BETWEEN` to filter values within a range (inclusive).

**🎯 What I Learned:**

* Range filtering using `BETWEEN`
* Understanding inclusive boundaries

---

## 🚀 Overall Learnings

* Writing basic `SELECT` queries
* Filtering data using `WHERE`
* Using `IN` for multiple values
* Using `BETWEEN` for range conditions
* Writing clean and readable SQL queries

---

✨ *This module builds the foundation for all SQL queries and filtering techniques.*
