# Auth bypass via SQL injection

​A common and impactful demonstration of SQLi is an authentication bypass. This allows an attacker to log in as a legitimate user (often an administrator) without knowing the correct password.
---

## How it Works
​The vulnerability occurs when a web application uses user-supplied input directly in an SQL query without proper sanitization. A typical login form might construct a query like this:
If the app builds the database query by inserting raw user input into the SQL statement, the input can change the logic the database executes. In effect the attacker is not guessing a password, they are changing the test the application runs so the test passes even with wrong or unknown credentials.

```
SELECT * FROM users WHERE username = 'user input' AND password = 'password input';
```
a specific string into the username or password fields to manipulate this query. For example, if a user enters ' OR '1'='1 into the password field, the resulting SQL query could become:

```
SELECT * FROM users WHERE username = 'admin' AND password = '' OR '1'='1';
```
Because '1'='1' is always true, the WHERE clause becomes true, allowing the query to return a valid user record, often the first one in the database (which is typically an admin account). The application then grants access, bypassing the need for a correct password.

---
## Common Payload
​The payload you provided, '" OR "'=', is a classic example of this technique. Let's break down how it works:
​The ' character closes the string for the password field.
​The OR keyword introduces a new condition.
​The '=' part creates a condition that is always true.
​This essentially transforms the query's logic from "find a user with a specific username AND password" to "find a user with a specific username OR a condition that is always true."

