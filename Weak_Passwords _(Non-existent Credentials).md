## Weak Passwords:

I accessed the database to find the list of users.

<img width="975" height="307" alt="image" src="https://github.com/user-attachments/assets/bb6ce1a0-4eba-4fed-810a-47950b141e23" />

I tested several well-known passwords, and when a password failed, the application returned the response below:

  <img width="975" height="495" alt="image" src="https://github.com/user-attachments/assets/363b24d8-ca1f-40ac-8125-773985c7ac80" />

After trying a set of known credentials where the password was the same as the username, I was able to successfully login.

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/c74da0bf-c0c4-48ba-a0ad-ce80940d1fdb" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/32ccf290-bbd8-4159-8485-b7bcbbc9ebb1" />

Interestingly, the ‘test’ username and password do not exist in the database, which means that this vulnerability allowed authentication without properly validating the credentials against the entries in the database.

### The Potential Impacts of this Vulnerability:
-	An attacker could take advantage of this vulnerability to gain unauthorized access into the application. 	If they’re assigned a valid session, they may be able to view information intended only for legitimate users. Whereas if they’re assigned an administrative or privileged session, they could potentially access administrative functions.
-	They may be able to perform actions as an authenticated user, such as modifying records, submitting transactions, or changing account information.
-	Actions performed using a nonexistent account may make it difficult to reliably associate activity with a legitimate user.

<img width="1071" height="652" alt="image" src="https://github.com/user-attachments/assets/87667547-4465-4d9d-bcb5-9659685fc364" />


### Severity: Critical

## Mitigation Strategies:
1.	Perform server-side credential validation.
2.	Reject nonexistent accounts.
3.	Enforce authorization after authentication. Even if authentication succeeds, the application should verify that the authenticated user has permission to perform the requested action.
4.	Avoid responses that reveal whether a username exists.
5.	Remove development/test authentication mechanisms from production builds.
