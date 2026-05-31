# Elevate_labs_Task1
Task for my internship 

Task 1: Local Network Port Scanning
Internship Program: Elevate Labs (MSME, Ministry of India)
My Objective: Figure out how to scan my own local network, see what ports are left wide open on my devices, and understand what kind of security risks those openings create.  
------- What I Did (Step-by-Step)------
Step 1: Finding My Target Range
Before running any scans, I needed to know what network I was actually on. I opened up my terminal and checked my local IP setup.
I used the ip a command (if you're on Windows, use ipconfig).
I found out my machine's IP was 192.168.1.15, which meant my whole local network range was 192.168.1.0/24.
Step 2: Running the Nmap Scan
I used Nmap to run a TCP SYN scan. Because SYN scans mess with raw network packets, the terminal made me use sudo to run it as an administrator.
I also used a little trick (-oN) to automatically dump the terminal results into a text file so I didn't have to copy-paste it manually.
sudo nmap -sS 192.168.1.0/24 -oN network_scan_log.txt
-----Scan Results----------
My scan picked up three live devices on my home Wi-Fi. Here is the breakdown of what's running on them:
1. The Home Router (192.168.1.1)
Port 80/tcp (Open) - HTTP: This is just the standard web page you log into to change the Wi-Fi password or reboot the router.
Port 53/tcp (Open) - domain: Used for DNS, which helps the router translate website names into IP addresses.
2. My Laptop (192.168.1.15)
Port 22/tcp (Open) - SSH: I forgot I left this on! It’s open so I can remotely access my laptop's terminal from other devices.
3. Living Room Smart TV (192.168.1.42)
Port 443/tcp (Open) - HTTPS: Secure web traffic.
Port 8008/tcp (Open) - HTTP-Alt: This is standard for local casting and streaming services (like Chromecast or DLNA).
Security Risk Analysis
Looking at these results, a few things stood out to me from a security perspective:
The Router's Port 80: Since HTTP isn't encrypted, if a malicious user got onto my Wi-Fi, they could theoretically sniff the network packets and steal my router's admin password. I should look into forcing HTTPS (Port 443) for the router admin page.
My Laptop's Port 22: Leaving SSH wide open is fine if my password is super strong, but if it's weak, someone could try to brute-force their way into my laptop. I should probably switch to SSH key authentication instead of passwords.
Smart TV Port 8008: IoT devices like TVs are notorious for rarely getting software updates. If an attacker gets into the network, unpatched ports on a smart TV are an easy target to exploit.
