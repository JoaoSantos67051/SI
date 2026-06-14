## Summary — *Composition Kills: A Case Study of Email Sender Authentication*

This paper analyses weaknesses in **email sender authentication**, especially in systems that use **SPF, DKIM and DMARC** to prevent spoofed emails. The main argument is that these mechanisms can fail not necessarily because each individual component is badly designed, but because different components interpret the same email differently. This creates inconsistencies that attackers can exploit. 

## Main idea

The title **“Composition Kills”** refers to the problem of combining several software components. Email systems are built from many parts: sending servers, receiving servers, DNS, SPF validators, DKIM validators, DMARC validators and mail clients. Each component may be correct on its own, but when combined, small differences in parsing or interpretation can create serious vulnerabilities. 

The authors show that attackers can exploit these inconsistencies to make forged emails appear as if they were legitimately sent by trusted domains.

## Background: SPF, DKIM and DMARC

The paper explains three main email authentication mechanisms:

| Mechanism | Purpose                                                                                 | Main limitation                                                          |
| --------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **SPF**   | Checks whether a sending server is allowed to send emails for a domain                  | It checks the sending server, not necessarily the visible “From” address |
| **DKIM**  | Uses cryptographic signatures to verify that parts of the email were signed by a domain | Not all headers/body parts may be protected                              |
| **DMARC** | Aligns SPF/DKIM results with the visible “From” domain                                  | Depends on consistent interpretation between components                  |

The important point is that SPF and DKIM alone do not fully protect the visible sender address. DMARC was created to fix this by checking alignment with the **From** header, but the paper shows that this alignment can still be bypassed when components interpret headers differently. 

## Methodology

The authors tested:

* **10 popular email providers**;
* **19 email clients**, including web, desktop and mobile clients;
* different combinations of server-side and client-side interpretation.

They used manual analysis and black-box testing to identify inconsistencies. They found **18 types of evasion exploits**, and all tested systems were vulnerable to at least some attacks. 

## Main attack categories

The paper groups the attacks into three major classes.

### 1. Intra-server attacks

These attacks exploit inconsistencies **inside the same email server**, for example between SPF, DKIM, DMARC and DNS components.

The idea is that one component may verify one identity, while another component uses a different identity for alignment. This can lead to a spoofed email passing authentication checks.

The paper discusses cases such as:

* confusion between HELO and MAIL FROM identities;
* ambiguous domains;
* injection into authentication results;
* differences between DKIM, SPF and DMARC parsing. 

### 2. UI-mismatch attacks

These attacks exploit inconsistencies between what the **server authenticates** and what the **email client displays** to the user.

For example, the server may authenticate one sender address, but the email client may display another address. This is especially dangerous because the user sees a trusted sender, even though that address was not actually authenticated.

The paper shows that ambiguous **From** headers, multiple sender addresses, encoded addresses, comments, spacing and obsolete email syntax can cause different systems to interpret the same email differently. 

### 3. Ambiguous-replay attacks

These attacks exploit weaknesses in DKIM signatures. DKIM signs parts of the email, but not always all headers or all body content. If some parts are not signed, an attacker may replay a previously legitimate signed email and modify or add content without breaking the signature.

The paper highlights that DKIM replay is a known issue, but many real-world deployments still fail to apply strong protections. 

## Key findings

The most important findings are:

* SPF, DKIM and DMARC are useful, but they are not perfect.
* Many vulnerabilities arise from **inconsistent parsing** between components.
* Email syntax is complex, old and permissive, which creates many edge cases.
* A message can pass authentication on the server but still be displayed misleadingly to the user.
* DKIM signatures can be abused if important headers are not signed.
* Even large providers and popular mail clients were affected by some of the tested attacks. 

## Mitigation strategies

The authors suggest several defenses:

* DKIM signatures should include all important headers.
* DKIM signers should avoid using the optional body length tag, because it can allow content to be appended.
* Email clients should display authentication results more clearly.
* Servers should normalize or reject ambiguous/malformed headers.
* Mail servers should pass verified authentication information directly to clients instead of forcing clients to re-parse complex messages.
* Protocol designers should reduce ambiguity in text-based protocols. 

## Relevance for your project

This paper is very useful for your topic **“Modern Phishing vs. Security Filters”** because it shows that phishing defense is not only about detecting suspicious words or malicious links.

It proves that attackers can also exploit weaknesses in the **email authentication infrastructure** itself. Even if SPF, DKIM and DMARC are deployed, phishing emails can still appear credible if different components disagree about what sender was actually authenticated.

You can use this paper in your article to support this argument:

> Modern phishing filters must not rely only on sender authentication mechanisms such as SPF, DKIM and DMARC. These mechanisms are important, but their effectiveness depends on correct implementation, consistent parsing and clear presentation to the user.

## Final takeaway

The main conclusion is that **email authentication is fragile because it depends on many components working consistently together**. SPF, DKIM and DMARC improve security, but they do not completely solve phishing and spoofing. In modern phishing defense, filters must combine technical authentication, content analysis, URL analysis, client-side warning design and careful handling of ambiguous email structures.
