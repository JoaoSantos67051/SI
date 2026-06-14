## Summary — *Phishing Attacks Survey: Types, Vectors, and Technical Approaches*

This paper is a broad survey of phishing attacks. Its main goal is to explain **how phishing works**, what forms it can take, which technical methods attackers use, and which anti-phishing defenses exist. The author argues that phishing remains a serious cybersecurity problem because attackers continuously adapt their methods, use new platforms, and combine technical tricks with social engineering. 

## Main objective

The paper aims to create awareness about phishing by reviewing:

* classic phishing techniques;
* modern phishing techniques;
* emerging/cutting-edge phishing attacks;
* phishing vectors and media;
* technical approaches used by attackers;
* prevention and detection methods.

The author also notes that much research focuses on **anti-phishing defenses**, while fewer works explain phishing techniques in detail. This paper tries to fill that gap. 

## Definition of phishing

Phishing is described as a **social engineering technique** where the attacker manipulates the victim into revealing sensitive information, such as:

* usernames;
* passwords;
* financial information;
* email credentials;
* personal data.

The attacker usually uses “bait”, such as fake emails, fake websites, fraudulent messages, malware, or impersonation, to trick the victim. 

## Why phishing is still dangerous

The paper shows that phishing is not just a simple email scam. It can lead to:

* credential theft;
* financial fraud;
* malware infection;
* account takeover;
* corporate breaches;
* attacks on critical infrastructure.

One example discussed is the **2015 Ukraine power grid attack**, where spear phishing emails with malicious Microsoft Word documents helped attackers install malware and shut down substations, leaving around **230,000 people without power**. 

## Phishing lifecycle

The paper describes phishing as a process with several stages:

| Stage                                | Meaning                                                         |
| ------------------------------------ | --------------------------------------------------------------- |
| **Planning**                         | The attacker chooses targets, goals, tools and methods          |
| **Phishing**                         | The attack is launched through email, SMS, website, voice, etc. |
| **Infiltration**                     | The victim reacts and the attacker gains access or data         |
| **Data collection and exploitation** | The stolen data is used for fraud, access or sale               |
| **Exfiltration**                     | The attacker removes traces and may evaluate the attack         |

This lifecycle is useful because it shows that phishing is not only the message itself, but a complete attack process. 

## Main classification: medium, vector and technical approach

A key contribution of the paper is the classification of phishing into three connected dimensions:

| Dimension              | Meaning                                                          |
| ---------------------- | ---------------------------------------------------------------- |
| **Medium**             | The communication method used to reach the victim                |
| **Vector**             | The channel through which the attack is carried out              |
| **Technical approach** | The technique used to steal information or compromise the victim |

The diagram on page 7 maps different **media** to different **vectors**, showing that phishing can happen through voice, SMS/MMS and the internet, not only through email. 

## Phishing media and vectors

The paper identifies three main media:

1. **Voice**
2. **SMS/MMS**
3. **Internet**

From these media, several phishing vectors appear:

| Vector                         | Explanation                                                 |
| ------------------------------ | ----------------------------------------------------------- |
| **Vishing**                    | Phishing through voice calls                                |
| **Smishing**                   | Phishing through SMS/MMS                                    |
| **Email phishing**             | Fraudulent emails designed to steal data or deliver malware |
| **eFax phishing**              | Fake fax-like digital messages                              |
| **Instant messaging phishing** | Attacks through WhatsApp, Telegram, Messenger, etc.         |
| **Social network phishing**    | Fake profiles, fake posts, fake promotions or impersonation |
| **Website phishing**           | Fake websites designed to look legitimate                   |
| **Wi-Fi phishing**             | Attacks through rogue access points or public hotspots      |

This is important for your topic because it shows that **modern phishing is multi-channel**. Security filters focused only on email are not enough. 

## Main technical approaches

The paper reviews many phishing techniques. The most important are:

### Spear phishing

A targeted form of phishing where the attacker researches the victim and creates a personalized message. It often uses psychological principles such as authority, scarcity, trust, urgency and social proof. 

### Whaling

A form of spear phishing aimed at high-level executives or people with privileged access. The goal is often to steal sensitive corporate information or install malware. 

### Business Email Compromise

BEC targets organizations by impersonating employees, executives or business partners. The attacker often tries to trick someone into transferring money, changing payroll details or sending sensitive data. The paper notes that BEC can be very difficult to detect automatically because the messages may not contain obvious malware or suspicious links. 

### Cross-Site Scripting

XSS is used to inject malicious scripts into vulnerable websites. These scripts can steal cookies, session data or other sensitive information from the victim’s browser. 

### QRishing

QRishing uses QR codes to send victims to malicious websites or trigger malware downloads. This is dangerous because humans cannot easily read the destination of a QR code before scanning it. 

### Drive-by download

The victim is tricked into visiting a website or opening content that silently downloads malware. This malware can include spyware, trojans, botnet malware or keyloggers. 

### Malvertising

Attackers use malicious online advertisements to infect victims. A major problem is that these ads may appear on legitimate websites, making users trust them. 

### Wiphishing / evil twin attack

The attacker creates a fake Wi-Fi access point that looks legitimate. When users connect, the attacker can intercept traffic or redirect them to malicious pages. 

### Typo squatting and sound squatting

Typo squatting uses domains similar to real domains, such as misspelled brand names. Sound squatting targets voice assistants by creating malicious commands or apps with names that sound like legitimate ones. 

### GUI-squatting

This is a mobile phishing technique where attackers automatically generate fake app login screens that look like real apps. The paper describes this as especially concerning because fake apps can be generated quickly and may bypass several anti-phishing techniques. 

## Phishing-as-a-Service

The paper explains that phishing has become easier because attackers can buy ready-made tools and services.

Examples include:

* phishing kits;
* fake website templates;
* malware toolkits;
* Phishing-as-a-Service platforms;
* phishing simulation tools that can also be abused.

This lowers the technical barrier for attackers, meaning even less skilled criminals can launch phishing campaigns. 

## Anti-phishing techniques

The paper divides anti-phishing defenses into non-technical and technical methods.

### Non-technical methods

| Method             | Explanation                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| **Legal measures** | Laws and prosecution can deter some attackers                          |
| **Education**      | Users are trained to recognize phishing emails and suspicious behavior |

The paper highlights education as important, but not sufficient on its own.

### Technical methods

| Method                          | Explanation                                         |
| ------------------------------- | --------------------------------------------------- |
| **Blacklisting**                | Blocks known malicious domains or URLs              |
| **Whitelisting**                | Allows only known legitimate sites                  |
| **Heuristic detection**         | Detects suspicious features in emails or websites   |
| **Visual similarity detection** | Compares suspicious websites with legitimate brands |
| **Machine learning**            | Classifies phishing based on learned patterns       |

The paper states that machine learning is promising because phishing detection is essentially a classification problem. However, ML effectiveness depends heavily on dataset quality, training data and model tuning. 

## Main limitations of current defenses

The paper argues that there is still no complete solution to phishing because:

* phishing uses many different media and vectors;
* attackers constantly change techniques;
* blacklists are often too slow for new attacks;
* phishing websites increasingly use HTTPS, so HTTPS alone is no longer a sign of safety;
* mobile phishing is harder to detect than desktop phishing;
* users often ignore warnings or lack cybersecurity knowledge;
* attackers use semantic changes to bypass filters;
* phishing may be only the first step in larger attacks.

This is very useful for your article because it directly supports the idea that **traditional security filters are limited against modern phishing**. 

## Relevance for your project

For your theme **“Modern Phishing vs. Security Filters”**, this paper is useful because it gives you a broad foundation. You can use it to explain:

* what phishing is;
* why phishing is still effective;
* how phishing evolved beyond email;
* what types of phishing exist;
* why user education alone is not enough;
* why technical filters need to evolve;
* why modern phishing requires layered defense.

It also gives you many examples for your introduction and literature review, especially spear phishing, BEC, QRishing, smishing, vishing, mobile phishing and social media phishing.

## Final takeaway

The main conclusion is that phishing is a persistent and evolving threat. It is no longer limited to fake emails, but now includes SMS, voice calls, social media, QR codes, Wi-Fi, mobile apps, browser attacks and cloud-based attacks.

The strongest idea for your paper is:

> Modern phishing is successful because it combines human manipulation with technical deception. Therefore, security filters must go beyond simple blacklists and rule-based detection, combining machine learning, URL analysis, visual similarity checks, user education, endpoint protection and multi-channel monitoring.
