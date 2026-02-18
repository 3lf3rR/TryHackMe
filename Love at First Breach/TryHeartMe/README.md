# TryHeartMe

# Scenario

![image.png](image.png)

# Solution

Check the website

![image.png](image%201.png)

It’s a shop , Let’s register as test user with creds — `test@thm.com:testtest` 

Once registered inspect the cookies with `F12` muscle 

![image.png](image%202.png)

---

## JWT Token ?

- **JWT** is a **token** that contains a small amount of **user-related information**, like your **user ID** or **role** (e.g., admin, user).
- It’s usually sent from a **server** to a **client** (browser or app) after logging in or performing some action, and the client can use this token for **subsequent requests** without having to log in again.
- It’s **self-contained** — all the information the server needs is inside the token itself, so the server doesn’t have to look up the user in a database every time.

---

Let’s get back to it i have a site for you to help decode the token — [https://www.jwt.io/](https://www.jwt.io/)

![image.png](image%203.png)

Then hit `JWT Encoder` and modify the payload

```bash
{
  "email": "test@thm.com",
  "role": "user",
  "credits": 0,
  "iat": 1771275268,
  "theme": "valentine"
}
```

We’re gonna simply change `role → admin` and `credits → 9999` 

```bash
{
  "email": "test@thm.com",
  "role": "admin",
  "credits": 9999,
  "iat": 1771275268,
  "theme": "valentine"
}
```

![image.png](image%204.png)

Paste the new **JWT token** in here 

![image.png](image%205.png)

Then simply refresh the page

![image.png](image%206.png)

Boom a new item that looks like our flag , and most importantly we became admin , let’s buy the new item we have `credits = 9999` 

![image.png](image%207.png)

![image.png](image%208.png)

And you’re Finished 😊
