# Web Application Security - Task 3

Overview

This project focuses on identifying and exploiting common web application vulnerabilities based on OWASP Top 10 in a controlled lab environment.

The lab was performed using Kali Linux and DVWA (Damn Vulnerable Web Application) to simulate real-world attack scenarios and demonstrate mitigation techniques.

Objectives

-- Identify and exploit OWASP Top 10 vulnerabilities  
-- Understand real-world attack techniques  
-- Implement mitigation strategies for each vulnerability  

Tools & Technologies

-- Kali Linux  
-- DVWA (Damn Vulnerable Web Application)  
-- Burp Suite  
-- Apache Server  
-- MySQL Database  
-- Web Browser  

Vulnerabilities Covered

 1. SQL Injection (SQLi)
-- Extracted usernames and passwords from database  
-- Demonstrated authentication bypass  

 Mitigation:
-- Prepared Statements  
-- Parameterized Queries  
-- Input Validation  

2. Cross-Site Scripting (XSS)

Stored XSS
-- Injected malicious script stored in the database  

Reflected XSS
-- Injected script via URL parameters  

 Mitigation:
-- Input Sanitization  
-- Output Encoding  
-- Content Security Policy (CSP)  

3. Cross-Site Request Forgery (CSRF)
-- Created malicious request to change user password  

 Mitigation:
-- CSRF Tokens  
-- SameSite Cookies  

4. File Inclusion Attacks

Local File Inclusion (LFI)
-- Accessed sensitive system files  

Remote File Inclusion (RFI)
-- Executed external malicious code  

 Mitigation:
-- Input Validation  
-- Restrict File Paths  
-- Disable Remote File Inclusion  

5. Burp Suite (Advanced Testing)
-- Intercepted and modified HTTP requests  
-- Performed fuzzing using Intruder  

6. Web Security Headers

-- Analyzed using securityheaders.com  

 Implemented:
-- Content-Security-Policy  
-- X-Frame-Options  
-- X-XSS-Protection  


Methodology

-- Lab setup and DVWA configuration  
-- Vulnerability identification  
-- Exploitation of vulnerabilities  
-- Analysis of impact  
-- Implementation of mitigation techniques  


Conclusion

This project demonstrates how web applications can be vulnerable to common attacks and highlights the importance of implementing proper security controls to prevent exploitation.
