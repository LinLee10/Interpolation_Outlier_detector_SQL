# SQL Interpolation & Outlier Detection

**Source:** Data Engineering (INFO 258) “Project 3: Time-Series Interpolation & Outlier Detection” 

A three-pass PostgreSQL pipeline that:

1. **Interpolates** missing sensor readings using linear averages of the previous and next values.  
2. **Smooths** the time series via rolling-window averages.  
3. **Flags** statistical outliers beyond ±3 σ for further review.

---

## Tech Stack

- PostgreSQL 13+  
- SQL window functions: `LAG()`, `LEAD()`, `AVG() OVER (ORDER BY …)`  
- Common Table Expressions (CTEs)  

---

## Usage

1. **Load your raw data**:
   ```sql
   CREATE TABLE sensor_data (
     id   SERIAL PRIMARY KEY,
     ts   TIMESTAMP NOT NULL,
     val  DOUBLE PRECISION
   );
   COPY sensor_data(ts, val) FROM 'sensor_readings.csv' CSV HEADER;
