# Nmap Web Server Enumeration using DVWA

## 📌 Overview
This project demonstrates web server enumeration using **Nmap and NSE scripts**
against **DVWA (Damn Vulnerable Web Application)** in a controlled local lab
environment.

The goal is to identify exposed services, HTTP methods, server information,
and potentially sensitive endpoints.

---

## 🛠️ Tools & Environment
- Nmap 7.95
- Kali Linux
- Apache Web Server
- DVWA (Localhost)
- Target: 127.0.0.1

---

## ⚙️ Enumeration Techniques
- Port & service detection
- HTTP methods enumeration
- HTTP header and title discovery
- Directory enumeration using NSE

---

## 🧪 Commands Used
All commands are documented in `commands.txt`

Example:
```bash
nmap -sS -sV -p 80 127.0.0.1
