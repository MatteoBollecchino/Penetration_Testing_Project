# VAPT Final Report - IMPS Hack

[![University](https://img.shields.io/badge/University-UniFI-blue.svg)](https://www.unifi.it/)
[![Course](https://img.shields.io/badge/Course-Penetration%20Testing-red.svg)]()
[![CVSS](https://img.shields.io/badge/Standard-CVSS%20v4.0-orange.svg)](https://www.first.org/cvss/v4.0/)
[![License](https://img.shields.io/badge/License-Academic%20Use%20Only-lightgrey.svg)]()

This repository contains the official Vulnerability Assessment and Penetration Testing (VAPT) report conducted in **Black-Box mode** on the containerized target application representing the website of the **"Istituto Mondiale di Previdenza Sociale degli Hacker" (IMPS Hack)**.

The testing activity was performed as part of the **Penetration Testing** course within the Master's Degree in *Software: Science and Technology* at the **University of Florence (Università degli Studi di Firenze)**.

---

### Executive Summary

The assessment identified multiple critical security flaws within the target web application, escalating from an initial unauthenticated entry point to **Full System Compromise (Remote Code Execution)** and interactive **Reverse Shell** access under the context of the `www-data` service user.

Post-exploitation analysis confirmed that the target operates within an isolated Docker container lacking local privilege escalation vectors (`sudo`), effectively bounding the impact within the containerized perimeter.

---

## Summary of Identified Vulnerabilities

All vulnerabilities have been classified using the **CVSS v4.0** standard:

| ID | Vulnerability Title | Severity | CVSS v4.0 Score | Vector String |
| :--- | :--- | :---: | :---: | :--- |
| **VULN-01** | Remote Code Execution via SQLi `INTO OUTFILE` | **`CRITICAL`** | **10.0** | `CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:H/VA:H/SC:H/SI:H/SA:H` |
| **VULN-02** | SQL Injection (Union & Error-Based) | **`HIGH`** | **8.7** | `CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:N/VA:N/SC:N/SI:N/SA:N` |
| **VULN-03** | Local File Inclusion (LFI) / Path Traversal | **`HIGH`** | **8.7** | `CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:N/VA:N/SC:N/SI:N/SA:N` |
| **VULN-04** | Information Disclosure & Verbose Errors | **`MEDIUM`** | **6.9** | `CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:L/VI:N/VA:N/SC:N/SI:N/SA:N` |
| **VULN-05** | Reflected XSS via HTML Attribute Breakout | **`MEDIUM`** | **5.1** | `CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:P/VC:N/VI:N/VA:N/SC:L/SI:L/SA:N` |

---

## Target & Engagement Scope

* **Testing Mode:** Black-Box
* **Target Container:** `gabrielec/ptexam4`
* **Target IP Address:** `172.17.0.2:80/TCP` (HTTP)
* **Out of Scope:** Denial of Service (DoS/DDoS), Social Engineering, Host System Intrusion outside the Docker container.

---

## Methodology

The assessment followed a structured 7-phase methodology adapted to containerized web environments:

1. **Information Gathering:** Passive & Active perimeter identification.
2. **Network Scanning & Banner Grabbing:** Port scanning (`nmap`), Layer 2/3 reachability (`arping`), and HTTP banner identification (`Apache/2.4.68 (Debian)`).
3. **Enumeration:** Hidden content discovery (`gobuster`), parameters mapping, and diagnostic endpoint analysis (`info.php`).
4. **Vulnerability Assessment:** Input vector testing for SQLi, LFI, and Reflected XSS.
5. **Exploitation:** Web Shell deployment via SQL `INTO OUTFILE` and URL-encoded Reverse Shell execution via Netcat.
6. **Post-Exploitation:** Permission checks (`/etc/shadow`), SUID binary auditing (`find / -perm -4000`), and privilege escalation vector verification.
7. **Remediation Strategy:** Architectural and code-level remediation recommendations (Prepared Statements, Input Sanitization, Static Path Maps, Verbose Error Disabling).

---

## Author Information

* **Candidate:** Matteo Bollecchino
* **Degree:** Master's Degree Course in Software: Science and Technology
* **Institution:** Università degli Studi di Firenze (UniFI)
* **Academic Year:** 2025/2026

---

## Disclaimer

*This report was produced solely for academic assessment purposes within an isolated, controlled laboratory environment. All testing activities were executed strictly in accordance with pre-agreed Rules of Engagement (RoE).*
