# homelab-honeypot
Deploy a Simple Honeypot – Using Cowrie, SSH/Telnet honeypot.

Cowrie Honeypot Lab (Home Lab Project)

This is a simple honeypot project set up as part of my home cybersecurity lab to detect and log unauthorized SSH login attempts.

It uses Cowrie, (https://github.com/cowrie/cowrie), a very low-interaction SSH honeypot that simulates a fake Linux system to attract attackers and record their behavior and login attempts.


---


What I Used / Specs

- MacBook Pro M2 with 64 GB RAM
- VMware Fusion for running virtual machines
- Kali Linux VM (honeypot host)
- Windows 10 VM (attacker simulation)
- Cowrie honeypot (SSH port listener)
- Linux terminal & basic commands


---


Project Summary

In this lab, I configured a Kali Linux VM to run Cowrie on port 2222 and simulated an attack by SSHing into the honeypot from a Windows VM. All login attempts were logged for analysis.


---


Step-by-Step Setup On Kali Linux

1. Pre-Check - Update Kali VM terminal

Sudo apt update && sudo apt upgrade -y


2. Install Dependencies on Kali

sudo apt update && sudo apt install git python3-venv libssl-dev libffi-dev build-essential libpython3-dev -y


3. Clone Cowrie Repository

git clone https://github.com/cowrie/cowrie.git
cd cowrie


4. Set Up Python Virtual Environment

python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt


5. Configure Cowrie

cp etc/cowrie.cfg.dist etc/cowrie.cfg


6. Start Cowrie

bin/cowrie start


***Cowrie listens on port 2222 for SSH connections***
To check and verify:

sudo netstat -tulnp | grep 2222

The expected output should be:
tcp 0	0	0.0.0.0:2222	0.0.0.0:* LISTEN


---


Simulate the Attack from Windows VM

1. Enter the Following On the Windows VM Command Prompt:

ssh root@<KALI IP ADDRESS> -p 2222

Use any fake password. Cowrie will log the attempt and will be viewable on the Kali Linux VM.


---


View the Logs on Kali Linux VM

1. On Kali Linux VM Terminal

cd cowrie/var/log/cowrie
cat cowrie.log | grep “login attempt”


---

**Screenshots/Evidence**
* [Screenshot: Kali Linux VM - Honeypot Configuration](kali-linux-vm-honeypot-1.png)
* [Screenshot: Kali Linux VM - Honeypot Log Output](kali-linux-vm-honeypot-2.png)
* [Screenshot: Windows VM - Command Prompt (SSH Login Attempt)](windows-vm-command-prompt-ssh-login-attempt.png)

---

What I learned and practiced

	•	How to set up and run a simple honeypot
	•	Basic Linux administration and networking
	•	How attackers attempt brute-force SSH access
	•	Logging and monitoring unauthorized access attempts

What I can improve on in the future

	•	I can automate log analysis with scripts
	•	I can set up alerts when login attempts are made


