[![CI](https://github.com/nogibjj/Eric_Ortega_Rodriguez_Mini_Project_6/actions/workflows/cicd.yml/badge.svg)](https://github.com/nogibjj/Eric_Ortega_Rodriguez_Mini_Project_6/actions/workflows/cicd.yml)
# Eric Ortega Rodriguez Mini Project 5

# Complex SQL Query for MySQL Database

## Overview
This project implements a complex SQL query involving **joins**, **aggregation**, and **sorting** using an external database. The external database used in this project is [Databricks](https://databricks.com/), and the query fetches data from two related tables (`Avengers` and `Battles`) to calculate the total number of appearances and battles per Avenger.

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
### 1. Python Script

### 2. Screenshots (See Below)
![#1:](image-4.png)
![#2:](image-2.png)
![#3:](image-3.png)
## References
https://github.com/nogibjj/sqlite-lab