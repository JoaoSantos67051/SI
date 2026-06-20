# Class 01 - Security Principles

Saltzer & Schroeder (1975):
10 design rules that still define resilient systems today.

Principle 1
Economy of Mechanism
1 Keep security simple and usable

    Smaller, clearer designs reduce implementation bugs and hidden attack paths.
    Usable controls increase compliance and reduce unsafe workarounds.
    Security that users can understand is security they can maintain.

Principle 2
Fail-Safe Defaults
2 Deny by default, allow explicitly

    Every new user, service, or API call starts with zero permissions.
    Access is granted deliberately, scoped, and auditable.
    Misconfiguration tends to reduce access, not accidentally expose data.

Principle 3
Complete Mediation
3 Check every access, every time

    Authorization must happen at each sensitive operation, not just at login.
    Permissions evolve; stale trust decisions create security gaps.
    Policy enforcement points should be central, consistent, and testable.

Principle 4
Open Design
4 Security should survive public scrutiny

    Do not depend on hidden algorithms or secret architecture for safety.
    Prefer peer-reviewed mechanisms with known security properties.
    Keep secrets where they belong: keys, credentials, and operational data.

Principle 5
Separation of Privilege
5 Require multiple conditions for critical actions

    Combine independent checks such as MFA, approvals, or dual control.
    A single compromised account should not unlock high-impact operations.
    Defense-in-depth lowers the blast radius of individual failures.

Principle 6
Least Privilege (Need-to-Know)
6 Grant only what is necessary

    Users, workloads, and services receive minimum rights for their task.
    Short-lived and just-in-time access reduces long-term exposure.
    Compromises stay contained because unnecessary paths are closed.

Principle 7
Least Common Mechanism
7 Reduce shared mechanisms across users

    Shared components create cross-tenant dependencies and side channels.
    Isolate resources and control planes whenever practical.
    Lower coupling means fewer system-wide compromise opportunities.

Principle 8
Psychological Acceptability
8 Security UX must feel natural

    People follow secure workflows when they are clear and low-friction.
    Confusing prompts and heavy friction trigger risky bypass behavior.
    Good design aligns safe behavior with user goals.

Principle 9
Work Factor
9 Make attacks economically impractical

    Estimate attacker cost in time, compute, expertise, and required access.
    Raise barriers with strong crypto, rate limits, and layered detection.
    Reassess continuously as tools and hardware reduce attack costs.

Principle 10
Compromise Recording
10 Detect, log, and learn from breaches

    Logging and telemetry turn incidents into actionable lessons.
    Forensics, timeline reconstruction, and alerting accelerate response.
    Visibility enables deterrence, accountability, and continuous hardening.

Takeaway
Secure by Design Beats Secure by Patch

These principles are not historical artifacts; they are practical guardrails for modern cloud, apps, and AI systems.

---


# Class 02 - Security Threats

Threat landscape overview: what attacks look like today and where organizations are most exposed.

Category 1
Common Threats
1 High-frequency attacks across all sectors

    Denial of Service (DoS/DDoS): availability disruption through traffic floods.
    Phishing, vishing, and smishing: credential theft via social engineering.
    Credential stuffing and password spraying: automated account takeover attempts.

Category 2
Hardware Threats
2 Compromises through physical and device vectors

    Supply-chain tampering in firmware, chips, or third-party equipment.
    Rogue USB devices (Rubber Ducky), keyloggers, and malicious peripherals.
    Physical attacks: theft, unauthorized access, and device manipulation.

Category 3
Software Threats
3 Exploits targeting code and application logic

    Memory flaws: buffer overflows, use-after-free, and unsafe deserialization.
    Injection attacks: SQL, command, LDAP, template, and prompt injections.
    Vulnerable dependencies and unpatched CVEs in libraries and runtimes.

Category 4
Network Threats
4 Threats in transit and protocol abuse

    Man-in-the-Middle (MitM): interception and tampering of communications.
    Spoofing and session hijacking: impersonation of trusted systems or users.
    Sniffing and reconnaissance: passive data capture and attack surface mapping.

Category 5
Cloud and Identity Threats
5 Modern exposures in hybrid and cloud-native stacks

    Misconfigured storage, IAM roles, and over-privileged service accounts.
    Token theft, OAuth abuse, and MFA fatigue/social engineering bypasses.
    Exposed secrets in repositories, CI/CD pipelines, and container images.

Category 6
Insider and Third-Party Threats
6 Risk from trusted users and partner ecosystems

    Malicious insiders abusing legitimate access to steal or sabotage.
    Negligent insiders causing data leaks through mistakes or weak practices.
    Vendor and MSP compromise propagating into customer environments.

Category 7
Ransomware and Extortion
7 Business disruption plus financial pressure

    Double and triple extortion: encrypt, steal, then pressure stakeholders.
    Lateral movement and backup targeting increase recovery difficulty.
    Initial access commonly via phishing, RDP abuse, or unpatched services.

Category 8
Emerging Threats
8 New attack patterns from AI and connected systems

    Deepfake-enabled fraud and AI-assisted phishing at scale.
    IoT and OT attacks against weakly managed devices and critical operations.
    LLM misuse: data leakage, model manipulation, and prompt injection abuse.

Category 9
Impact and Prioritization
9 Focus defense where risk is highest

    Assess threats by likelihood, business impact, and detection difficulty.
    Prioritize crown-jewel assets, identity systems, and exposed services.
    Map controls to top threat paths, not just compliance checklists.

Category 10
Defense Priorities
10 Practical baseline to reduce exposure fast

    Identity-first security: phishing-resistant MFA and least privilege.
    Patch and vulnerability management with verified backup strategy.
    Continuous monitoring, incident drills, and tested recovery playbooks.

Takeaway
Threats Evolve Fast, Defense Must Evolve Faster

The most resilient organizations combine strong prevention, rapid detection, and rehearsed response.


---

# Class 03 - Anatomy of a Pentest Ficheiro PDF

1
0 Scope (Scope Definition)
This phase involves planning the pentest, where goals, permissions, systems,
and the level of information provided to pentesters are discussed. The goal
is to establish clear boundaries to avoid unauthorized actions.

0.1 Useful Tools:
• Documentation and project management (like Jira, Trello, or No-
tion) to track objectives and ensure organization. Scope management
does not require specific hacking tools but rather documentation soft-
ware.
1 Recon (Reconnaissance and Intelligence Gather-
ing)
In this phase, an extensive collection of public and visible information about
the target is gathered using OSINT (Open Source Intelligence) techniques.
The objective is to compile as much data as possible without directly inter-
acting with the target system.

1.1 Tools
• Maltego: To create relationship maps between different entities.
• theHarvester: To gather emails, subdomains, and other public infor-
mation.
• Recon-ng: An OSINT framework with various modules.
• Shodan and Censys: To see what is publicly accessible about the target
on the internet.

2 Scanning
The goal here is to identify available hosts and services, open ports, and
“interesting” addresses. It also includes mapping possible vulnerabilities for
future exploitation.

2
2.1 Tools
• Nmap: For port and service scanning.
• Masscan: An extremely fast port scanner for large networks.
• Nikto: A web vulnerability scanner that identifies dangerous configu-
rations and problems in web servers.
• OpenVAS: A vulnerability scanner to detect possible flaws in hosts and
services.
• dnsrecon or dnsenum: For DNS enumeration, useful for finding sub-
domains and other records.
• dirbuster or gobuster: For web directory and file enumeration

3 Exploitation
In this phase, identified vulnerabilities are exploited. It may involve exploit-
ing known CVEs, social engineering, or physical access.

3.0.1 Tools
• Metasploit Framework: One of the most popular exploitation frame-
works, with an extensive library of exploits.
• Exploit-DB: Exploit database where you can search for specific soft-
ware vulnerabilities.
• BeEF (Browser Exploitation Framework): For attacks directed at
browsers.
• Responder and Inveigh: Network Poisoning tools, useful for Man-in-
the-Middle (MITM) attacks.
• Social Engineering Toolkit (SET): For social engineering tests, in-
cluding phishing attacks.

3.1 Shell Access
Obtaining a remote shell on the target system, which enables initial access.
This access is typically the entry point for lateral movement.

3
3.1.1 Tools
• Netcat: For establishing basic backdoors.
• SSH/OpenSSH: If a password or key is compromised.
• Meterpreter (Metasploit): Provides an interactive shell on compro-
mised systems with various functionalities.

3.2 Lateral Movement / Pivoting
The goal here is to use the acquired access to reach other systems and net-
works in the infrastructure. At this stage, the pentester moves laterally
across the network.

3.2.1 Tools
• Mimikatz: For credential extraction on the network, useful for lateral
movement.
• Impacket: Set of scripts enabling SMB, RDP, and other interactions,
facilitating lateral movement.
• ProxyChains: To route traffic through a compromised host.

3.3 Log Cleaning
Deleting or modifying logs to hide activity. This practice is fundamental to
ensure the intrusion is not immediately detected.

3.3.1 Tools
• Manual scripts or system’s own tools, such as Clear-EventLog in Win-
dows PowerShell.
• Metasploit (Meterpreter): Includes options to clear logs after ex-
ploitation.
4 Privilege Escalation
The aim here is to increase privileges (e.g., from a limited user to root or ad-
ministrator) to gain full access to the system. If new privileges are obtained,
the scanning and exploitation cycle is restarted from the new access level.

4
4.1 Tools
• LinPEAS: To find potential escalation vectors on Linux systems.
• WinPEAS: Windows version.
• PowerUp and SharpUp: Privilege escalation tools in the Windows envi-
ronment.
• GTFOBins and LOLBAS: Repositories of legitimate binaries and scripts
that can be exploited for privilege escalation.
5 Install APT (Advanced Persistent Threat)
A backdoor or another type of persistent access is configured to maintain
long-term intrusion, if this is the goal of the test.
5.1 Tools

• Empire: Framework for persistence attacks in Windows environments.
• Pupy: Remote access tool that allows creating backdoors on compro-
mised systems.
• C2 frameworks like Cobalt Strike or Sliver (for open-source alter-
natives).

6 Reporting
The final pentest report documents all findings, successful exploits, and rec-
ommendations for improving security. This is a critical document that should
be clear, detailed, and accessible to all stakeholders, from technical to exec-
utive levels.

6.1 Tools
• Dradis: For security report management and team collaboration.
• MagicTree: Data management tool for pentesting, allowing centralized
and structured information.
• Faraday: Collaborative IDE for security teams that supports report
creation.

---

# Class 04 - Attack Vectors


How attackers enter systems from the outside, from the inside, and through human behavior that links both.

Framing
What Is an Attack Vector?
1 A path used to reach a target or trigger a compromise

    Attack vectors describe how attackers gain entry, escalate access, or disrupt operations.
    They may involve networks, software flaws, hardware exposure, or human weakness.
    Real incidents usually combine several vectors into a single attack chain.

Perspective
From the Outside
2 External attackers start with exposed surfaces

    Public-facing services, websites, VPNs, and email gateways are common first targets.
    Outside attackers look for weak software, people, hardware deliveries, and physical access gaps.
    The goal is usually initial access that can later be expanded internally.

Outside
Vulnerable Software
3 Exposed services create remote attack paths

    Remote exploits target web servers, VPNs, mail systems, and admin interfaces.
    Injection flaws allow external input to alter SQL, commands, or application behavior.
    Outdated software and weak configurations make public services easier to compromise.

Outside
Vulnerable People
4 External attackers often start with manipulation

    Phishing campaigns capture credentials, secrets, and approval actions.
    Malicious websites exploit browsers or convince users to download malware.
    Public information, metadata, and discarded material help attackers prepare tailored attacks.

Outside
Vulnerable Hardware and Locks
5 Physical weaknesses can become remote entry enablers

    Supply-chain compromise can insert malicious components before delivery.
    Malicious peripherals or backdoored devices may arrive by mail and look legitimate.
    Weak locks, tailgating, and poor visitor control expose infrastructure directly.

Perspective
From the Inside
6 Internal access changes the attacker’s advantages

    Once inside, attackers often face weaker segmentation and higher implicit trust.
    Internal compromise may begin through stolen credentials, malware, or rogue devices.
    The focus shifts from entry to movement, privilege gain, and persistence.

Inside
Vulnerable Network and Software
7 Internal trust often hides exploitable paths

    Rogue ethernet or wireless devices can create footholds inside the organization.
    Misconfigurations enable sniffing, spoofing, reconnaissance, and lateral movement.
    Privilege escalation and insecure internal software expand limited access into control.

Inside
Vulnerable People and Hardware
8 Internal compromise still depends on human and physical weakness

    Malware from unsafe browsing, USB media, or downloads can open internal paths.
    Malicious insiders or coerced employees may abuse legitimate access.
    Unencrypted devices, weak backup posture, and poor hardware policies increase impact.

Cross-Cutting
Human Factor
9 People connect outside and inside attack paths

    Human trust is exploited through urgency, deception, convenience, and habit.
    User mistakes can bypass otherwise strong technical controls.
    Security awareness matters, but clear procedures and safe defaults matter more.

Visual Example
Attack Surface Extension
Office network diagram showing internet, firewall, router, wireless clients, servers, printer, and internal clients.

Takeaway
Attack Vectors Are Connected, Not Isolated

Effective defense must consider external exposure, internal trust boundaries, hardware risks, and the human factor at every stage.



---

# Class 05 - Defense

Modern defense is not a wall. It is a continuous system of visibility, control, detection, and response.

Framing
1Defense Starts With the Right Model
Good defense is structured, not improvised

    The old perimeter-only mindset fails in a world of constant exposure.
    Defenders need models that explain how attacks unfold and where to interrupt them.
    The objective is resilience: make attacks harder, noisier, and more expensive.

Frameworks
2Kill Chain, Diamond, MITRE, NIST
Frameworks turn defense into an architecture

    The Cyber Kill Chain shows attack stages and where a defender can break them.
    The Diamond Model links adversary, capability, infrastructure, and victim.
    MITRE ATT&CK and NIST CSF give shared language for coverage, risk, and priorities.

[1] Cyber Kill Chain [2] Diamond Model [3] MITRE ATT&CK [4] NIST CSF

Visibility
3The Visibility Triad
You cannot defend what you cannot observe

    EDR gives host-level visibility into processes, files, and registry activity.
    NDR or network analytics reveal suspicious communication patterns and lateral movement.
    SIEM correlates logs from endpoints, networks, and services into a usable picture.

[1] EDR: Endpoint Detection and Response [2] NDR: Network Detection and Response [3] SIEM: Security Information and Event Management

Perimeter
4Network and Edge Controls
The outer layers still matter, but they are not enough

    NGFWs and WAFs filter malicious traffic and reduce exposure of internet-facing services.
    VPNs and DNS protection secure remote access and block known malicious destinations.
    DDoS protection helps preserve availability under flood and disruption attempts.

[1] NGFW: Next-Generation Firewall [2] WAF: Web Application Firewall [3] VPN: Virtual Private Network

Endpoint
5From Antivirus to EDR
Modern defense needs host-level ground truth

    Traditional antivirus is reactive and mostly tied to known signatures.
    EDR monitors process execution, registry changes, and file activity in real time.
    Tools like osquery and OSSEC make endpoints searchable, monitorable, and automatable.

[1] EDR: Endpoint Detection and Response

Detection
6IDS, SIEM, and Network Telemetry
Detection depends on correlation, not isolated alerts

    IDS and IPS engines like Snort or Suricata inspect traffic for suspicious behavior.
    SIEM platforms aggregate logs and support correlation across firewalls, servers, and endpoints.
    Zeek adds protocol-aware network visibility that helps surface subtle anomalies.

[1] IDS: Intrusion Detection System [2] IPS: Intrusion Prevention System [3] SIEM: Security Information and Event Management

Active Defense
7Deception as Detection
Decoys work because no legitimate user should touch them

    Honeypots such as Cowrie or ConPot attract attackers into controlled environments.
    Honeytokens like Canarytokens trigger immediate alerts when touched or opened.
    Deception is powerful because it creates high-confidence signals with low noise.

Operations
8SOC, XDR, and SOAR
Defense becomes real when people and automation meet

    The SOC is the operating model that monitors, investigates, and responds continuously.
    XDR combines endpoint, network, identity, and cloud signals into one investigative context.
    SOAR reduces analyst fatigue by automating repetitive containment and response playbooks.

[1] SOC: Security Operations Center [2] XDR: Extended Detection and Response [3] SOAR: Security Orchestration, Automation, and Response

After the Breach
9Forensics and Incident Response
Recovery depends on understanding what actually happened

    TheHive helps teams coordinate cases, tasks, and incident reporting.
    Cuckoo Sandbox and GRR Rapid Response support malware analysis and large-scale live forensics.
    Network forensics tools such as Xplico reconstruct activity from PCAP evidence.

Takeaway
10So, Is Defense Possible?
Perfect prevention is impossible, resilient defense is not

    Start with visibility, then add detection, response, and recovery discipline.
    Use frameworks to prioritize investment and measure coverage against real attacker behavior.
    Build a visible, automated, and well-practiced environment that raises attacker cost.

Closing
Defense Is Possible, but Never Perfected

The defender wins by making compromise harder to achieve, easier to detect, and faster to contain.


---



# Class 06 - Network Security

Attacks and defenses across the network stack: from Wi-Fi sniffing to DNS spoofing, SSL interception, firewalls, VPNs, and honeypots.

Framing
1Security by Layer
Each network layer exposes different attack surfaces

    Physical attacks target signals, cables, radios, and device access.
    Link and network attacks abuse local addressing, routing, and trust assumptions.
    Transport and application attacks manipulate sessions, names, and encrypted channels.

Physical Layer
2Signals Can Leak
Wireless traffic makes the physical layer visible

    Wi-Fi sniffing captures nearby radio traffic without touching the target device.
    Weak encryption or open networks turn passive observation into data exposure.
    Physical proximity often becomes the first requirement for local network attacks.

Link Layer
3Local Networks Are Trusting
Hubs, switches, and MAC addresses shape local exposure

    Packet sniffing observes frames that reach the attacker on the local segment.
    MAC addresses identify interfaces, but they are not strong identities.
    Switches reduce casual sniffing, but they do not remove link-layer attacks.

MAC: Media Access Control

Link Layer
4ARP and DHCP Spoofing
Local control protocols can be impersonated

    ARP spoofing poisons address mappings and can redirect traffic through the attacker.
    DHCP spoofing can hand out malicious gateways, DNS servers, or network settings.
    Both attacks rely on the local network accepting unauthenticated announcements.

ARP: Address Resolution Protocol DHCP: Dynamic Host Configuration Protocol DNS: Domain Name System

Availability
5DoS and Flooding
Availability is a security property too

    DoS attacks try to exhaust bandwidth, CPU, memory, queues, or protocol state.
    Ping floods overwhelm a target with ICMP echo traffic.
    SYN flooding abuses TCP handshakes by filling half-open connection tables.

DoS: Denial of Service ICMP: Internet Control Message Protocol TCP: Transmission Control Protocol

Network Layer
6IP Spoofing
Source addresses are data, not proof

    IP spoofing forges source addresses to hide origin or bypass weak filters.
    Spoofed packets support reflection, amplification, and some blind attacks.
    Filtering and traceback are needed because packets do not authenticate themselves.

IP: Internet Protocol

Transport Layer
7TCP Session Attacks
Sessions depend on state, sequence, and timing

    TCP sequence prediction guesses valid sequence numbers for blind injection.
    Blind injection inserts data without seeing the full traffic path.
    Complete session hijacking takes over an established connection.

TCP: Transmission Control Protocol

Reconnaissance
8Port Scanning
Scanning maps what a host exposes

    TCP and SYN scans test open ports by observing connection behavior.
    FIN, UDP, and idle scans use protocol edge cases to infer service state.
    Scan results guide exploitation by revealing services, filters, and reachable hosts.

SYN: synchronize flag FIN: finish flag UDP: User Datagram Protocol

Application Layer
9DNS and SSL Interception
Names and encrypted channels are frequent targets

    DNS spoofing redirects names to attacker-controlled destinations.
    Pharming changes name resolution so users reach fake services transparently.
    SSL MITM attempts to intercept encrypted traffic by abusing trust or certificates.

DNS: Domain Name System SSL: Secure Sockets Layer MITM: Man in the Middle

Defenses
10Secure Channels and Encryption
Confidentiality and authenticity need cryptographic support

    VPNs create encrypted tunnels over untrusted networks.
    SSH and SCP protect remote administration and file transfer.
    Encryption reduces the value of sniffing and interception when keys are protected.

VPN: Virtual Private Network SSH: Secure Shell SCP: Secure Copy Protocol

Defenses
11Control, Trace, and Deceive
Network defense combines blocking, visibility, and traps

    Firewalls restrict traffic by policy and reduce exposed services.
    Port knocking hides services until a valid connection sequence is observed.
    Honeypots and IP traceback help detect attackers and reconstruct paths.

Closing
Secure the Path, Not Just the Endpoint

Protecting systems also means protecting the routes, sessions, names, and protocols that connect them.



---


# Class 07 - Social Engineering



Class #07
Social Engineering

How attackers exploit trust, urgency, routine, and organizational process to turn people into entry points.

Framing
1People Are Part of the System
Social engineering is not separate from technical compromise

    Attackers influence people into revealing information, granting access, or taking unsafe actions.
    Many incidents begin when a person trusts the wrong message, identity, device, or website.
    The human factor often becomes the entry point for later technical exploitation.

Psychology
2Trust, Pressure, Habit
The attack targets context and behavior

    Trust in colleagues, institutions, brands, and authority figures can be abused.
    Urgency pushes victims to act before verifying the request.
    Convenience and repeated prompts train users to approve actions automatically.

Techniques
3Phishing Families
Different channels, same objective: manipulate trust

    Phishing uses broad messages to steal credentials, deliver malware, or redirect users.
    Spear phishing and whaling target specific people with tailored context.
    Vishing and smishing use voice calls, SMS, or messaging apps to create immediacy.

SMS: Short Message Service

Techniques
4Pretext, Bait, Impersonation
The story gives the victim a reason to comply

    Pretexting invents a believable scenario that justifies the request.
    Impersonation borrows authority from IT, managers, vendors, auditors, or delivery staff.
    Baiting and quid pro quo exploit curiosity, helpfulness, greed, or convenience.

Reconnaissance
5OSINT Makes It Personal
Public information becomes attack material

    Websites, social media, job posts, repositories, and documents reveal useful details.
    Attackers collect names, roles, suppliers, technologies, and internal vocabulary.
    Metadata can expose usernames, software versions, locations, or document history.

OSINT: Open Source Intelligence

Targeting
6Profiles Become Pretexts
Small facts combine into convincing stories

    Targets are selected by access, influence, habits, or likelihood of responding.
    Finance, HR, IT, support, and management are frequent high-value targets.
    Projects, invoices, outages, and events can become hooks for credible requests.

HR: Human Resources IT: Information Technology

Tooling
7SET and Simulation Tools
Tools help teach workflow, scope, and defensive lessons

    SET is a classic framework for authorized security testing and awareness exercises.
    Gophish supports controlled phishing campaigns and reporting-behavior measurement.
    Simulations should improve processes, not shame individual users.

SET: Social Engineer Toolkit

Modern Tooling
8Modern Attack Platforms
Modern tooling lowers cost and increases realism

    Evilginx2 illustrates adversary-in-the-middle phishing and session-token theft risk.
    Zphisher, Fluxion, Doppel, Sliver, and Mythic C2 show adjacent abuse patterns.
    LLM-based agents can tailor messages, simulate conversations, and scale personalization.

C2: Command and Control LLM: Large Language Model

Physical
9Physical and Hybrid Attacks
Not every social engineering attack starts in email

    Tailgating abuses politeness and social pressure to enter restricted spaces.
    USB drops and rogue peripherals exploit curiosity and device trust.
    Hybrid attacks combine email, phone calls, fake websites, and physical delivery.

USB: Universal Serial Bus

Defense
10Reduce Damage, Improve Reporting
Fast reporting matters more than perfect behavior

    Users need simple ways to report suspicious messages, calls, devices, or visitors.
    Sensitive requests should be verified through independent channels.
    Training should be realistic, repeated, and connected to actual workflows.

Defense
11Technical and Cultural Controls
Awareness works best when systems are designed for mistakes

    MFA reduces damage from stolen passwords, especially phishing-resistant methods.
    Email filtering, endpoint controls, and conditional access reduce exposure.
    A healthy culture makes verification normal, not rude or suspicious.

MFA: Multi-Factor Authentication

Boundaries
12Ethics and Authorization
Social engineering tests need explicit permission

    Scope must define targets, techniques, data collection, and stopping conditions.
    Collected data should be minimized, protected, and deleted according to policy.
    Reports should focus on systemic weaknesses rather than public individual blame.

Closing
Design for Human Reality

Social engineering cannot be solved by telling people to never make mistakes; defense must make verification easy and mistakes survivable.


