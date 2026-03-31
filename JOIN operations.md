# 🎬 SQL Practice – More JOIN operations (SQLZoo)

This repository contains my solutions to the **SQLZoo – More JOIN operations** tutorial.

---

## 📌 Tables Overview

### 🟦 movie

| Column   | Description         |
| -------- | ------------------- |
| id       | Movie ID            |
| title    | Movie title         |
| yr       | Release year        |
| director | Director ID         |
| budget   | Movie budget        |
| gross    | Movie gross revenue |

### 🟩 actor

| Column | Description |
| ------ | ----------- |
| id     | Actor ID    |
| name   | Actor name  |

### 🟥 casting

| Column  | Description                |
| ------- | -------------------------- |
| movieid | Movie ID                   |
| actorid | Actor ID                   |
| ord     | Actor position in the cast |

---

## 🧠 SQL Exercises

---

### ✅ 1. 1962 movies

**📖 Problem:**
List the films where the yr is 1962 and the budget is over 2000000 [Show id, title]

**💡 Query:**

```sql
SELECT id, title
FROM movie
WHERE yr = 1962
  AND budget > 2000000;
```

**🧾 Explanation:**
Filters films by both year and budget.

**🎯 What I Learned:**

* Using multiple conditions with `AND`
* Filtering numeric values

---

### ✅ 2. When was Citizen Kane released?

**📖 Problem:**
Give year of 'Citizen Kane'.

**💡 Query:**

```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane';
```

**🧾 Explanation:**
Looks up a single movie title and returns its release year.

**🎯 What I Learned:**

* Retrieving a specific column from a filtered row

---

### ✅ 3. Star Trek movies

**📖 Problem:**
List all of the Star Trek movies, include the id, title and yr (all of these movies start with the words Star Trek in the title). Order results by year.

**💡 Query:**

```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE 'Star Trek%'
ORDER BY yr;
```

**🧾 Explanation:**
Uses `LIKE` to match titles starting with "Star Trek" and sorts them by year.

**🎯 What I Learned:**

* Pattern matching with `LIKE`
* Sorting results using `ORDER BY`

---

### ✅ 4. id for actor Glenn Close

**📖 Problem:**
What id number does the actor 'Glenn Close' have?

**💡 Query:**

```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close';
```

**🧾 Explanation:**
Finds the actor ID by exact name match.

**🎯 What I Learned:**

* Looking up unique identifiers

---

### ✅ 5. id for Casablanca

**📖 Problem:**
What is the id of the 1942 film 'Casablanca'

**💡 Query:**

```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
  AND yr = 1942;
```

**🧾 Explanation:**
Filters by both title and year to avoid ambiguity.

**🎯 What I Learned:**

* Using multiple filters for precise lookup

---

### ✅ 6. Cast list for Casablanca

**📖 Problem:**
Obtain the cast list for 1942's 'Casablanca'.

**💡 Query:**

```sql
SELECT name
FROM actor
JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = casting.movieid
WHERE movie.title = 'Casablanca'
  AND movie.yr = 1942;
```

**🧾 Explanation:**
Joins `actor`, `casting`, and `movie` to retrieve all actors in the film.

**🎯 What I Learned:**

* Joining three tables
* Using link tables like `casting`

---

### ✅ 7. Alien cast list

**📖 Problem:**
Obtain the cast list for the film 'Alien'

**💡 Query:**

```sql
SELECT name
FROM actor
JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = casting.movieid
WHERE movie.title = 'Alien';
```

**🧾 Explanation:**
Same join pattern as the previous question, but filtering by a different movie.

**🎯 What I Learned:**

* Reusing JOIN logic across similar problems

---

### ✅ 8. Harrison Ford movies

**📖 Problem:**
List the films in which 'Harrison Ford' has appeared

**💡 Query:**

```sql
SELECT title
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE actor.name = 'Harrison Ford';
```

**🧾 Explanation:**
Finds all movies linked to Harrison Ford through the `casting` table.

**🎯 What I Learned:**

* Traversing relationships through JOINs

---

### ✅ 9. Harrison Ford as a supporting actor

**📖 Problem:**
List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

**💡 Query:**

```sql
SELECT title
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE actor.name = 'Harrison Ford'
  AND ord <> 1;
```

**🧾 Explanation:**
Filters out starring roles by excluding `ord = 1`.

**🎯 What I Learned:**

* Filtering based on role position in a cast list

---

### ✅ 10. Lead actors in 1962 movies

**📖 Problem:**
List the films together with the leading star for all 1962 films.

**💡 Query:**

```sql
SELECT title, name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE movie.yr = 1962
  AND casting.ord = 1;
```

**🧾 Explanation:**
The leading actor is identified by `ord = 1`.

**🎯 What I Learned:**

* Combining JOINs with role-based filtering

---

## 🔥 Harder Questions

---

### ✅ 11. Busy years for Rock Hudson

**📖 Problem:**
Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

**💡 Query:**

```sql
SELECT yr, COUNT(title)
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE actor.name = 'Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2;
```

**🧾 Explanation:**
Groups Rock Hudson’s movies by year and filters years where he made more than two movies.

**🎯 What I Learned:**

* Using `GROUP BY` with JOINs
* Filtering grouped results using `HAVING`

---

### ✅ 12. Lead actor in Julie Andrews movies

**📖 Problem:**
List the film title and the leading actor for all of the films 'Julie Andrews' played in.

**💡 Query:**

```sql
SELECT m.title, a.name
FROM movie m
JOIN casting c1 ON m.id = c1.movieid
JOIN actor ja ON ja.id = c1.actorid
JOIN casting c2 ON m.id = c2.movieid
JOIN actor a ON a.id = c2.actorid
WHERE ja.name = 'Julie Andrews'
  AND c2.ord = 1;
```

**🧾 Explanation:**
Uses one join path to find Julie Andrews’ movies and another to find the lead actor in those same movies.

**🎯 What I Learned:**

* Self-joining through the same table with aliases
* Using aliases to manage complex JOINs

---

### ✅ 13. Actors with 15 leading roles

**📖 Problem:**
Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

**💡 Query:**

```sql
SELECT actor.name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE ord = 1
GROUP BY actor.name
HAVING COUNT(*) >= 15
ORDER BY actor.name;
```

**🧾 Explanation:**
Counts leading roles (`ord = 1`) for each actor and keeps only those with 15 or more.

**🎯 What I Learned:**

* Aggregating role counts per actor
* Filtering grouped results with thresholds

---

### ✅ 14. released in the year 1978

**📖 Problem:**
List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

**💡 Query:**

```sql
SELECT movie.title, COUNT(casting.actorid)
FROM movie
JOIN casting ON movie.id = casting.movieid
WHERE movie.yr = 1978
GROUP BY movie.title
ORDER BY COUNT(casting.actorid) DESC, movie.title;
```

**🧾 Explanation:**
Counts cast members for each 1978 film, then sorts by cast size and title.

**🎯 What I Learned:**

* Counting related rows after a JOIN
* Ordering by aggregated values

---

### ✅ 15. with 'Art Garfunkel'

**📖 Problem:**
List all the people who have worked with 'Art Garfunkel'.

**💡 Query:**

```sql
SELECT DISTINCT a2.name
FROM actor a1
JOIN casting c1 ON a1.id = c1.actorid
JOIN casting c2 ON c1.movieid = c2.movieid
JOIN actor a2 ON a2.id = c2.actorid
WHERE a1.name = 'Art Garfunkel'
  AND a2.name <> 'Art Garfunkel';
```

**🧾 Explanation:**
Finds all actors who appeared in the same movies as Art Garfunkel, excluding Art Garfunkel himself.

**🎯 What I Learned:**

* Self-joining relationship tables
* Using `DISTINCT` to remove duplicates

---

## 🚀 Overall Learnings

* Joining multiple related tables
* Using bridge tables like `casting`
* Filtering based on actor roles with `ord`
* Grouping and counting joined data
* Using aliases for more advanced JOIN queries
* Solving real-world many-to-many relationship problems

---

✨ *This module strengthened my understanding of multi-table JOINs, aliases, and cast-based queries — all important for real SQL problem-solving.*
