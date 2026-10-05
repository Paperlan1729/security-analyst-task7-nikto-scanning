# Security Analyst Task 7: Vulnerability Scanning with Nikto

**Author:** Dhrumit Asari  
**GitHub:** [Paperlan1729](https://github.com/Paperlan1729)  
**Track:** Security Analyst (Intermediate Practical Task)

---

## What Nikto Does

Nikto is an open-source web server scanner that performs comprehensive tests against web servers for multiple items, including over 6700 potentially dangerous files/programs, checks for outdated versions of more than 1250 servers, and version-specific problems on more than 270 servers. It also checks for server configuration items such as the presence of multiple index files and HTTP server options, and attempts to identify installed web servers and software.

## Limitations — “Noisy” Scanner

Nikto is intentionally thorough and therefore **noisy**. It generates a large volume of HTTP requests in a short time, which:
- Is easily detected by WAFs, IDS/IPS, and logging systems
- Can trigger rate-limiting or temporary blocks
- Is unsuitable for stealthy or production assessments without explicit permission and coordination

It is excellent for lab environments and intentional vulnerability discovery (e.g., against DVWA), but should not be run against production systems without written authorisation and a defined scope.

## Difference Between Nikto and Nmap

| Aspect              | Nmap                                      | Nikto                                          |
|---------------------|-------------------------------------------|------------------------------------------------|
| Primary focus       | Network hosts, ports, services, OS        | Web server / application vulnerabilities       |
| Protocol depth      | Broad (TCP/UDP/ICMP, many protocols)      | Primarily HTTP/HTTPS                           |
| Output style        | Port/service oriented                     | Finding / vulnerability oriented               |
| Noise level         | Configurable (can be stealthy)            | High by design                                 |
| Typical use case    | Reconnaissance & service discovery        | Web vulnerability identification               |

Nmap tells you *what is listening*; Nikto tells you *what is wrong with the web service*.

---

## Installation

### Kali Linux
Nikto is pre-installed. Verify:
```bash
nikto -Version
```

### Ubuntu / Debian
```bash
sudo apt update
sudo apt install nikto -y
```

### From source (any Linux)
```bash
git clone https://github.com/sullo/nikto
cd nikto/program
perl nikto.pl -Version
```

---

## Scans Performed

**Target:** Local DVWA instance (`http://127.0.0.1/DVWA` or `http://192.168.56.101/DVWA`)

### Basic scan
```bash
nikto -h http://127.0.0.1/DVWA
```

### Scan with output saved to file
```bash
nikto -h http://127.0.0.1/DVWA -o nikto_scan_results.txt -Format txt
```

### SSL check (if HTTPS is available)
```bash
nikto -h https://127.0.0.1/DVWA -ssl
```

Full findings and remediation notes are in [nikto_scan_results.txt](nikto_scan_results.txt).

---

## Files

- `nikto_scan_results.txt` — Scan output + severity categorisation + remediation
- `README.md` — This documentation
- `screenshots/` — Terminal screenshots of Nikto running and results

## Ethics

Scans were performed exclusively against a local DVWA instance under my control. Nikto was never pointed at external or production systems.

---

*Completed by Dhrumit Asari — Security Analyst Track*
