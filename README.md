[![CI](https://github.com/nogibjj/Eric_Ortega_Rodriguez_Mini_Project_6/actions/workflows/cicd.yml/badge.svg)](https://github.com/nogibjj/Eric_Ortega_Rodriguez_Mini_Project_6/actions/workflows/cicd.yml)
# Eric Ortega Rodriguez Mini Project 6

# Complex SQL Query for MySQL Database

## Overview
This project implements a complex SQL query involving **joins**, **aggregation**, and **sorting** using an external database. The external database used in this project is [Databricks](https://databricks.com/), and the query fetches data from two related tables (`Avengers` and `Battles`) to calculate the total number of appearances and battles per Avenger. The I used can be found [here.](https://github.com/fivethirtyeight/data/tree/refs/heads/master/avengers)

## Requirements
1. **SQL Query**: Design and implement a complex SQL query that:
   - Joins data from multiple tables.
   - Aggregates data to compute totals.
   - Sorts the results based on specific criteria.

2. **Explanation**: Provide detailed documentation explaining what the query does and the expected results.

3. **CI/CD Pipeline**: Implement a basic Continuous Integration/Continuous Deployment (CI/CD) pipeline that automatically runs tests and ensures the query executes without errors.

4. **README**: This document explains the query, its purpose, and how to run it.

---

## Query Explanation

The following SQL query was designed for a **MySQL-compatible** database (Databricks in this case). It retrieves information about Avengers and their battle history, joining two tables (`Avengers` and `Battles`) to calculate the total number of battles each Avenger has participated in, as well as their total appearances in comics. The results are sorted by the number of battles and the number of appearances.

### SQL Query:

```sql
SELECT 
    a.`Name/Alias`, 
    SUM(a.Appearances) AS total_appearances, 
    COUNT(b.battle_id) AS total_battles
FROM 
    Avengers a
JOIN 
    Battles b ON a.avenger_id = b.avenger_id
GROUP BY 
    a.`Name/Alias`
HAVING 
    SUM(a.Appearances) > 100  -- Only Avengers with more than 100 appearances
ORDER BY 
    total_battles DESC, total_appearances DESC;

## Project Breakdown

```
├── .devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
│
├── .github/
│   └── workflows/
│       └── cicd.yml
│
├── data/
│   ├── avengers.csv
│   ├── avengers.db
│   ├── empty_avengers.db
│   ├── image-1.png
│   ├── image-2.png
│   ├── image-3.png
│   └── image-4.png
│
├── mylib/
│   ├── __pycache__/
│   │   ├── __init__.cpython-312.pyc
│   │   ├── extract.cpython-312.pyc
│   │   ├── query.cpython-312.pyc
│   │   └── transform_load.cpython-312.pyc
│   ├── __init__.py
│   ├── extract.py
│   ├── query.py
│   └── transform_load.py
│
├── .gitignore
├── Dockerfile
├── image.png
├── main.py
├── Makefile
├── README.md
├── requirements.txt
├── setup.sh
├── test_main.py
└── test_avengers.db

```

## Deliverables 
### 1. SQL query
### 2. Written or video explanation of the query

# Written Explanation of the SQL Query

This query is designed to retrieve data about the Avengers and their participation in battles. The main purpose of the query is to calculate two key metrics for each Avenger:

1. **Total number of comic book appearances**.
2. **Total number of battles they have fought**.

Additionally, the query filters out any Avengers with fewer than 100 comic book appearances, and it sorts the results based on the total number of battles fought (from most to least) and, secondarily, by total appearances.

### Query Breakdown:

1. **FROM and JOIN Clauses**:
   - The query is pulling data from two tables: `Avengers` and `Battles`.
   - The `JOIN` clause is used to link the two tables using the `avenger_id` field, which exists in both tables. This allows the query to combine information about each Avenger from the `Avengers` table with information about their participation in battles from the `Battles` table.

2. **SELECT Clause**:
   - `a.Name/Alias`: This selects the name or alias of the Avenger from the `Avengers` table.
   - `SUM(a.Appearances) AS total_appearances`: This sums the number of comic book appearances for each Avenger. The `SUM()` function aggregates the values in the `Appearances` column for each Avenger.
   - `COUNT(b.battle_id) AS total_battles`: This counts the number of battles that each Avenger has participated in, based on the number of `battle_id` entries in the `Battles` table.

3. **GROUP BY Clause**:
   - The query groups the results by `a.Name/Alias`. This means that for each unique Avenger, it calculates the total appearances and battles.

4. **HAVING Clause**:
   - The `HAVING` clause filters out Avengers who have appeared in fewer than 100 comic books. The query only returns Avengers with 100 or more appearances.
   - This filter is applied after the aggregation, meaning that only Avengers with 100 or more total appearances (as calculated by the `SUM(a.Appearances)`) are included in the results.

5. **ORDER BY Clause**:
   - The results are first sorted by `total_battles DESC`, meaning that Avengers with the highest number of battles are listed first.
   - If two Avengers have the same number of battles, they are further sorted by `total_appearances DESC`, so Avengers with more appearances are listed higher.

### Example Scenario:

Let’s assume the `Avengers` table contains the following data:

| avenger_id | Name/Alias      | Appearances |
|------------|-----------------|-------------|
| 1          | Iron Man        | 3000        |
| 2          | Captain America | 2800        |
| 3          | Black Widow     | 800         |

And the `Battles` table contains:

| battle_id | avenger_id |
|-----------|------------|
| 1         | 1          |
| 2         | 1          |
| 3         | 2          |
| 4         | 2          |
| 5         | 3          |

The query would:
- Join these two tables using `avenger_id`.
- Calculate that Iron Man has 3000 appearances and 2 battles, Captain America has 2800 appearances and 2 battles, and Black Widow has 800 appearances and 1 battle.
- Filter out Black Widow since she has fewer than 100 comic book appearances.
- Return Iron Man and Captain America, sorted by their number of battles and appearances.

### Expected Results:

| Name/Alias      | total_appearances | total_battles |
|-----------------|-------------------|---------------|
| Iron Man        | 3000              | 2             |
| Captain America | 2800              | 2             |

In this case, the results show that both Iron Man and Captain America have fought in 2 battles, but Iron Man is listed first because he has more comic book appearances.

### Summary:

This query provides valuable insights into the popularity and involvement of Avengers based on their battle history and overall comic book presence, prioritizing those with high participation in battles and appearances.
