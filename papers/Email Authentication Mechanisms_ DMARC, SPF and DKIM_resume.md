## Summary — *Email Authentication Mechanisms: DMARC, SPF and DKIM*

This NIST Technical Note explains how **SPF, DKIM and DMARC** work together to improve email authentication and reduce problems such as **spoofing, phishing and message modification**. It also describes a NIST test system called **Pythentic**, created to test whether domains have correctly configured these mechanisms. 

## Main problem

The paper starts by explaining that the original **SMTP** email protocol was not designed with strong security. Because of this, three major problems became common:

| Problem                            | Meaning                                                                   |
| ---------------------------------- | ------------------------------------------------------------------------- |
| **From address spoofing**          | An attacker can make an email appear to come from another domain          |
| **Phishing**                       | An attacker uses deceptive emails and links to steal credentials or money |
| **Man-in-the-middle modification** | A message can be changed in transit if there is no integrity protection   |

The paper argues that email needs mechanisms to verify whether the sender is authorized and whether the message has been modified. 

## SPF — Sender Policy Framework

**SPF** allows a domain owner to publish DNS records listing which IP addresses are allowed to send email for that domain.

Example logic:

* if an email claims to come from `example.com`;
* the receiving server checks the SPF record of `example.com`;
* if the sending IP address is authorized, SPF passes;
* otherwise, SPF fails.

SPF is useful against spoofing because it links a domain to authorized sending servers. However, SPF mainly checks the **envelope sender** and the sending IP address, not necessarily the visible “From” address that the user sees. 

## DKIM — DomainKeys Identified Mail

**DKIM** uses cryptographic signatures. The sending server signs selected parts of the email using a private key. The receiving server retrieves the corresponding public key from DNS and verifies the signature.

DKIM helps prove two things:

1. the message was signed by a domain that owns the private key;
2. the signed parts of the message were not modified in transit.

However, DKIM only protects the parts of the email that are included in the signature. If some headers or parts of the message are not signed, there may still be weaknesses. 

## DMARC — Domain-based Message Authentication, Reporting and Conformance

**DMARC** builds on SPF and DKIM. Its purpose is to connect authentication results to the visible domain in the email’s **From** header.

DMARC does three main things:

1. authenticates messages using SPF and/or DKIM;
2. tells receiving servers what to do when authentication fails;
3. provides reports back to domain owners about how their domain is being used or abused.

A DMARC policy can tell receivers to:

* do nothing special: `p=none`;
* quarantine suspicious messages;
* reject failed messages.

This reporting feature is important because it allows domain owners to see whether attackers are spoofing their domains. 

## How the three mechanisms work together

The key point is that **SPF, DKIM and DMARC are stronger together than separately**.

| Mechanism | Protects mainly against      | Main function                                                           |
| --------- | ---------------------------- | ----------------------------------------------------------------------- |
| **SPF**   | Unauthorized sending servers | Checks if the sender IP is allowed                                      |
| **DKIM**  | Message tampering            | Verifies cryptographic signature                                        |
| **DMARC** | Domain spoofing              | Aligns SPF/DKIM with the visible From domain and gives policy/reporting |

The paper stresses that there is no single “big bang” solution for securing email. Instead, secure email depends on multiple complementary protocols. 

## Pythentic test system

A large part of the paper describes **Pythentic**, a NIST test system for SPF, DKIM and DMARC.

The system lets a domain owner send an email to a test address. Then Pythentic analyzes the message and sends back a report showing whether SPF, DKIM and DMARC passed or failed.

The system includes several components:

* correspondent/user;
* DNS records;
* web interface;
* Sendmail;
* sending milter;
* receiving milter;
* DMARC reporter;
* database.

The diagram on page 10 shows these components and how the test system receives an email, checks the DNS records, performs SPF/DKIM/DMARC authentication and stores the results. 

## What Pythentic checks

The system can test:

* SPF records;
* DKIM signatures;
* DMARC records;
* spoofed email scenarios;
* bad DKIM signatures;
* malformed DKIM headers;
* forensic reporting.

For example, a domain can send a message with subject `dmarc`, `spf`, `dkim` or `test`, and Pythentic returns a detailed authentication report. The paper includes a full example using a Gmail sender, where SPF, DKIM and DMARC all pass and the message is delivered. 

## Experience and results

The system had been running since 2012, and the paper analyses its use over several years.

Some important observations:

* use of the test system increased over time;
* many different domains and top-level domains used it;
* legitimate test messages were usually delivered correctly;
* suspicious/spam-like messages were often discarded or rejected;
* combining SPF and DKIM improves authentication coverage.

The paper also compares SPF and DKIM results. It notes that only one successful SPF or DKIM result is needed for DMARC authentication, depending on alignment and policy. The results suggest that SPF was often more effective as a standalone mechanism in their dataset, but that the combination of SPF and DKIM provides stronger coverage. 

## Important warning about SPF `+all`

One practical finding is the misuse of SPF records ending in `+all`.

In SPF, `-all` usually means “no other IP addresses are authorized.” But `+all` means “all IP addresses are allowed.” That makes SPF almost useless, because any sender can pass SPF.

The paper observes that some spammers appear to use this trick and recommends treating `+all` as an error when processing SPF records. 

## Limitations and challenges

The paper also explains that SPF, DKIM and DMARC need careful configuration.

Some problems include:

* mail forwarding can break SPF because the forwarding server changes the source IP;
* mailing lists or footer additions can break DKIM signatures;
* DMARC reporting creates a burden for receiving domains;
* small organizations may not send aggregate reports;
* DNS records must be correctly configured;
* authentication policies must be tuned carefully before being enforced strictly.

So, while these mechanisms are useful, they are not automatic solutions. Poor configuration can reduce their effectiveness. 

## Relevance for your project

This paper is very useful for **“Modern Phishing vs. Security Filters”** because it explains the technical foundations behind email authentication.

You can use it to support these ideas:

* phishing often relies on spoofed sender identities;
* SPF, DKIM and DMARC are core defenses against email spoofing;
* email authentication helps filters decide whether a message is trustworthy;
* DMARC is especially important because it connects authentication results to the visible From domain;
* technical filters still need correct configuration;
* authentication mechanisms reduce phishing risk, but do not eliminate phishing completely.

## Final takeaway

The main conclusion is that **SPF, DKIM and DMARC are essential layers in modern email security**. SPF checks whether the sending server is authorized, DKIM checks message integrity through signatures, and DMARC connects these checks to domain policy and reporting.

For your article, this paper is useful as the technical base for explaining how security filters authenticate emails before deciding whether to deliver, quarantine or reject them.
