# 🦉 OAD

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OReconnaissance-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0.0-cyan?style=flat-square"/>
</p>

> **OAD** — Active Directory Offline Auditor

---

> ⚠️ **AUTHORISED USE ONLY** — Use only on systems you own or have explicit written permission to test. Unauthorised use is illegal.

---

## 📌 Overview

OAD is a strictly offline, read-only auditor for Active Directory data that was collected elsewhere, so it performs no LDAP queries or network calls of any kind. It ingests BloodHound/SharpHound JSON, ldapsearch LDIF exports and CSV dumps, then evaluates Kerberos, delegation, account-hygiene, privilege, host and GPO misconfigurations against a built-in rule catalogue. Findings are mapped to MITRE ATT&CK with remediation guidance and rolled up into a weighted A+…F grade for defenders hardening a domain.

---

## ✨ Features

- Strictly OFFLINE, READ-ONLY auditing of AD data that was collected elsewhere — no LDAP / network calls
- Tolerant ingest: BloodHound / SharpHound JSON (v3–v6, plain files, directories and .zip archives), ldapsearch LDIF exports (base64 + folded lines), CSV dumps (PowerShell Get-ADUser / Get-ADComputer / csvde)
- Format autodetection with per-file parse diagnostics
- Kerberos rules — Kerberoastable SPN users, AS-REP roastable (DONT_REQ_PREAUTH), DES-only, krbtgt age
- Delegation rules — unconstrained, constrained with protocol transition, resource-based (RBCD)
- Account hygiene — PASSWD_NOTREQD, DONT_EXPIRE_PASSWORD, reversible encryption, stale/inactive users & machines, old machine passwords, orphaned adminCount, SIDHistory, passwords in description fields
- Privilege rules — oversized Domain/Enterprise/Schema Admins, built-in operator groups, nested privilege, disabled-but-privileged, Protected Users coverage
- Host rules — LAPS absence, legacy / EOL operating systems, DC hygiene, unconstrained non-DC servers
- GPO / Domain rules — risky GPO names & paths, weak functional level, MachineAccountQuota, trusts w/o SID filtering, dangerous ACEs on high-value objects
- Text attack-path engine (BFS) to Domain Admins over MemberOf / AdminTo / HasSession / ACL edges
- Weighted A+…F grade with per-category subscores
- MITRE ATT&CK tags + remediation references per rule
- Export TXT / Markdown / JSON / CSV / SARIF 2.1.0
- --demo generates a realistic insecure AD dataset

---

## ⚙️ Requirements

- **Linux**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OAD --demo
./OAD --path ./bloodhound_export.zip --paths
./OAD -p ad_dump/ --format-out json -o report.json --fail-on high
./OAD --list-rules
./OAD --help
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
