# Hidden Deep Into my Heart

# Scenario

![image.png](6bc85cc6-2163-4055-87cd-9c7063c27f97.png)

# Solution

Access : [http://10.66.188.200:5000/](http://10.66.188.200:5000/) , appears like a normal site 

![image.png](image.png)

Let’s check `/robots.txt` 

![image.png](image%201.png)

Let’s dig more and access at `/cupids_secret_vault/`

![image.png](image%202.png)

Let’s enumerate if there is hidden directories !!

```bash
sudo dirsearch -u http://10.66.188.200:5000/cupids_secret_vault

[14:39:52] 200 -    2KB - /cupids_secret_vault/administrator
```

We found `/cupids_secret_vault/administrator` accessible so let’s try that, probably that’s gonna be our login page

![image.png](de797fa8-fd5a-4dc0-b491-4cdd13c9bfbd.png)

at `/robots.txt` remember we found a comment that could be probably the password , and the username let’s try something like `admin`  

→ **Login Creds :** `admin:cupid_arrow_2026!!!`

![image.png](image%203.png)

There you go we found our flag!! , try it for yourself , of course im not gonna show you the flag 😊
