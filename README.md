# Example Docker Lab Setup

This will build a lab with 3 boxes, a kali box, a ubuntu container running `sshd`, and an nginx container.

## Starting Lab

```bash
# Start Lab
docker compose up

# During development, if making changes to the Dockerfiles, you can rebuild the images and restart the containers
docker compose build && docker compose up

# Ensure you see the containers running
docker ps
```

## Lab Tasks

After starting the lab docker compose, attach to the kali container and start the lab tasks.

```bash
docker exec -it kali bash
```

1. What is the IP address of the kali box?
    - `ifconfig`
    - `10.22.180.5`
2. Run a `nmap` TCP SYn (Stealth) scan of the subnet
    - `nmap -sS 10.22.180.0/24`
3. What is the IP address of the server with an open SSH port?
    - `10.22.180.40`
4. What is the version of `sshd` running on the server?
    - `nmap -sV 10.22.180.40`
    - `OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)`
5. How do you run the `nmap` default scripts against the server?
    - `nmap -sV -sC`
6. After running the default scripts against the server running `sshd`, what is the additional information output?
    - The `ssh-hostkey` information
7. What is the IP address of the server running a web server on port `80`?
    - `10.22.180.50`
8. What is the version of the web server running on the server?
    - `nmap -sV 10.22.180.50`
    - `nginx 1.23.1`
        - This will change eventually because the `Dockerfile` is pulling `nginx:latest`, pull specific version to avoid this)
9. Run the `nmap` default scripts against the server
    - `nmap -sC 10.22.180.50`
10. What additional information is output that might lead to hidden files?
    - Output specifies that the server has a `robots.txt` file
11. What is the page that the `robots.txt` file specifies index crawlers not to index?
    - `curl 10.22.180.50/robots.txt`
    - `l33t.html`
12. What is the flag that is displayed on the page?
    - `curl 10.22.180.50/l33t.html`
    - `UARK{d0ck3r_1s_4w3s0m3}`
