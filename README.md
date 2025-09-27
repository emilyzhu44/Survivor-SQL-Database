# Survivor Database Project

## Project Overview

This project models and analyzes data from the TV show *Survivor*. The goal was to design a normalized relational database, populate it with test data, and run queries to generate meaningful insights about players, tribes, challenges, and voting outcomes.

This project demonstrates skills including:

* Data modeling & normalization (entity-relationship design, primary/foreign keys)
* SQL database creation and schema design
* Data population and validation with realistic scenarios
* Writing queries to extract business insights

---

## Tools & Technologies

* **SQL / MySQL** – schema creation, inserts, queries
* **Database Normalization** – 3NF design principles
* **Data Analysis** – writing queries for reports & insights

---

## Database Design

The database schema was designed in 3rd Normal Form (3NF) to avoid redundancy and ensure efficient querying.

### Entity-Relationship Diagram (ERD)

![ERD Diagram](https://github.com/emilyzhu44/Survivor-SQL-Database/blob/main/Screenshot%202025-09-26%20202649.png)

---

## Example Queries & Insights

### 1. Players who did not make top 10

```sql
SELECT *
FROM Player
WHERE Placement > 11;
```

Shows which contestants were eliminated early, useful for analyzing underperformance trends.

---

### 2. Business majors with season & placement

```sql
SELECT p.Name AS PlayerName, p.Major, p.Placement, s.SeasonName
FROM Player p JOIN Tribe t Join Season s
ON p.TribeID = t.TribeID AND t.SeasonID = s.SeasonID
WHERE p.Major = 'Business';
```

Highlights contestants with a business background and how well they performed.

---

### 3. Count of players per tribe per season

```sql
SELECT
  s.SeasonName,
  t.TribeName,
  COUNT(p.PlayerID) AS PlayerCount
FROM
  Season s
JOIN
  Tribe T ON s.SeasonID = t.SeasonID
LEFT JOIN
  Player p ON t.TribeID=p.TribeID
GROUP BY
  s.SeasonName, T.TribeName
ORDER BY
  s.SeasonName, T.TribeName;
```

Provides an overview of team sizes — useful for balancing or fairness analysis.

---

### 4. Players with their tribe names

```sql
SELECT p.Name AS PlayerName, t.TribeName
FROM Player p JOIN Tribe t
On p.TribeID = t.TribeID;
```

Maps each contestant to their tribe — a simple but foundational query for many analyses.

---

### 5. First winner of Survivor

```sql
SELECT
  p.Name AS FirstWinnerName,
  p.Email AS FirstWinnerEmail,
  s.SeasonName AS FirstSeasonName,
  s.StartDate AS FirstSeasonStartDate,
  s.EndDate AS FirstSeasonDate
FROM
  Season s
JOIN
  Tribe t ON s.SeasonID=t.SeasonID
JOIN
  Player p ON p.Name=s.Winner
ORDER BY
  s.StartDate
Limit 1;
```

Returns the very first winner in Survivor history.

---

## Business Relevance

These queries mirror common business analysis tasks:

* **Segmentation** (top performers vs. underperformers)
* **Demographic analysis** (e.g., major/field of study)
* **Aggregations** (counts and groupings per category)
* **Entity mapping** (people to teams, products to categories)
* **Historical trends** (first events, earliest outcomes)

---

