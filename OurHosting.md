# CTF Event Setup Using Nginx

This guide explains how to set up **CTFd** and multiple challenge servers using **Nginx** on a LAN environment. All contestants will access services through subdomains on the same network.

---

## Nginx Configuration

### CTFd

```nginx
server {
    listen 80;
    server_name ctfd.prayag.ai;

    location / {
        proxy_pass http://127.0.0.1:4000;   # CTFd backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
Challenge 1
nginx
Copy code
server {
    listen 80;
    server_name chal1.prayag.ai;

    location / {
        proxy_pass http://127.0.0.1:5000;   # Challenge 1 backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
Challenge 2
nginx
Copy code
server {
    listen 80;
    server_name chal2.prayag.ai;

    location / {
        proxy_pass http://127.0.0.1:6000;   # Challenge 2 backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
Contestant Machine Setup
Add the following entries to each contestant's /etc/hosts file:

Copy code
192.168.1.35 ctfd.prayag.ai
192.168.1.35 chal1.prayag.ai
192.168.1.35 chal2.prayag.ai
Note: 192.168.1.35 is the server's LAN IP.

Server Environment Setup
Create Conda Environment
bash
Copy code
conda create -n ctfd python=3.11
conda activate ctfd
Install Requirements
bash
Copy code
pip install -r requirements.txt
Running the Services
Activate the environment:

bash
Copy code
conda activate ctfd
Start CTFd:

bash
Copy code
python serve.py
Start other challenge servers on their respective ports (5000, 6000, etc.) as needed.

Access URLs
CTFd: http://ctfd.prayag.ai

Challenge 1: http://chal1.prayag.ai

Challenge 2: http://chal2.prayag.ai

pgsql
Copy code

You can save this as `README.md` and push it to GitHub. It’s fully copy-pasteable and renders cleanly.  

If you want, I can also make a **template with 5–10 challenges** ready to drop into Nginx for the event, so you don’t have to edit manually. Do you want me to do that?







Ask ChatGPT




