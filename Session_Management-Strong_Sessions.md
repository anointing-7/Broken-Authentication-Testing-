## Session Management - Strong Sessions:

This vulnerability allowed me to acquire one user’s session ID and use it for another (hypothetical) user.
I opened the first browser (User 1/attacker)

<img width="975" height="494" alt="image" src="https://github.com/user-attachments/assets/ac1b0ebb-4df8-49cd-a312-c8be0aa69aaf" />

I captured the http request using Burp Suite.

<img width="975" height="451" alt="image" src="https://github.com/user-attachments/assets/e399ab91-03b2-493d-bcb2-76f547c53398" />

<img width="975" height="485" alt="image" src="https://github.com/user-attachments/assets/456b546a-f78a-48bd-ba9f-ab57c95fd2d5" />

I then opened another browser (User 2/victim)

<img width="975" height="496" alt="image" src="https://github.com/user-attachments/assets/f714444c-12e5-48d2-af87-93b4a3320736" />

In Burp Suite, I changed the attacker’s session identifier to the above PHPSESSID:6kj9e24rI731mf819st4kudo15 and submitted the request. 

<img width="975" height="448" alt="image" src="https://github.com/user-attachments/assets/a6078fbe-6722-4b46-8451-09ed3b6be6f8" />

<img width="975" height="455" alt="image" src="https://github.com/user-attachments/assets/74a3731b-8617-47e8-90b9-2ae905955345" />

Once I reloaded the attacker’s webpage, it now had the victim’s session ID. Meaning that the attacker was now using the victim’s session.

<img width="975" height="496" alt="image" src="https://github.com/user-attachments/assets/ebd107bd-8bf4-445d-a2ec-2701ecf8cc03" />

### The Potential Impacts of this vulnerability:
-	If an attacker is able to successfully use another user’s session ID, it means that the application may treat the attacker as the legitimate user associated with that session. As a result, the attacker could potentially gain unauthorized access to information and functionality available to that user, including personal or sensitive data.
-	Depending on the victim’s privileges, the attacker may also be able to view, modify, or delete information and perform actions on the user’s behalf.

<img width="510" height="314" alt="Capture (6)" src="https://github.com/user-attachments/assets/b57b1605-c9e1-403c-87b9-c16f55504287" />

### Severity: High

### Mitigation Strategies:
1.	Mark session cookies HTTP Only, Secure, and Same Site so they resist script access and only travel over TLS.
2.	Generate session IDs with a cryptographically strong random source — never sequential or guessable.
3.	Rotate/reissue the session ID at login and at any privilege change to defeat fixation attacks.
4.	Link user sessions to the device or IP address and require the user to log in again if there is a suspicious change.
5.	Expire sessions after a reasonable idle/absolute timeout and allow users to view/revoke active sessions.

### Conclusion:
The authentication testing exercises I conducted in bWAPP demonstrated how weaknesses in authentication and session management can affect the security of a web application. The tests identified several security issues, including an insecure login page, weak authentication controls that accepted credentials not present in the database, and susceptibility to credential stuffing attacks.
The Session ID in URL exercise further demonstrated the risks associated with exposing session identifiers through URLs, while the Strong Sessions exercise highlighted the importance of using unpredictable and securely generated session identifiers to prevent session-related attacks.
Overall, the exercises showed that authentication security extends beyond simply requiring a username and password. Secure authentication requires strong credential validation, protection against automated login attempts, secure session management, and properly generated session identifiers. Addressing these weaknesses can reduce the risk of unauthorized access and help protect user accounts and application data.


