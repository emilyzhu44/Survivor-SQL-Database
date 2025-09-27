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

![ERD Diagram]([assets/ERD.png](https://github.com/emilyzhu44/Survivor-SQL-Database/blob/main/Survivor%20ERD%20diagram.pdf))
*(Replace with your ERD image in the repo — usually kept in an `assets/` or `images/` folder.)*

---

## 🧮 Example Queries & Insights

### 1. Players who did not make top 10

```sql
SELECT Name, Placement
FROM Player
WHERE Placement > 10;
```

✅ Shows which contestants were eliminated early, useful for analyzing underperformance trends.

---

### 2. Business majors with season & placement

```sql
SELECT P.Name, P.Major, S.SeasonName, P.Placement
FROM Player P
JOIN Tribe T ON P.TribeID = T.TribeID
JOIN Season S ON T.SeasonID = S.SeasonID
WHERE P.Major = 'Business';
```

✅ Highlights contestants with a business background and how well they performed.

---

### 3. Count of players per tribe per season

```sql
SELECT S.SeasonName, T.TribeName, COUNT(P.PlayerID) AS PlayerCount
FROM Player P
JOIN Tribe T ON P.TribeID = T.TribeID
JOIN Season S ON T.SeasonID = S.SeasonID
GROUP BY S.SeasonName, T.TribeName;
```

✅ Provides an overview of team sizes — useful for balancing or fairness analysis.

---

### 4. Players with their tribe names

```sql
SELECT P.Name, T.TribeName
FROM Player P
JOIN Tribe T ON P.TribeID = T.TribeID;
```

✅ Maps each contestant to their tribe — a simple but foundational query for many analyses.

---

### 5. First winner of Survivor

```sql
SELECT Winner
FROM Season
ORDER BY StartDate ASC
LIMIT 1;
```

✅ Returns the very first winner in Survivor history.

---

## 📊 Business Relevance

These queries mirror common business analysis tasks:

* **Segmentation** (top performers vs. underperformers)
* **Demographic analysis** (e.g., major/field of study)
* **Aggregations** (counts and groupings per category)
* **Entity mapping** (people to teams, products to categories)
* **Historical trends** (first events, earliest outcomes)

---

## 🚀 How to Run

1. Clone the repository:

```bash
git clone https://github.com/yourusername/survivor-database.git
cd survivor-database
```

2. Import the SQL scripts into your MySQL environment:

```bash
mysql -u root -p < create_schema.sql
mysql -u root -p < populate_data.sql
mysql -u root -p < queries.sql
```

3. Run the queries to generate insights.

---

