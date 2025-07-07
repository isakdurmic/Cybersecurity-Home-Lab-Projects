# My Cybersecurity-Home-Lab-Projects

Hello! This repo is where I'm documenting all the hands-on cybersecurity projects I'm working on in my home lab (virtual machine environment). I am basically documenting my journey of trying to learn this stuff by doing it, breaking things, and then figuring out how to fix them.

---

## Lab Environment Overview

This section details the primary technologies and tools used across these projects:

* **Host OS:** macOS (M2 MacBook Pro 64GB)
* **Virtualization Platform:** VMware Fusion
* **Guest OS:** Kali Linux 2025.2 (specific version as installed) as well as Windows 11 VM.
* **Network Configuration:** Primarily NAT (Network Address Translation) for VM isolation and host connectivity.
* **Web Server:** Nginx
* **Browsers for Testing:** Safari, Google Chrome
* **Primary Interface:** Linux Command Line Interface (Bash) and macOS Terminal

---

## Project Log

Below is a structured log of the completed and ongoing projects within this lab. Each project has its own dedicated directory with comprehensive documentation.

* [Project: Honeypot Deployment](#project-honeypot-deployment)
* [Project: Nginx Web Server Deployment and Log Analysis](#project-nginx-web-server-deployment-and-log-analysis)

---

### Project: Honeypot Deployment

This project involved setting up a basic honeypot on a Kali Linux VM. The primary goal was to deploy a low-interaction honeypot to detect and log unauthorized SSH login attempts, providing insights into common attack vectors.

[View Detailed Honeypot Project Documentation Here](Honeypot-Project/README.md)

---

### Project: Nginx Web Server

This project focused on the practical deployment of a basic Nginx web server within the Kali Linux VM. It covered initial setup, ensuring network accessibility from the host machine, and critical log analysis for monitoring server activity and identifying potential security events.

[View Detailed Nginx Web Server Project Documentation Here](Nginx-Webserver-Project/README.md)

---
