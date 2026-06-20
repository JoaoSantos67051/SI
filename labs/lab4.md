# Lab #04 — Hypothetical Network Attack

## Index

* [1. Objective](#1-objective)
* [2. Network Scenario](#2-network-scenario)
* [3. Attack Description](#3-attack-description)
* [4. Possible Consequences](#4-possible-consequences)
* [5. Prevention Measures](#5-prevention-measures)
* [6. References](#6-references)
* [7. Conclusion](#7-conclusion)

---

## 1. Objective

The objective of this lab is to describe a hypothetical network attack against the example network presented in the statement.

The network includes internet access, a firewall, a router, wireless clients, wired clients, servers, and a printer. The goal is to explain a possible attack vector, how the attacker could gain access, how privileges could be increased, what the impact could be, and how the attack could be prevented.


## 2. Network Scenario

The selected scenario is based on a **wireless initial access attack**.

In the example network, wireless clients connect to the internal infrastructure through a wireless access point. If the wireless network is weakly protected or poorly segmented, an attacker located nearby could try to join the network and then explore internal systems.

This is relevant because attack vectors can come from the outside, from the inside, or through the human factor. In this case, the wireless network becomes the first entry point into the internal environment.


## 3. Attack Description

The attack could happen in the following way:

1. **Initial Access**
   The attacker stays near the organization and targets the wireless network. Access could be obtained through a weak Wi-Fi password, a shared credential, a rogue access point, or a social engineering technique that convinces a user to reveal the password.

2. **Internal Reconnaissance**
   After connecting to the wireless network, the attacker scans the internal network to identify clients, servers, the printer, the router, and exposed services. This follows the reconnaissance and scanning phases of a pentest.

3. **Credential Capture**
   The attacker may try to capture credentials or authentication hashes by abusing local network trust. This could involve fake login pages, spoofing attacks, or targeting poorly configured internal services.

4. **Privilege Escalation**
   If the attacker compromises a client machine or obtains valid credentials, they may attempt to increase privileges by exploiting outdated software, weak passwords, stored credentials, or misconfigured services.

5. **Lateral Movement**
   Once the attacker has stronger access, they may move from the wireless segment to wired clients, servers, or the printer. If the network is not segmented, the initial wireless access can become a path to sensitive internal systems.


## 4. Possible Consequences

A successful attack could have several consequences:

| Consequence             | Description                                                    |
| ----------------------- | -------------------------------------------------------------- |
| Data theft              | Sensitive files from servers or clients could be stolen.       |
| Credential compromise   | User or administrator credentials could be captured.           |
| Service disruption      | Servers, printers, or network devices could be affected.       |
| Malware deployment      | The attacker could install malware or ransomware.              |
| Lateral movement        | One compromised device could lead to more compromised systems. |
| Loss of confidentiality | Internal data and communications could be exposed.             |


## 5. Prevention Measures

To reduce the risk of this attack, the organization should apply the following controls:

| Measure                      | Purpose                                                                               |
| ---------------------------- | ------------------------------------------------------------------------------------- |
| Strong Wi-Fi security        | Use WPA2/WPA3 Enterprise and disable weak shared passwords.                           |
| Network segmentation         | Separate guest Wi-Fi, employee Wi-Fi, servers, printers, and administration networks. |
| Least privilege              | Users and devices should only access what they need.                                  |
| Secure printer configuration | Change default credentials, update firmware, and restrict administration access.      |
| Monitoring and detection     | Use SIEM, EDR, IDS/IPS, and network monitoring to detect suspicious activity.         |
| Protection against spoofing  | Use DHCP snooping, Dynamic ARP Inspection, and secure switch configurations.          |
| User awareness               | Train users to avoid fake Wi-Fi networks, phishing, and suspicious login pages.       |
| Regular updates              | Keep clients, servers, printers, and network devices patched.                         |


## 6. References

This lab is based on the theoretical concepts from:

* **Class 03 — Anatomy of a Pentest**

  * Scope definition
  * Reconnaissance
  * Scanning
  * Exploitation
  * Privilege escalation
  * Reporting

* **Class 04 — Attack Vectors**

  * External attack paths
  * Internal attack paths
  * Vulnerable networks
  * Vulnerable people
  * Human factor
  * Lateral movement

* **Class 05 — Defense**

  * Visibility
  * Detection
  * SIEM
  * EDR
  * Firewalls
  * Network and edge controls

* **Class 06 — Network Security**

  * Wi-Fi sniffing
  * ARP and DHCP spoofing
  * Port scanning
  * DNS and SSL interception
  * Firewalls, VPNs, and honeypots

## 7. Conclusion

This lab described a hypothetical attack where the wireless network is used as the initial entry point into the internal infrastructure.

After gaining wireless access, the attacker could perform reconnaissance, capture credentials, escalate privileges, and move laterally to clients, servers, or the printer. The main risk is that a weak wireless configuration or lack of segmentation can expose the whole internal network.

The most important defenses are strong Wi-Fi authentication, network segmentation, least privilege, secure device configuration, monitoring, and user awareness. The firewall is important, but it is not enough by itself. Internal networks must also be designed to limit trust and detect suspicious behavior quickly.

