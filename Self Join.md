# 🚌 SQL Practice – Self join (SQLZoo)

This repository contains my solutions to the **SQLZoo – Self join** tutorial.

---

## 📌 Tables Overview

### 🟦 stops

| Column | Description |
| ------ | ----------- |
| id     | Stop ID     |
| name   | Stop name   |

### 🟩 route

| Column  | Description         |
| ------- | ------------------- |
| num     | Bus number          |
| company | Bus company         |
| pos     | Stop order/position |
| stop    | Stop ID             |

---

## 🧠 SQL Exercises

---

### ✅ 1.

**📖 Problem:**
How many stops are in the database.

**💡 Query:**

```sql
SELECT COUNT(*)
FROM stops;
```

**🧾 Explanation:**
Counts all rows in the `stops` table.

**🎯 What I Learned:**

* Using `COUNT(*)` to count total rows

---

### ✅ 2.

**📖 Problem:**
Find the id value for the stop 'Craiglockhart'

**💡 Query:**

```sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart';
```

**🧾 Explanation:**
Looks up the stop ID by exact stop name.

**🎯 What I Learned:**

* Retrieving specific values using `WHERE`

---

### ✅ 3.

**📖 Problem:**
Give the id and the name for the stops on the '4' 'LRT' service.

**💡 Query:**

```sql
SELECT stops.id, stops.name
FROM route
JOIN stops ON route.stop = stops.id
WHERE route.num = '4'
  AND route.company = 'LRT';
```

**🧾 Explanation:**
Joins `route` and `stops` to display stop details for a specific bus service.

**🎯 What I Learned:**

* Joining route data with stop data
* Filtering by service number and company

---

### ✅ 4.

**📖 Problem:**
The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

**💡 Query:**

```sql
SELECT company, num, COUNT(*)
FROM route
WHERE stop = 149 OR stop = 53
GROUP BY company, num
HAVING COUNT(*) = 2;
```

**🧾 Explanation:**
Groups routes and keeps only those that visit both stops.

**🎯 What I Learned:**

* Using `GROUP BY` with `HAVING`
* Filtering grouped results

---

### ✅ 5.

**📖 Problem:**
Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

**💡 Query:**

```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a
JOIN route b
  ON a.company = b.company AND a.num = b.num
WHERE a.stop = 53
  AND b.stop = 149;
```

**🧾 Explanation:**
Uses a self join on the `route` table to find services connecting two stops directly.

**🎯 What I Learned:**

* Basics of self join
* Comparing rows within the same table

---

### ✅ 6.

**📖 Problem:**
The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

**💡 Query:**

```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a
JOIN route b
  ON a.company = b.company AND a.num = b.num
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart'
  AND stopb.name = 'London Road';
```

**🧾 Explanation:**
Joins the same tables multiple times using aliases so stops can be matched by name instead of ID.

**🎯 What I Learned:**

* Using aliases with self joins
* Joining the same table more than once

---

## 🔁 Using a self join

---

### ✅ 7.

**📖 Problem:**
Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

**💡 Query:**

```sql
SELECT a.company, a.num
FROM route a
JOIN route b
  ON a.company = b.company AND a.num = b.num
WHERE a.stop = 115
  AND b.stop = 137;
```

**🧾 Explanation:**
Finds all services where both stops appear on the same route.

**🎯 What I Learned:**

* Identifying direct connections between two stops

---

### ✅ 8.

**📖 Problem:**
Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

**💡 Query:**

```sql
SELECT a.company, a.num
FROM route a
JOIN route b
  ON a.company = b.company AND a.num = b.num
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart'
  AND stopb.name = 'Tollcross';
```

**🧾 Explanation:**
Same self join logic, but this time matching stop names instead of numeric IDs.

**🎯 What I Learned:**

* Solving route problems using names instead of IDs

---

### ✅ 9.

**📖 Problem:**
Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

**💡 Query:**

```sql
SELECT DISTINCT stopb.name, b.company, b.num
FROM route a
JOIN route b
  ON a.company = b.company AND a.num = b.num
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart'
  AND a.company = 'LRT';
```

**🧾 Explanation:**
Starts from Craiglockhart and finds every reachable stop on the same LRT service.

**🎯 What I Learned:**

* Using `DISTINCT` to remove duplicates
* Finding all directly reachable destinations

---

### ✅ 10.

**📖 Problem:**
Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.

**💡 Query:**

```sql
SELECT DISTINCT a.num, a.company, stopx.name, b.num, b.company
FROM route a
JOIN route a2
  ON a.company = a2.company AND a.num = a2.num
JOIN route b
JOIN route b2
  ON b.company = b2.company AND b.num = b2.num
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b2.stop = stopb.id
JOIN stops stopx ON a2.stop = stopx.id AND b.stop = stopx.id
WHERE stopa.name = 'Craiglockhart'
  AND stopb.name = 'Lochend';
```

**🧾 Explanation:**
Finds two-bus journeys by identifying a transfer stop shared between two different routes.

**🎯 What I Learned:**

* Solving multi-step journey problems
* Advanced self join logic with transfer points

---

## 🚀 Overall Learnings

* Understanding self joins
* Using aliases to compare rows in the same table
* Finding direct and indirect connections
* Combining self joins with `GROUP BY`, `HAVING`, and `DISTINCT`
* Solving route and transfer problems using SQL

---

✨ *This module strengthened my understanding of self joins, aliases, and route-mapping logic — valuable skills for solving advanced SQL problems.*
