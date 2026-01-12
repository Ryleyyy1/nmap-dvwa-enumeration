# Web Server Enumeration Analysis (DVWA Lab)

## Target Information
- Target IP      : 127.0.0.1 (localhost)
- Service        : HTTP
- Web Server     : Apache 2.4.65 (Debian)
- Environment    : Local DVWA Lab
- Scan Tool      : Nmap 7.95

---

## 1. Port & Service Detection

### Command Used
nmap -sS -sV -p 80 127.0.0.1

### Result
- Port     : 80/tcp
- State    : Open
- Service  : HTTP
- Version  : Apache httpd 2.4.65 (Debian)

### Analysis
Web server aktif dan dapat diakses secara publik.
Informasi versi server terdeteksi secara jelas yang dapat dimanfaatkan
oleh attacker untuk mencari vulnerability yang spesifik terhadap versi Apache tersebut.

---

## 2. HTTP Methods Enumeration

### Command Used
nmap -p 80 --script http-methods 127.0.0.1

### Result
Supported HTTP Methods:
- GET
- POST
- HEAD
- OPTIONS

### Analysis
Method GET dan POST aktif, yang merupakan metode utama pada aplikasi web.
Jika tidak divalidasi dengan benar, POST dapat dimanfaatkan untuk:
- SQL Injection
- XSS
- Command Injection

Method OPTIONS memungkinkan attacker mengetahui metode yang diizinkan oleh server.

---

## 3. HTTP Header & Title Enumeration

### Command Used
nmap -p 80 --script http-title,http-server-header 127.0.0.1

### Result
- Server Header : Apache/2.4.65 (Debian)
- Page Title    : Apache2 Debian Default Page: It works

### Analysis
Server masih menggunakan default Apache page, menandakan:
- Web server belum di-hardening
- Informasi banner terbuka
- Konfigurasi awal belum diubah

Hal ini meningkatkan kemungkinan reconnaissance lanjutan oleh attacker.

---

## 4. Directory Enumeration (NSE)

### Command Used
nmap -p 80 --script http-enum 127.0.0.1

### Result
Discovered Directory:
- /server-status/

### Analysis
Endpoint `/server-status/` terdeteksi, yang biasanya digunakan untuk
monitoring Apache server.

Jika endpoint ini dapat diakses tanpa autentikasi, attacker dapat melihat:
- Request aktif
- Informasi resource server
- Potensi traffic mapping

---

## 5. Security Impact Summary

### Potential Risks
- Information Disclosure (server version & banner)
- Exposed administrative endpoint
- Weak web server hardening
- Increased attack surface for further exploitation

---

## 6. Recommendations

- Nonaktifkan atau batasi akses `/server-status/` dengan authentication
- Sembunyikan server banner dan version disclosure
- Hapus default Apache page
- Terapkan web application firewall (WAF)
- Lakukan vulnerability assessment lanjutan (Nikto, OWASP ZAP)

---

## 7. Disclaimer

This project was conducted strictly in a legal and controlled lab environment
using DVWA on localhost.  
Any unauthorized scanning of systems without permission is illegal.
