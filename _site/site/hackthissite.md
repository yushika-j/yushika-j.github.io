# ***"HackThisSite.org"*** Penetration Testing Challenges

---

[Back to Projects](Projects.md)

---

## Project Overview

This project showcases penetration testing exercises completed on **HackThisSite** as part of the ***Commonwealth Bank Intro to Cybersecurity Program***. The primary goal was to identify, exploit, and document vulnerabilities across multiple web application levels, gaining hands-on experience in ethical hacking.

The project explores vulnerabilities like weak input validation, insecure encryption, and flawed authentication mechanisms, using techniques such as JavaScript tampering, SSI injection, and directory traversal. Each level provided insight into common web security issues and highlights the importance of secure application development practices.

---

## Objectives

1. Identify web application vulnerabilities, including weak input validation and improper authentication mechanisms.
2. Learn and apply penetration testing techniques, such as command injection and directory traversal.
3. Understand and exploit encryption vulnerabilities to assess the strength of cryptographic methods.
4. Enhance knowledge of securing server-side logic, including SSI injection and Apache configuration files.
5. Document all vulnerabilities, exploits, and provide security recommendations to improve the application’s security posture.

---

## Tools & Technologies

- **Languages**: HTML, JavaScript, PHP
- **Frameworks**: OWASP Top 10 (focus on A1: Injection, A3: Sensitive Data Exposure, A5: Broken Access Control)
- **Techniques**: HTML source code inspection, JavaScript manipulation, cookie tampering, SSI (Server Side Includes) injection, directory traversal, URL manipulation, command injection, form tampering, cryptographic reverse-engineering, and session hijacking
- **Cryptographic Analysis**: Pattern recognition for weak encryption algorithms
- **Web Server Analysis**: Apache configurations, `.htaccess` file security

---

## Challenges Completed

### **Level 1**
- **Vulnerability**: Password stored in the HTML source code.
- **Exploit**: By inspecting the page's HTML source code using Web Developer Tools, I found the password in a hidden input field. This exposed the password without any need for bypassing authentication. 
- **Recommendation**: Avoid storing sensitive data, such as passwords, client-side in HTML or JavaScript, and use server-side authentication mechanisms.

### **Level 2**
- **Vulnerability**: Missing password file allowed blank input to be accepted.
- **Exploit**: The password validation script relied on an external file that was missing. By submitting the form without entering any password, the server accepted the blank input and granted access. This demonstrated the lack of input validation and error handling. This exposed a major flaw in error handling, as the absence of critical files should prompt an error, not bypass the authentication process entirely.
- **Recommendation**: Implement proper error handling and file validation to ensure necessary files are available, and reject empty or invalid input.

### **Level 3**
- **Vulnerability**: Password stored in an accessible file (`password.php`).
- **Exploit**: I manually navigated to the `password.php` file by appending the file name to the URL. The file contained the password in plaintext, bypassing any form-based security measures.
- **Recommendation**: Restrict access to sensitive files using proper directory permissions and store sensitive data on the server-side.

### **Level 4**
- **Vulnerability**: Password recovery system allowed email address modification.
- **Exploit**: By using the browser's developer tools, I modified the email field in the password recovery form. I replaced the hardcoded email address with my own, intercepting the password reset information intended for another user.
- **Recommendation**: Ensure that all input fields, especially those handling sensitive data like email addresses, are validated server-side. Use secure methods for handling password recovery processes.

### **Level 5**
- **Vulnerability**: Similar to Level 4, the password recovery system allowed modification of the email address.
- **Exploit**: Just like how I did it in Level 4, for this level, I simply altered the email field and intercepted the password reminder by modifying the hardcoded email in the HTML. The repeated vulnerability shows how an attacker could consistently exploit the system to gain unauthorized access to user accounts.
- **Recommendation**: Implement server-side validation and secure input fields to prevent tampering. Use secure methods for handling password recovery processes.

### **Level 6**
- **Vulnerability**: Weak encryption algorithm allowed reverse-engineering.
- **Exploit**: The encryption used a predictable character-shifting pattern. By analyzing the input-output pairs of encrypted data, I reverse-engineered the algorithm and decrypted the password. This level demonstrated how weak, non-standard encryption techniques can be easily compromised by pattern recognition.
- **Recommendation**: Use modern cryptographic standards like AES or RSA, instead of weak custom encryption schemes.

### **Level 7**
- **Vulnerability**: Command injection allowed directory listing.
- **Exploit**: The calendar input field on the page was vulnerable to command injection. By appending commands to the input (e.g., 2024; ls -l), I was able to execute shell commands on the server. This provided a list of the directory contents, revealing the password file. This type of vulnerability is particularly dangerous as it allows an attacker to run arbitrary commands on the server, potentially compromising the entire system.
- **Recommendation**: Implement strict input sanitization, especially for input fields that interact with system commands, to prevent injection attacks. Limit user privileges on the server to reduce the impact of such attacks.

### **Level 8**
- **Vulnerability**: SSI (Server Side Includes) injection allowed directory traversal and file access.
- **Exploit**: By injecting an SSI command into the input field, I could traverse the file system and access files outside the intended directories. This type of attack exploits the server’s ability to process SSI commands embedded in user input, which can lead to unauthorized access to sensitive files and directories. By injecting the right commands, I navigated through the file system to locate and retrieve the password file.
- **Recommendation**: Disable SSI in web applications and ensure input fields are properly sanitized.

### **Level 9**
- **Vulnerability**: Directory traversal via SSI allowed access to restricted files.
- **Exploit**: By manipulating the input field and specifying file paths, I was able to bypass the application’s directory restrictions and retrieve sensitive information stored in protected files. This demonstrated the danger of allowing unchecked input to interact with the server's file system.
- **Recommendation**: Implement strong input validation, restrict access to sensitive directories using proper permissions, and disable SSI processing to prevent exploitation.

### **Level 10**
- **Vulnerability**: Cookie manipulation allowed unauthorized access.
- **Exploit**: By modifying the value of an authorization cookie from "no" to "yes" using JavaScript, I was able to bypass authentication and gain access to restricted areas of the application. This type of vulnerability highlights the risks of relying on client-side cookies for critical security decisions without validating them on the server side.
- **Recommendation**: Use server-side validation for all authentication and authorization processes, and ensure that cookies used for security purposes are encrypted and cannot be easily manipulated.

### **Level 11**
- **Vulnerability**: Hidden directory and file accessible through Apache's `.htaccess` configurations.
- **Exploit**: This level involved navigating through directories based on clues provided in song lyrics and file names. By systematically altering the URL, I eventually located the .htaccess file, which contained instructions revealing a hidden file named "DaAnswer." Accessing this file provided the password. This demonstrated the importance of properly securing .htaccess files and ensuring that sensitive files and directories are not exposed through misconfigurations.
- **Recommendation**: Secure .htaccess files and ensure that hidden directories and files are properly protected by configuring directory permissions and access controls.

---

## Methodology

- **Reconnaissance**: Used tools such as Web Developer Tools and Burp Suite to identify potential vulnerabilities in HTML, JavaScript, and server configurations.
- **Exploitation**: Exploited vulnerabilities using techniques such as cookie tampering, directory traversal, and SSI injection to gain unauthorized access to sensitive files and data.
- **Documentation**: Each vulnerability was documented with a description of the exploit and detailed security recommendations to mitigate the issues.

---

## Findings

- **Input Validation**: Inadequate validation of user input exposed the application to various attacks, including command injection and email modification.
- **Encryption**: Weak encryption schemes were reverse-engineered, highlighting the risks of predictable encryption algorithms.
- **Authentication**: Client-side authentication mechanisms, such as cookie manipulation, were easily bypassed without server-side validation.
- **Directory Traversal**: Improper directory permissions allowed unauthorized access to sensitive files through directory traversal and SSI injection.

---

## Conclusion

The HackThisSite penetration testing exercise highlighted a variety of critical vulnerabilities, including weak input validation, flawed authentication, and poor encryption practices. By exploiting these vulnerabilities using techniques such as command injection, directory traversal, and cookie manipulation, I gained unauthorized access to restricted areas of the application. This exercise underscored the importance of strong input validation, server-side checks, and modern encryption methods to mitigate risks and protect sensitive data. Addressing these issues through secure development practices is crucial for enhancing the security posture of any web application.

This project provided invaluable hands-on experience with various penetration testing techniques, reinforcing my understanding of how web vulnerabilities are exploited in real-world scenarios. By learning to identify and address these vulnerabilities, I am better equipped to ensure that future applications are built with robust security controls, thereby reducing the risk of exploitation and strengthening overall application integrity.

---

[Back to Projects](Projects.md)


