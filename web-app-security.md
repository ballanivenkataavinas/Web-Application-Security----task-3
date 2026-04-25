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

---

-- All testing performed in a controlled lab environment  
