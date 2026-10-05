## Session Management-Session ID Exposed in URL

This vulnerability allows the user’s session identifier to be seen in the URL instead of being hidden in a cookie.

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/5fa1bd82-e5bc-40b0-8f0c-aaa3d41f722f" />

I copied the URL, opened another browser tab and pasted the copied URL. I was granted access to the page without needing any authentication, meaning I was now using the previous browser’s session.

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/bbf2cea2-dbbe-45c6-82ac-4a9dba2134de" />

### The Potential Impacts of this vulnerability:
-	An attacker could potentially monitor network traffic and intercept requests containing the session ID in the URL. If the session ID is exposed, the attacker could use it to hijack the victim’s active session, potentially gaining unauthorized access to the victim’s information and performing actions on their behalf.

<img width="515" height="325" alt="Capture (5)" src="https://github.com/user-attachments/assets/f08fc0a2-f8f6-47de-a774-b423b00164e9" />

### Severity: Medium
### Mitigation Strategies:
1.	Place session tokens in a cookie (HTTP Only, Secure, Same Site) or an Authorization header — never in the URL.
2.	Invalidate the session ID immediately if one is ever detected in a URL, log, or Referrer header.
3.	Set a strong Referrer-Policy so URLs (and any tokens in them) aren't leaked to third-party page resources.
4.	Scrub existing logs, proxies, and analytics tools of any historical query-string session identifiers.
5.	Keep session lifetimes short and require re-authentication for sensitive actions.

