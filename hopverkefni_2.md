# Hóverkefni
```sql
/* =================
   Database creation
   ================= */

CREATE DATABASE 1611012220_hopverkefni2;
USE 1611012220_hopverkefni2;


CREATE TABLE job (
    job_code        CHAR(3) PRIMARY KEY NOT NULL,
    job_description VARCHAR(55),
    job_chg_hour    DECIMAL(10,2),
    job_last_update DATE
);

CREATE TABLE employee (
    emp_num         CHAR(3) PRIMARY KEY NOT NULL,
    emp_lname       VARCHAR(15),
    emp_fname       VARCHAR(15),
    emp_initial     CHAR(1),
    emp_hiredate    DATE,
    job_code        CHAR(3),
    emp_year        INT,
    FOREIGN KEY (job_code) REFERENCES job(job_code)
);

CREATE TABLE project (
    proj_num        CHAR(3) PRIMARY KEY NOT NULL,
    proj_name       VARCHAR(25),
    proj_value      DECIMAL(10,2),
    proj_balance    DECIMAL(10,2),
    emp_num         CHAR(3),
    FOREIGN KEY (emp_num) REFERENCES employee(emp_num)
);

CREATE TABLE assignment (
    assign_num      INT PRIMARY KEY NOT NULL,
    assign_date     DATE,
    proj_num        CHAR(3),
    emp_num         CHAR(3),
    assign_job      CHAR(3),
    assign_chg_hr   DECIMAL(10,2),
    assign_hours    DECIMAL(10,2),
    assign_charge   DECIMAL(10,2) -- assign_chg_hr * asssign_hours
    FOREIGN KEY (proj_num)      REFERENCES project(proj_num),
    FOREIGN KEY (emp_num)       REFERENCES employee(emp_num),
    FOREIGN KEY (assign_job)    REFERENCES job(job_code)
);

/* =============
   Insert values
   ============= */

INSERT INTO employee VALUES
    ('101', 'News', 'John', 'G', '2000-11-08', '502', 04),
    ('102', 'Senior', 'David', 'H', '1989-07-12', '501', 15),
    ('103', 'Arbough', 'June', 'E', '1996-12-01', '503', 08),
    ('104', 'Ramoras', 'Anne', 'K', '1987-11-15', '501', 17),
    ('105', 'Johnson', 'Alice', 'K', '1993-02-01', '502', 12),
    ('106', 'Smithfield', 'William', NULL, '2004-06-22', '500', 12),
    ('107', 'Alonzo', 'Maria', 'D', '1993-10-10', '500', 00),
    ('108', 'Washington', 'Ralph', 'B', '1991-08-22', '501', 11),
    ('109', 'Smith', 'Larry', 'W', '1997-07-18', '501', 13),
    ('110', 'Olenko', 'Gerald', 'A', '1995-12-11', '505', 07),
    ('111', 'Wabash', 'Geoff', 'B', '1991-04-04', '506', 09),
    ('112', 'Smithson', 'Darlene', 'M', '1994-10-23', '507', 14),
    ('113', 'Joenbrood', 'Delbert', 'K', '1996-11-15', '508', 10),
    ('114', 'Jones', 'Annelise', NULL, '1993-07-20', '508', 08),
    ('115', 'Bawangi', 'Travis', 'B', '1992-01-25', '510', 11),
    ('116', 'Pratt', 'Gerald', 'L', '1997-03-05', '509', 13),
    ('117', 'Williamson', 'Angie', 'H', '1996-06-19', '510', 08),
    ('118', 'Frommer', 'James', 'J', '2005-01-04', '502', 00);

INSERT INTO project VALUES
    ('15', 'Evergreen', 1453500.00, 1002350.00, '103'),
    ('18', 'Amber Wave', 3500500.00, 2110346.00, '108'),
    ('22', 'Rolling Tide', 805000.00, 500345.20, '102'),
    ('25', 'Starflight', 2650500.00, 230980.00, '107');

INSERT INTO assignment VALUES
    (1001, '2007-03-22', '18', '103', '503', 84.50, 3.5, 295.75),
    (1002, '2007-03-22', '22', '117', '509', 34.55, 4.2, 145.11),
    (1003, '2007-03-22', '18', '117', '509', 34.55, 2.0, 69.10),
    (1004, '2007-03-22', '18', '103', '503', 84.50, 5.9, 498.55),
    (1005, '2007-03-22', '25', '108', '501', 96.75, 2.2, 212.85),
    (1006, '2007-03-22', '22', '104', '501', 96.75, 4.2, 406.35),
    (1007, '2007-03-22', '25', '113', '508', 50.75, 3.8, 192.85),
    (1008, '2007-03-22', '18', '103', '503', 84.50, 0.9, 76.05),
    (1009, '2007-03-23', '15', '115', '501', 96.75, 5.6, 541.81),
    (1010, '2007-03-23', '15', '117', '509', 34.55, 2.6, 82.92),
    (1011, '2007-03-23', '25', '105', '502', 105.00, 4.3, 451.50),
    (1012, '2007-03-23', '18', '108', '501', 96.75, 3.4, 328.95),
    (1013, '2007-03-23', '25', '115', '501', 96.75, 2.0, 193.50),
    (1014, '2007-03-23', '22', '104', '503', 96.75, 2.8, 270.90),
    (1015, '2007-03-23', '15', '103', '502', 84.50, 6.1, 515.45),
    (1016, '2007-03-23', '22', '105', '509', 105.00, 4.7, 493.50),
    (1017, '2007-03-23', '18', '117', '509', 34.55, 3.8, 131.29),
    (1018, '2007-03-23', '25', '117', '501', 34.55, 2.2, 76.01),
    (1019, '2007-03-23', '25', '104', '502', 110.50, 4.9, 541.45),
    (1020, '2007-03-24', '15', '101', '501', 125.00, 3.1, 387.50),
    (1021, '2007-03-24', '22', '108', '501', 110.50, 2.7, 298.35),
    (1022, '2007-03-24', '22', '115', '502', 110.50, 4.9, 541.45),
    (1023, '2007-03-24', '22', '105', '503', 125.00, 3.5, 437.50),
    (1024, '2007-03-24', '15', '105', '509', 84.50, 3.3, 278.85),
    (1025, '2007-03-24', '18', '117', '502', 34.55, 4.2, 145.11);

INSERT INTO job VALUES
    ('500', 'Programmer', 35.75, '2006-11-20'),
    ('501', 'System Analyst', 96.75, '2006-11-20'),
    ('502', 'Database Designer', 125.00, '2007-03-24'),
    ('503', 'Electrical Engineers', 84.50, '2007-11-20'),
    ('504', 'Mechanical Engineer', 67.90, '2007-11-20'),
    ('505', 'Civil Engineers', 55.78, '2007-11-20'),
    ('506', 'Clerical Support', 26.87, '2007-11-20'),
    ('507', 'DSS Analyst', 45.95, '2007-11-20'),
    ('508', 'Application Designer', 48.10, '2007-03-24'),
    ('509', 'BioTechnician', 34.55, '2007-11-20'),
    ('510', 'General Support', 18.36, '2007-11-20');
```
1.
```sql
CREATE TABLE emp_1 AS SELECT * FROM employee;
```
2.
```sql
INSERT INTO emp_1 VALUES
    ('101', 'News', 'John', 'G', '2000-11-08', '502', 04),
    ('102', 'Senior', 'David', 'H', '1989-07-12', '501', 15);
```

3. 
```sql
SELECT * FROM emp_1 WHERE job_code = 502;
```

4.
```sql
COMMIT;
```

5.
```sql
UPDATE emp_1 SET job_code = '501' WHERE emp_num = '107';
UPDATE emp_1 SET job_code = '500' WHERE emp_num = '107';
```

6.
```sql
DELETE FROM emp_1
WHERE emp_fname = 'William' AND emp_lname = 'Smithfield' AND job_code = '500';
```

7.
```sql
ROLLBACK;
```

8.
```sql
CREATE TABLE emp_2 AS (
    SELECT * FROM emp_1
);
ALTER TABLE emp_2
ADD emp_pct DECIMAL(4,2),
ADD proj_num CHAR(3);
```

9.
```sql
UPDATE emp_2 SET emp_pct = 3.85 WHERE emp_num = '103';
UPDATE emp_2 SET emp_pct = 5.00 WHERE emp_num = '101';
UPDATE emp_2 SET emp_pct = 8.00 WHERE emp_num = '102';
UPDATE emp_2 SET emp_pct = 10.00 WHERE emp_num = '104';
UPDATE emp_2 SET emp_pct = 5.00 WHERE emp_num = '105';
UPDATE emp_2 SET emp_pct = 6.20 WHERE emp_num = '106';
UPDATE emp_2 SET emp_pct = 5.15 WHERE emp_num = '107';
UPDATE emp_2 SET emp_pct = 10.00 WHERE emp_num = '108';
UPDATE emp_2 SET emp_pct = 2.00 WHERE emp_num = '109';
```
10.
```sql
UPDATE emp_2 SET proj_num = '18' WHERE job_code = '500';
```
11.
```sql
UPDATE emp_2 SET proj_num = '25' WHERE job_code >= '502';
```
12.
```sql
UPDATE emp_2 SET proj_num = '14' WHERE emp_hiredate <= '1994-01-01' && job_code >= '501';
```
13.
```sql
CREATE TEMPORARY TABLE temp_1 SELECT emp_num, emp_pct FROM emp_2;
```
14.
```sql
IF(OBJECT_ID('tempdb..#temp_1') IS NOT NULL)
BEGIN
    DROP TABLE temp_1
END
-- DROP TABLE temp_1;
```
15.
```sql
SELECT * FROM emp_2 WHERE emp_lname LIKE 'Smith%';
```
16.
```sql
SELECT proj_name,
       proj_value,
       proj_balance,
       employee.emp_lname,
       emp_fname,
       emp_initial,
       employee.job_code,
       job.job_description,
       job.job_chg_hour
FROM project, employee, job
WHERE employee.emp_num = project.emp_num
AND	job.job_code = employee.job_code;
```
17.
```sql
CREATE VIEW rep_1 AS
SELECT proj_name,
       proj_value,
       proj_balance,
       employee.emp_lname,
       employee.emp_fname,
       employee.emp_initial,
       employee.job_code,
       job.job_description,
       job.job_chg_hour
FROM project, employee, job
WHERE employee.emp_num = project.emp_num
AND	job.job_code = employee.job_code;
```
18.
```sql
SELECT AVG(emp_pct)
FROM emp_2;
```
19.
```sql
SELECT * FROM emp_2
ORDER BY emp_pct ASC;
```
20.
```sql
SELECT DISTINCT proj_num FROM emp_2;
```
21.
```sql
UPDATE assignment
SET assign_charge = assign_chg_hr * assign_hours;
```
22.
```sql
SELECT assignment.emp_num, employee.emp_lname,
       SUM(assignment.assign_hours) AS sum_of_assign_hours,
       SUM(assignment.assign_charge) AS sum_of_assign_charge
FROM employee, assignment
WHERE employee.emp_num = assignment.emp_num
GROUP BY assignment.emp_num, employee.emp_lname;
```
23.
```sql
SELECT assignment.proj_num, 
       SUM(assignment.assign_hours) AS sum_of_assign_hours,
       SUM(assignment.assign_charge) AS sum_of_assign_charge
FROM assignment
GROUP BY assignment.proj_num
```
24.
```sql
SELECT SUM(sum_of_assign_hours), SUM(sum_of_assign_charge)
FROM (
    SELECT assignment.emp_num, employee.emp_lname,
        SUM(assignment.assign_hours) AS sum_of_assign_hours,
        SUM(assignment.assign_charge) AS sum_of_assign_charge
    FROM employee, assignment
    WHERE employee.emp_num = assignment.emp_num
    GROUP BY assignment.emp_num, employee.emp_lname
) AS t;
```
25.
```sql
SELECT SUM(sum_of_assign_hours), SUM(sum_of_assign_charge)
FROM (
    SELECT assignment.proj_num,
        SUM(assignment.assign_hours) AS sum_of_assign_hours,
        SUM(assignment.assign_charge) AS sum_of_assign_charge
    FROM assignment
    GROUP BY assignment.proj_num
) AS t;

```
