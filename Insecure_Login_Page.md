In this project, I assessed various authentication vulnerabilities using Buggy Web Application (bWAPP), a deliberately vulnerable web application designed for security testing purposes. I then analyzed the potential impact of these vulnerabilities and suggested OWASP-aligned mitigation strategies.
## Project objective:
### Goal
Perform a controlled security assessment of authentication mechanisms in bWAPP, focusing on:
1.	Weak login mechanisms 
2.	Credential stuffing / automated credential attacks 
3.	Session fixation and session-management weaknesses 

### Tools Used:
-Docker.
-bWAPP
-Burp Suite.

In order for me to be able to conduct the targeted security assessments, I installed bWAPP on my localhost.
 
<img width="975" height="157" alt="image" src="https://github.com/user-attachments/assets/3c0f5023-9016-4219-b0b2-5a8f0001817a" />


### How the Application’s Normal Login Page Behaves:
Before I explored any of the vulnerabilities listed above, I tested the application to see how its authentication mechanism usually behaves and found the following:

1.	Clicking the logout option redirects a user back to the login page, which means the application terminates sessions successfully once a user is logged out.
2.	Once a user is logged out, trying to access the portal directly using the portal’s URL without first authenticating will lead the user back to the login page.
3.	When the wrong password is used, access to the portal is denied and an error message is generated.

## Insecure Login Page-Credentials exposed through client-side application code:
- This login page had a vulnerability that exposed user credentials in the HTML source code. When I inspected the code, I noticed that the credentials had been hardcoded directly into the page.
The credentials can be seen in the screenshot below:

<img width="975" height="521" alt="image" src="https://github.com/user-attachments/assets/0013d3f0-97ab-4340-b357-a827d1a533fd"/>

 Using those exposed credentials, I was able to successfully login.

 <img width="975" height="517" alt="image" src="https://github.com/user-attachments/assets/177b26ec-8681-4ed8-97cd-761873157b59" />

### How a Secure Application Should Behave:
-	A secure application should store users’ credentials on a web server and when users enter their credentials, the provided credentials should be verified against the application’s database.

### The Potential Impacts of this Vulnerability:
-	An attacker could simply inspect the page’s source code and find the credentials within the code, which would grant them unauthorized access into the application. Depending on the user’s permissions, they could access and steal sensitive information from the database.

<img width="491" height="294" alt="Capture(1)" src="https://github.com/user-attachments/assets/3be9fd7c-f2c3-4ab9-bee7-7acfa7127538" />

### Severity: Critical

### Mitigation Strategies:
1.	Remove hardcoded credentials. Never place usernames, passwords, API keys, or authentication secrets directly in HTML, JavaScript, or other client-side code.
2.	Review client-side code before deployment.
3.	Rotate exposed credentials. If credentials have already been hardcoded or exposed, immediately replace or rotate them and investigate where they may have been disclosed.
4.	Perform server-side authentication testing. The login page should send the user's credentials to a secure server-side authentication mechanism.
5.	Store passwords securely. Keep credentials in secure server-side configuration rather than source code.
6.	Apply multi-factor authentication to each account.










