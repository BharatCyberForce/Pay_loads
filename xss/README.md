# What is XSS?

XSS happens when untrusted input is rendered into a web page and executed as code in the victim’s browser. The attacker’s script runs with the same privileges as the site’s own scripts and can read/modify the DOM, send requests as the user, and more. 
MDN Web Docs

Three canonical types

Reflected XSS attacker supplies data (URL parameter) that is immediately reflected in the server response and executed in the victim’s browser.

Stored (persistent) XSS attacker stores malicious content on the server (forum post) so that every user who views it executes the payload.

DOM-based XSS vulnerability originates in client side code that writes untrusted data into DOM APIs (innerHTML) without sanitization; the server may be innocent. 
OWASP Cheat Sheet Series

# How XSS Works

An XSS vulnerability exists when a web application takes user input and includes it in the output HTML without properly sanitizing or encoding it.

## 1. Reflected XSS

This is the most common type of XSS. The malicious script is "reflected" off the web server, often in an error message, search result, or any other immediate response. The script is not stored on the server.

An attacker crafts a URL with a malicious payload and sends it to a victim.

```https://target.com/greeting.php?name=<script>alert('reflect');</script>```

When the victim clicks the link, their browser executes the script, causing a pop-up alert box. A real-world attack would replace this simple alert with code to steal cookies, perform actions on behalf of the user, or redirect them to a malicious site.

## 2. Stored XSS

This is the most dangerous type of XSS. The malicious script is permanently stored on the target server, for instance, in a database, a comment section, or a user profile.

How an attacker exploits it:

  An attacker submits a comment on a blog with a malicious payload: <script>alert('You have been hacked!');</script>.

  The server stores this comment in its database.

  Every time a user views that comment or visits the page where it's displayed, their browser retrieves the payload from the database and executes the malicious script.

## 3. DOM-based XSS

DOM (Document Object Model)-based XSS occurs entirely on the client side. The malicious script's execution is triggered by manipulating the page's DOM, rather than being a result of server-side code.

How an attacker exploits it:
An attacker manipulates a part of a URL, such as a URL fragment (#), which is then read by the page's JavaScript and written to the DOM.

```https://target.com/search.html#<script>alert('dom');</script>```

The malicious script is not sent to the server. The client-side JavaScript reads the fragment from the URL and injects it into the page's HTML, leading to execution.

Why This Matters for Bug Hunters

For bug hunters, XSS is a high-priority vulnerability. It can lead to:

  Session Hijacking: Stealing session cookies to impersonate a user.

  Sensitive Data Theft: Gaining access to private information.

  Malicious Redirection: Phishing the user by redirecting them to a fake login page.

  Cross-Site Request Forgery (CSRF): Forcing a user's browser to send authenticated requests on behalf of the attacker.
# How we can take advantage

Hacktivists or attackers may use XSS to:

Steal session tokens or other sensitive data (if cookies or tokens are accessible).

Perform actions as victims (automate requests using the victim’s credentials).

Deface pages or inject propaganda messages into public pages (stored XSS).

Phish or social-engineer inject malicious UI that prompts victims to enter secrets.

## Reflected XSS

Reflected XSS is often used for targeted attacks or to spread a message widely through social engineering. we can create a malicious URL with a payload that, when clicked by a victim, executes in their browser.

  Social Engineering: They can use phishing campaigns to send a malicious link to a specific target, like a government official or a corporate leader. When the target clicks the link, the payload runs, allowing the hacktivist to steal cookies or hijack their session.

  Disruptive Messages: Hacktivists can use this to create temporary pop-ups or redirects on a legitimate site that display their political message to a wide audience, though the effect is non-persistent and only lasts for the single click.

## Stored XSS

Stored XSS is the most powerful method for hacktivists because the malicious payload is permanently embedded into the website. It affects every user who views the compromised page.

  Website Defacement: This is a classic hacktivist tactic. By injecting a script into a comment section, a forum, or even a news article, they can alter the page HTML to display a political message or a symbol. This virtual defacement is a visible form of protest.

  Mass Message Dissemination: A hacktivist group can inject code into a popular website to automatically display their manifesto or propaganda to every user. This is a highly effective way to get their message out without having to engage in individual phishing attacks.

  Data Exfiltration on a Mass Scale: If the stored XSS payload is designed to steal data like session cookies or credentials, it can be used to harvest sensitive information from a large number of users over time. This data can then be used to further their cause, such as by leaking personal information of government employees or corporate executives.

## DOM-based XSS

DOM-based XSS can be a more subtle tool for hacktivists. While it's also non-persistent like reflected XSS, it doesn't require the malicious code to be sent to the server.

  Targeted Manipulation: A hacktivist can create a URL that, when clicked, manipulates the client-side JavaScript of a web page to display disinformation or alter content for a specific user. This can be used to spread propaganda or create a convincing but fake narrative, as the changes appear to be coming from the legitimate website itself.

  Bypassing Server-Side Protections: Since the payload is never sent to the server, this type of XSS can bypass many server-side firewalls and intrusion detection systems. This makes it a stealthy and effective method for hacktivist groups who want to avoid detection.


---

## ⚠️ Warning

This document is provided **for educational and real world attacks examples**.  

- **Do not use this information to attack on anyone sits unauthorize**  
- Testing should only be done on systems you are authorized to assess.  
- Any misuse of these techniques against third-party applications without permission is unethical and may be illegal.  

The purpose of this guide is to help the community **reduce security risks** and **increase awareness**
