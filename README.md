# Penetration-Test-su-Metasploitable
# 🔍 Penetration Test Lab: Nessus + Nmap su Metasploitable2 da Kali Linux

> **Obiettivo**: Simulare una fase di **ricognizione e scansione attiva** all’interno di un ambiente controllato, usando **Nmap** e **Nessus** da **Kali Linux** verso una macchina vulnerabile (**Metasploitable2**).

---

## 🖥️ Ambiente di test

| Sistema         | IP             | Note                          |
| --------------- | -------------- | ----------------------------- |
| Kali Linux      | `192.168.0.168` | Macchina attaccante (scanner) |
| Metasploitable2 | `192.168.0.167` | Macchina vulnerabile (target) |

Ambiente virtuale configurato con rete interna per comunicazione diretta tra Kali e Metasploitable.

---

## 🔧 Strumenti utilizzati

* **Nmap** – Scanner di rete per identificazione porte, servizi e sistema operativo
* **Nessus** – Vulnerability scanner per analisi di sicurezza approfondita
* **VirtualBox / VMware** – Ambiente di virtualizzazione (non obbligatorio, ma consigliato)

---

## 🔎 Scansioni eseguite con Nmap

### 🔹 TCP Connect Scan (`-sT`)

```bash
nmap -sT -p 1-1024 192.168.0.167
```

* Metodo "full open" (3-way handshake)
* Porte TCP 1-1024
* Risultato: **12 porte aperte**

### 🔹 TCP SYN Scan (`-sS`)

```bash
nmap -sS -p 1-1024 192.168.0.167
```

* Metodo "stealth"
* Stessi risultati del TCP Connect (12 porte aperte)

### 🔹 Scansione Aggressiva (`-A`)

```bash
nmap -A -p 1-1024 192.168.0.167
```

* Rilevamento sistema operativo, versioni dei servizi, script scanning
* OS rilevato: Linux 2.6.X
* Identificati anche:

  * `vsftpd`, `OpenSSH`, `Apache`, `BIND`, `Postfix`, `Netkit`, ecc.

---

## 📋 Porte e Servizi Identificati

| Porta | Protocollo | Servizio | Versione / Info                         |
| ----- | ---------- | -------- | --------------------------------------- |
| 21    | TCP        | FTP      | vsftpd 2.3.4 (**Anon login abilitato**) |
| 22    | TCP        | SSH      | OpenSSH 4.7p1 (Debian)                  |
| 23    | TCP        | Telnet   | Linux telnetd                           |
| 25    | TCP        | SMTP     | Postfix smtpd (supporta **SSLv2**)      |
| 53    | TCP        | DNS      | ISC BIND 9.4.2                          |
| 80    | TCP        | HTTP     | Apache 2.2.8 (Ubuntu, DAV/2)            |
| 111   | TCP        | RPCBind  | Versione 2                              |
| 139   | TCP        | NetBIOS  | tcpwrapped                              |
| 445   | TCP        | MS-DS    | tcpwrapped                              |
| 512   | TCP        | exec     | netkit-rsh rexecd                       |
| 513   | TCP        | login    | OpenBSD/Solaris rlogind (non precisato) |
| 514   | TCP        | shell    | netkit-rshd                             |

---

## 🧪 Nessus Scan (overview)

* Eseguito da Kali verso Metasploitable2
* Identificati servizi vulnerabili:

  * FTP anonimo abilitato
  * Servizi con SSLv2 obsoleto
  * Porte RPC, RSH, Telnet aperte (insecure by design)
* Nessus ha suggerito aggiornamenti critici e configurazioni da disabilitare

---

## 🛡️ Considerazioni sulla sicurezza

* Diversi servizi **obsoleti e vulnerabili** sono attivi sulla macchina target
* **Accesso anonimo FTP** e **Telnet non cifrato** rappresentano gravi rischi
* Servizi come `rsh`, `rlogin` e `rpcbind` sono spesso sfruttati in laboratori di exploit
* Ideale per test con **Metasploit Framework**

---

## 📁 File inclusi nella repository

* `nmap_scan.txt` – Output completo delle scansioni Nmap
* `nessus_report.html` – Report completo esportato da Nessus
* `screenshots/` – Cartella con eventuali immagini/screenshot
* `README.md` – Questo file

---

## 🧩 Organizzazione della repository GitHub

```
penetration-test-metasploitable/
├── README.md
├── nmap_scan.txt
├── nessus_report.html
├── screenshots/
│   ├── nmap_output.png
│   └── nessus_summary.png
└── LICENSE (opzionale)
```

### 📦 `.gitignore` consigliato

```
*.log
*.tmp
*.pcap
*.db
```

### 🏷️ Tag suggeriti

```
penetration-testing, nmap, nessus, metasploitable2, kali-linux, cybersecurity, ethical-hacking
```

### 📄 Licenza consigliata

* [MIT License](https://opensource.org/licenses/MIT) (open source, permissiva)
* [Creative Commons Attribution](https://creativecommons.org/licenses/by/4.0/) (didattica)

---

## 📘 Note finali

> Questo progetto è stato svolto **in ambiente controllato** per scopo **formativo**.
> Non va utilizzato per attività non autorizzate.

---

## 📌 Descrizione suggerita per la repository GitHub

> Penetration test simulato con **Nmap** e **Nessus** eseguito da Kali Linux contro una macchina vulnerabile Metasploitable2. Include scansioni, analisi e considerazioni di sicurezza. Progetto a scopo didattico.
