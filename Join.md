# ⚽ SQL Practice – JOIN (SQLZoo UEFA EURO 2012)

This repository contains my solutions to the **SQLZoo – JOIN** tutorial.
All problem statements are kept **exactly as given**, along with my solutions, explanations, and key learnings.

---

## 📌 Tables Overview

### 🟦 game

| Column  | Description |
| ------- | ----------- |
| id      | Match ID    |
| mdate   | Match date  |
| stadium | Stadium     |
| team1   | Home team   |
| team2   | Away team   |

### 🟩 goal

| Column  | Description |
| ------- | ----------- |
| matchid | Match ID    |
| teamid  | Team ID     |
| player  | Player name |
| gtime   | Goal time   |

### 🟥 eteam

| Column   | Description |
| -------- | ----------- |
| id       | Team ID     |
| teamname | Team name   |
| coach    | Coach name  |

---

## 🧠 SQL Exercises

---

### ✅ 1.

**📖 Problem:**
Modify it to show the matchid and player name for all goals scored by Germany.

**💡 Query:**

```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER';
```

**🧾 Explanation:**
Filtered German goals using `teamid`.

**🎯 What I Learned:**

* Filtering before joining

---

### ✅ 2.

**📖 Problem:**
Show id, stadium, team1, team2 for just game 1012.

**💡 Query:**

```sql
SELECT id, stadium, team1, team2
FROM game
WHERE id = 1012;
```

**🎯 What I Learned:**

* Retrieving specific rows

---

### ✅ 3.

**📖 Problem:**
Modify it to show the player, teamid, stadium and mdate for every German goal.

**💡 Query:**

```sql
SELECT player, teamid, stadium, mdate
FROM game JOIN goal ON game.id = goal.matchid
WHERE teamid = 'GER';
```

**🧾 Explanation:**
Joined `game` and `goal` using match id.

**🎯 What I Learned:**

* Basic JOIN syntax
* Connecting two tables

---

### ✅ 4.

**📖 Problem:**
Show the team1, team2 and player for every goal scored by a player called Mario.

**💡 Query:**

```sql
SELECT team1, team2, player
FROM game JOIN goal ON game.id = goal.matchid
WHERE player LIKE 'Mario%';
```

**🎯 What I Learned:**

* Combining JOIN + LIKE

---

### ✅ 5.

**📖 Problem:**
Show player, teamid, coach, gtime for all goals scored in the first 10 minutes.

**💡 Query:**

```sql
SELECT player, goal.teamid, coach, gtime
FROM goal
JOIN eteam ON goal.teamid = eteam.id
WHERE gtime <= 10;
```

**🧾 Explanation:**
Joined `goal` with `eteam` to get coach details.

**🎯 What I Learned:**

* Joining with lookup tables

---

### ✅ 6.

**📖 Problem:**
List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

**💡 Query:**

```sql
SELECT mdate, teamname
FROM game
JOIN eteam ON game.team1 = eteam.id
WHERE coach = 'Fernando Santos';
```

**🎯 What I Learned:**

* Joining using different keys

---

### ✅ 7.

**📖 Problem:**
List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.

**💡 Query:**

```sql
SELECT player
FROM game
JOIN goal ON game.id = goal.matchid
WHERE stadium = 'National Stadium, Warsaw';
```

**🎯 What I Learned:**

* Filtering after JOIN

---

## 🔥 More Difficult Questions

---

### ✅ 8.

**📖 Problem:**
Show the name of all players who scored a goal against Germany.

**💡 Query:**

```sql
SELECT player
FROM game
JOIN goal ON game.id = goal.matchid
WHERE (team1 = 'GER' OR team2 = 'GER')
  AND teamid <> 'GER';
```

**🎯 What I Learned:**

* Conditional filtering across joined tables

---

### ✅ 9.

**📖 Problem:**
Show teamname and the total number of goals scored.

**💡 Query:**

```sql
SELECT teamname, COUNT(*)
FROM eteam
JOIN goal ON eteam.id = goal.teamid
GROUP BY teamname;
```

**🎯 What I Learned:**

* JOIN + GROUP BY

---

### ✅ 10.

**📖 Problem:**
Show the stadium and the number of goals scored in each stadium.

**💡 Query:**

```sql
SELECT stadium, COUNT(*)
FROM game
JOIN goal ON game.id = goal.matchid
GROUP BY stadium;
```

**🎯 What I Learned:**

* Aggregation after JOIN

---

### ✅ 11.

**📖 Problem:**
For every match involving 'POL', show the matchid, date and the number of goals scored.

**💡 Query:**

```sql
SELECT matchid, mdate, COUNT(*)
FROM game
JOIN goal ON game.id = goal.matchid
WHERE team1 = 'POL' OR team2 = 'POL'
GROUP BY matchid, mdate;
```

**🎯 What I Learned:**

* Grouping joined results

---

### ✅ 12.

**📖 Problem:**
For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.

**💡 Query:**

```sql
SELECT matchid, mdate, COUNT(*)
FROM game
JOIN goal ON game.id = goal.matchid
WHERE teamid = 'GER'
GROUP BY matchid, mdate;
```

**🎯 What I Learned:**

* Filtering before aggregation

---

### ✅ 13.

**📖 Problem:**
List every match with the goals scored by each team.

**💡 Query:**

```sql
SELECT mdate,
       team1,
       SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1,
       team2,
       SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2
FROM game
JOIN goal ON game.id = goal.matchid
GROUP BY mdate, team1, team2
ORDER BY mdate, team1, team2;
```

**🧾 Explanation:**
Used `CASE WHEN` to calculate scores per team.

**🎯 What I Learned:**

* Conditional aggregation
* Real-world reporting queries

---

## 🚀 Overall Learnings

* Understanding `JOIN` operations
* Connecting multiple tables using keys
* Using `JOIN` with `WHERE`, `GROUP BY`
* Writing aggregation queries across tables
* Using `CASE WHEN` for conditional logic

---

✨ *This module built a strong foundation in JOINs — a critical skill for real-world SQL.*
