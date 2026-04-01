# 🧩 SQL Practice – Using NULL (SQLZoo)

This repository contains my solutions to the **SQLZoo – Using NULL** tutorial.
---

## 📌 Tables Overview

### 🟦 teacher

| Column | Description   |
| ------ | ------------- |
| id     | Teacher ID    |
| dept   | Department ID |
| name   | Teacher name  |
| phone  | Phone number  |
| mobile | Mobile number |

### 🟩 dept

| Column | Description     |
| ------ | --------------- |
| id     | Department ID   |
| name   | Department name |

---

## 🧠 SQL Exercises

---

### ✅ 1.

**📖 Problem:**
List the teachers who have NULL for their department.

**💡 Query:**

```sql
SELECT name
FROM teacher
WHERE dept IS NULL;
```

**🧾 Explanation:**
`NULL` cannot be checked using `=`, so we use `IS NULL`.

**🎯 What I Learned:**

* Handling NULL values correctly
* Using `IS NULL` instead of `=`

---

### ✅ 2.

**📖 Problem:**
Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

**💡 Query:**

```sql
SELECT teacher.name, dept.name
FROM teacher
INNER JOIN dept ON teacher.dept = dept.id;
```

**🧾 Explanation:**
`INNER JOIN` returns only matching rows.

**🎯 What I Learned:**

* Behavior of INNER JOIN

---

### ✅ 3.

**📖 Problem:**
Use a different JOIN so that all teachers are listed.

**💡 Query:**

```sql
SELECT teacher.name, dept.name
FROM teacher
LEFT JOIN dept ON teacher.dept = dept.id;
```

**🧾 Explanation:**
`LEFT JOIN` keeps all teachers, even if they have no department.

**🎯 What I Learned:**

* Using LEFT JOIN to include unmatched rows

---

### ✅ 4.

**📖 Problem:**
Use a different JOIN so that all departments are listed.

**💡 Query:**

```sql
SELECT teacher.name, dept.name
FROM teacher
RIGHT JOIN dept ON teacher.dept = dept.id;
```

**🧾 Explanation:**
`RIGHT JOIN` keeps all departments, even if they have no teachers.

**🎯 What I Learned:**

* Using RIGHT JOIN

---

## 🔧 Using COALESCE

---

### ✅ 5.

**📖 Problem:**
Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given.

**💡 Query:**

```sql
SELECT name, COALESCE(mobile, '07986 444 2266')
FROM teacher;
```

**🧾 Explanation:**
`COALESCE` returns the first non-NULL value.

**🎯 What I Learned:**

* Handling missing values with COALESCE

---

### ✅ 6.

**📖 Problem:**
Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

**💡 Query:**

```sql
SELECT teacher.name, COALESCE(dept.name, 'None')
FROM teacher
LEFT JOIN dept ON teacher.dept = dept.id;
```

**🧾 Explanation:**
Replaces NULL department names with 'None'.

**🎯 What I Learned:**

* Combining JOIN + COALESCE

---

### ✅ 7.

**📖 Problem:**
Use COUNT to show the number of teachers and the number of mobile phones.

**💡 Query:**

```sql
SELECT COUNT(name), COUNT(mobile)
FROM teacher;
```

**🧾 Explanation:**

* `COUNT(name)` counts all rows
* `COUNT(mobile)` ignores NULL values

**🎯 What I Learned:**

* COUNT behaves differently with NULLs

---

### ✅ 8.

**📖 Problem:**
Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

**💡 Query:**

```sql
SELECT dept.name, COUNT(teacher.id)
FROM teacher
RIGHT JOIN dept ON teacher.dept = dept.id
GROUP BY dept.name;
```

**🧾 Explanation:**
Ensures all departments appear, even with zero teachers.

**🎯 What I Learned:**

* GROUP BY with JOIN
* Handling missing data in groups

---

## 🔀 Using CASE

---

### ✅ 9.

**📖 Problem:**
Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.

**💡 Query:**

```sql
SELECT name,
       CASE 
         WHEN dept IN (1,2) THEN 'Sci'
         ELSE 'Art'
       END
FROM teacher;
```

**🧾 Explanation:**
Conditional logic using `CASE`.

**🎯 What I Learned:**

* Writing conditional expressions in SQL

---

### ✅ 10.

**📖 Problem:**
Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

**💡 Query:**

```sql
SELECT name,
       CASE 
         WHEN dept IN (1,2) THEN 'Sci'
         WHEN dept = 3 THEN 'Art'
         ELSE 'None'
       END
FROM teacher;
```

**🧾 Explanation:**
Multiple conditions handled in sequence.

**🎯 What I Learned:**

* Advanced CASE usage

---

## 🚀 Overall Learnings

* Handling NULL values using `IS NULL`
* Understanding JOIN types (`INNER`, `LEFT`, `RIGHT`)
* Using `COALESCE` for default values
* Understanding how `COUNT` treats NULLs
* Writing conditional logic using `CASE`
* Managing incomplete/missing data in SQL

---

✨ *This module strengthened my understanding of NULL handling and JOIN behavior — critical for real-world datasets where missing data is common.*
