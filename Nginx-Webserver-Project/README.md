# Cybersecurity Home Lab Projects

This repository documents a hands-on cybersecurity project performed within a virtualized lab environment. The goal is to build practical skills in system administration, network security, web server management, and incident response using open-source tools.

---

## Technology Stack

* **Host OS:** macOS (MacBook Pro)
* **Virtualization:** VMware Fusion
* **Guest OS:** Kali Linux 2025.2 (or whatever version you have installed)
* **Networking:** NAT (Network Address Translation)
* **Web Server:** Nginx
* **Browsers:** Safari, Google Chrome (for testing)
* **Command Line Interface:** Bash and macOS Terminal

---

## Table of Contents

* [Project 1: Deploying a Simple Web Server with Nginx and Monitoring Logs](#project-1-deploying-a-simple-web-server-with-nginx-and-monitoring-logs)

---

### Project 1: Deploying a Simple Web Server with Nginx and Monitoring Logs

**Goal:** To deploy a basic Nginx web server on Kali Linux, access it from the host machine (macOS), and learn to monitor web server access logs.

**Concepts Learned:**
* Web server deployment (nginx package).
* Service management (systemctl start/stop/enable/status).
* Port listening (ss command).
* Web server logs (access.log, error.log).
* Real-time log monitoring (tail -f).
* HTTP status codes (For example, "200 OK").

**Challenges Faced:**
* **Severe persistent conflict with Apache2:** Even on a newly installed VM, Apache2 (or remnants/cached pages) was occupying port 80, preventing Nginx from serving. This required in-depth purging of Apache2.
* **Missing Nginx web root (`/var/www/html`):** After Apache cleanup, the default web root was missing, preventing Nginx from serving content until the directory and a new `index.html` were created.
* **Google Chrome browser issues:** The web server was accessible via Safari on my macOS host, but Chrome persistently failed. I was not able to get to the bottom of this issue as I tried to implement many solutions, yet no luck.

**Steps Taken:**
1.  I ensured Kali Linux VM was clean (fresh install recommended due to previous issues).
2.  Ran `sudo apt update && sudo apt full-upgrade -y` in Terminal
3.  Verified Apache2 was completely removed (Used the command `sudo apt purge apache2`).
4.  Installed Nginx (`sudo apt install nginx`).
5.  Started and enabled Nginx service (`sudo systemctl start nginx`, `sudo systemctl enable nginx`).
6.  Confirmed Nginx was actively running and listening on port 80 (`sudo systemctl status nginx`, `sudo ss -tulnp | grep :80`).
7.  Discovered and resolved the missing "/var/www/html" directory by creating it and setting appropriate permissions. See below:
        `sudo mkdir -p /var/www/html`
        `sudo chown -R www-data:www-data /var/www/html`
        `sudo chmod -R 755 /var/www/html`
8.  Created a custom "index.html" file within Nginx's default web root. See below:
        `sudo nano /var/www/html/index.html`
9.  Accessed the Nginx web server locally within Kali (Firefox) using both `127.0.0.1` and the VM's specific IP address, confirming Nginx was on.
    Entering 127.0.0.1 in the Firefox browser, it kept giving me the Apache2 Debian Default Page for some reason. However, after entering my local VM's IP address into the address bar, it was showing the Nginx welcome page.
10. Accessed the Nginx web server from the host machine (Mac) using Safari by entering the VM's IP address into the address bar.
11. Monitored Nginx `access.log` in real-time (`sudo tail -f /var/log/nginx/access.log`) while generating traffic from the Mac browser (I was refreshing the welcome page in Safari).
12. Observed successful (200) requests in the logs.

**Commands Used:**
* `sudo apt update && sudo apt full-upgrade -y` (Initial setup)
* `sudo apt purge apache2* -y`
* `sudo rm -rf /etc/apache2 /var/log/apache2 /var/www/html/index.html` (Aggressive Apache cleanup)
* `sudo apt purge nginx nginx-common -y` (If reinstalling Nginx)
* `sudo apt install nginx -y`
* `sudo systemctl start nginx`
* `sudo systemctl enable nginx`
* `sudo systemctl status nginx`
* `ip a`
* `sudo ss -tulnp | grep :80`
* `sudo mkdir -p /var/www/html`
* `sudo chown -R www-data:www-data /var/www/html`
* `sudo chmod -R 755 /var/www/html`
* `sudo nano /var/www/html/index.html` (to create custom page)
* `sudo tail -f /var/log/nginx/access.log`
* `http://192.168.210.131` (in browser)

**Screenshots/Evidence:**
* [Screenshot: `sudo systemctl status nginx` output confirming Nginx is active and running.](nginx-status-active.png)
* [Screenshot: `sudo ss -tulnp | grep :80` output clearly showing Nginx listening on port 80.](nginx-port-80-listener.png)
* [Screenshot: Safari on macOS displaying the "Welcome to Nginx!" page from the Kali VM's IP address.](mac-safari-access.png)
* [Screenshot: Kali terminal showing the `access.log` updating in real-time with recent web requests.](nginx-access-logs.png)

**Key Takeaways:**
* Only one service can listen on a given port at a time; conflicts can be very tricky to diagnose. Issues with Apache2
* Verifying web server content locally (127.0.0.1, VM IP) is important before testing externally.
* Browser caching and specific browser quirks can cause false negatives. Example was Google Chrome not being able to access the server.
* Web server logs are invaluable for understanding traffic, successful requests, and errors.
* Basic Linux file system knowledge (permissions, directories) is essential for web server setup.

---
