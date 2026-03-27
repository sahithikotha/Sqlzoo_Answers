# 🏆 SQL Practice – SELECT from NOBEL (SQLZoo)

This repository contains my solutions to the **SQLZoo – SELECT from NOBEL** tutorial.
All problem statements are kept **exactly as given**, with my solutions, explanations, and learnings.

---

## 📌 Table Overview

| Column  | Description    |
| ------- | -------------- |
| yr      | Year of award  |
| subject | Prize category |
| winner  | Winner name    |

---

## 🧠 SQL Exercises

---

### ✅ 1. Winners from 1950

**📖 Problem:**
Change the query shown so that it displays Nobel prizes for 1950.

**💡 Query:**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

**🧾 Explanation:**
Filtered the records using `WHERE` to match a specific year.

**🎯 What I Learned:**

* Basic filtering using numeric conditions

---

### ✅ 2. 1962 Literature

**📖 Problem:**
Show who won the 1962 prize for literature.

**💡 Query:**

```sql
SELECT winner
FROM nobel
WHERE yr = 1962
  AND subject = 'Literature';
```

**🧾 Explanation:**
Used `AND` to apply multiple conditions together.

**🎯 What I Learned:**

* Combining filters using `AND`

---

### ✅ 3. Albert Einstein

**📖 Problem:**
Show the year and subject that won 'Albert Einstein' his prize.

**💡 Query:**

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

**🧾 Explanation:**
Filtered data using exact string match.

**🎯 What I Learned:**

* Querying based on text values

---

### ✅ 4. Recent Peace Prizes

**📖 Problem:**
Give the name of the 'peace' winners since the year 2000, including 2000.

**💡 Query:**

```sql
SELECT winner
FROM nobel
WHERE subject = 'Peace'
  AND yr >= 2000;
```

**🧾 Explanation:**
Used comparison operator to filter a range of years.

**🎯 What I Learned:**

* Filtering with conditions (`>=`)

---

### ✅ 5. Literature in the 1980's

**📖 Problem:**
Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.

**💡 Query:**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Literature'
  AND yr BETWEEN 1980 AND 1989;
```

**🧾 Explanation:**
`BETWEEN` includes both boundary values.

**🎯 What I Learned:**

* Range filtering using `BETWEEN`

---

### ✅ 6. Only Presidents

**📖 Problem:**
Show all details of the presidential winners:

Theodore Roosevelt
Thomas Woodrow Wilson
Jimmy Carter
Barack Obama

**💡 Query:**

```sql
SELECT *
FROM nobel
WHERE winner IN (
  'Theodore Roosevelt',
  'Thomas Woodrow Wilson',
  'Jimmy Carter',
  'Barack Obama'
);
```

**🧾 Explanation:**
Used `IN` to filter multiple specific values.

**🎯 What I Learned:**

* Efficient filtering using `IN`

---

### ✅ 7. John

**📖 Problem:**
Show the winners with first name John.

**💡 Query:**

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

**🧾 Explanation:**
Used `LIKE` with wildcard `%` to match names starting with "John".

**🎯 What I Learned:**

* Pattern matching with `LIKE`

---

### ✅ 8. Chemistry and Physics from different years

**📖 Problem:**
Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.

**💡 Query:**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Physics' AND yr = 1980)
   OR (subject = 'Chemistry' AND yr = 1984);
```

**🧾 Explanation:**
Used `OR` to combine multiple conditions.

**🎯 What I Learned:**

* Combining conditions using `OR`

---

### ✅ 9. Exclude Chemists and Medics

**📖 Problem:**
Show the year, subject, and name of winners for 1980 excluding chemistry and medicine.

**💡 Query:**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
  AND subject NOT IN ('Chemistry', 'Medicine');
```

**🧾 Explanation:**
Used `NOT IN` to exclude specific categories.

**🎯 What I Learned:**

* Excluding values in SQL

---

### ✅ 10. Early Medicine, Late Literature

**📖 Problem:**
Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004).

**💡 Query:**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910)
   OR (subject = 'Literature' AND yr >= 2004);
```

**🧾 Explanation:**
Combined multiple logical conditions using `AND` and `OR`.

**🎯 What I Learned:**

* Writing complex logical queries

---

### ✅ 11. Umlaut

**📖 Problem:**
Find all details of the prize won by PETER GRÜNBERG.

**💡 Query:**

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG';
```

**🧾 Explanation:**
Handled non-ASCII characters correctly.

**🎯 What I Learned:**

* Working with Unicode text

---

### ✅ 12. Apostrophe

**📖 Problem:**
Find all details of the prize won by EUGENE O'NEILL.

**💡 Query:**

```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL';
```

**🧾 Explanation:**
Escaped `'` using double single quotes.

**🎯 What I Learned:**

* Handling special characters in SQL

---

### ✅ 13. Knights of the realm

**📖 Problem:**
List the winners, year and subject where the winner starts with Sir. Show the most recent first, then by name order.

**💡 Query:**

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner;
```

**🧾 Explanation:**
Sorted results using `ORDER BY`.

**🎯 What I Learned:**

* Sorting results (`ASC`, `DESC`)

---

### ✅ 14. Chemistry and Physics last

**📖 Problem:**
Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.

**💡 Query:**

```sql
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY subject IN ('Physics','Chemistry'), subject, winner;
```

**🧾 Explanation:**
Used boolean logic inside `ORDER BY` to push specific values last.

**🎯 What I Learned:**

* Advanced sorting techniques

---

## 🚀 Overall Learnings

* Filtering using `WHERE`, `AND`, `OR`
* Using `IN`, `NOT IN`, `BETWEEN`
* Pattern matching with `LIKE`
* Handling special characters (`'`, Unicode)
* Sorting with `ORDER BY`
* Writing clean, readable SQL queries

---

✨ *Consistent practice to build strong SQL foundations.*
