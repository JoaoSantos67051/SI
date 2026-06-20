# Lab #05 — HoneyTokens and CanaryTokens

## Index

* [1. Objective](#1-objective)
* [2. What Are HoneyTokens and CanaryTokens?](#2-what-are-honeytokens-and-canarytokens)
* [3. Purpose and Relevance](#3-purpose-and-relevance)
* [4. Effectiveness](#4-effectiveness)
* [5. Practical Examples](#5-practical-examples)
* [6. Limitations](#6-limitations)
* [7. Conclusion](#7-conclusion)
* [8. References](#8-references)

---

## 1. Objective

The objective of this lab is to briefly describe the purpose, relevance, and effectiveness of **HoneyTokens** and **CanaryTokens** in modern system security.

This topic is related to modern defense and detection techniques, especially deception-based detection.


## 2. What Are HoneyTokens and CanaryTokens?

**HoneyTokens** are fake but realistic digital assets placed inside a system to detect suspicious activity. They should not be used by legitimate users, so any interaction with them is a strong sign that something unusual or malicious may be happening.

Examples of HoneyTokens include:

* Fake credentials.
* Fake API keys.
* Fake documents.
* Fake database records.
* Fake cloud secrets.
* Fake links or URLs.

**CanaryTokens** are a practical implementation of this idea. A CanaryToken is a small trap that triggers an alert when it is opened, accessed, or used.

For example, if an attacker opens a fake document or uses a fake API key, the security team can receive an alert with information such as the time, IP address, and type of interaction.


## 3. Purpose and Relevance

HoneyTokens and CanaryTokens are useful because they help detect attackers after initial access.

Traditional tools such as firewalls, antivirus, SIEM, and EDR are important, but they often depend on known patterns, rules, or suspicious behavior. Deception techniques work differently: they create fake assets that legitimate users should not touch.

This makes alerts more reliable because:

* A normal user should not use a fake secret.
* A normal process should not access a fake credential.
* A normal administrator should not open a fake sensitive file.
* An attacker performing reconnaissance may interact with the fake asset.

This is connected to the idea studied in class that defense is not only prevention. Modern defense also needs visibility, detection, response, and recovery.


## 4. Effectiveness

HoneyTokens and CanaryTokens can be effective because they create **high-confidence alerts**.

Their main advantages are:

| Advantage                | Explanation                                                                  |
| ------------------------ | ---------------------------------------------------------------------------- |
| Low noise                | Legitimate users should not interact with fake assets.                       |
| Fast detection           | Alerts are triggered as soon as the token is touched.                        |
| Simple deployment        | Tokens can be placed in files, repositories, systems, or cloud environments. |
| Good for insider threats | They can detect suspicious activity by users already inside the network.     |
| Useful after breach      | They help detect lateral movement, credential theft, and reconnaissance.     |

However, they are not a complete security solution. They should complement other controls such as patching, least privilege, logging, SIEM, EDR, and incident response.



## 5. Practical Examples

Some practical uses of HoneyTokens and CanaryTokens are:

| Example                              | Detection Goal                                    |
| ------------------------------------ | ------------------------------------------------- |
| Fake API key in a private repository | Detect secret scanning or repository compromise.  |
| Fake document named `Passwords.xlsx` | Detect unauthorized file access.                  |
| Fake administrator credential        | Detect credential theft or lateral movement.      |
| Fake AWS key                         | Detect cloud credential abuse.                    |
| Fake internal URL                    | Detect reconnaissance or phishing infrastructure. |
| Fake database record                 | Detect unauthorized database access.              |

A simple example would be placing a fake file in a shared folder. If nobody should open that file, then any access to it should generate an alert and be investigated.


## 6. Limitations

HoneyTokens and CanaryTokens also have limitations:

* They do not prevent attacks by themselves.
* They only work if the attacker interacts with them.
* Poorly placed tokens may never be touched.
* If tokens are too obvious, attackers may avoid them.
* Alerts still need investigation and response.
* They must be managed carefully to avoid confusion with real assets.

Because of this, HoneyTokens should be part of a broader security strategy, not the only defense mechanism.



## 7. Conclusion

HoneyTokens and CanaryTokens are useful deception-based detection mechanisms. Their purpose is to create fake but realistic assets that trigger alerts when accessed.

They are especially relevant in modern security because organizations must assume that prevention can fail. If an attacker bypasses the first layers of defense, HoneyTokens can help detect reconnaissance, credential theft, lateral movement, and insider threats.

Their effectiveness comes from the fact that legitimate users should not interact with them, which makes alerts more meaningful and usually less noisy. However, they should be used together with other controls such as SIEM, EDR, least privilege, logging, patch management, and incident response.

In conclusion, HoneyTokens and CanaryTokens do not replace traditional security tools, but they add an important detection layer that can help defenders discover suspicious activity faster.



## 8. References

* CanaryTokens: https://canarytokens.org/nest/
* CanaryTokens GitHub Repository: https://github.com/thinkst/canarytokens
* Tracebit: https://tracebit.com/
* Class 05 — Defense
* Class 06 — Network Security
   

