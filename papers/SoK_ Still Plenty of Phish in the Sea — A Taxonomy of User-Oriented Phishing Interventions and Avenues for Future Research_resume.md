## Summary — *SoK: Still Plenty of Phish in the Sea — A Taxonomy of User-Oriented Phishing Interventions and Avenues for Future Research*

This paper is a **Systematization of Knowledge (SoK)** about **user-oriented anti-phishing interventions**. Instead of focusing mainly on technical filters, machine learning, blacklists or email authentication, the paper studies how research has tried to help **users** recognize and avoid phishing attacks. 

## Main objective

The authors wanted to understand:

1. what types of user-oriented phishing interventions already exist;
2. how these interventions try to guide users toward safer behavior;
3. which phishing attack vectors they address;
4. when the intervention happens in the user’s decision process;
5. whether the intervention requires active user interaction;
6. what research gaps still exist. 

The central idea is that users are often the **last line of defense** against phishing, but current interventions are fragmented across different areas such as cybersecurity, human-computer interaction and psychology.

## Methodology

The authors conducted a **systematic literature review** using the **PRISMA** methodology. They searched academic databases such as:

* ACM Digital Library;
* IEEE Xplore;
* Web of Science;
* USENIX/SOUPS;
* NDSS/USEC/EuroUSEC.

They initially identified **2,124 publications**. After screening titles, abstracts and full texts, they selected **64 articles** for detailed analysis. The **PRISMA diagram on page 4** shows this filtering process from the initial search to the final sample. 

## Main taxonomy of phishing interventions

The paper’s biggest contribution is a taxonomy of user-oriented phishing interventions. The **taxonomy diagram on page 6, Figure 2**, divides interventions into four main categories:

| Category              | Meaning                                                    |
| --------------------- | ---------------------------------------------------------- |
| **Education**         | Teaches users about phishing and how to protect themselves |
| **Training**          | Gives users practical exercises to recognize phishing      |
| **Awareness-raising** | Warns users during the risky action                        |
| **Design**            | Changes interface design to guide safer behavior           |

This taxonomy is useful for your project because it shows that anti-phishing protection is not only about technical filters. It also depends on how users are trained, warned and supported by interface design. 

## 1. Education interventions

Education interventions aim to develop users’ knowledge about phishing.

Examples include:

* text-based materials;
* videos;
* classroom training;
* explanations about phishing risks;
* information about how to recognize suspicious emails or websites.

The paper notes that education can help, but education alone is often not enough. Users may understand phishing in theory but still fail to notice attacks in real situations, especially when they are busy with their main task, such as answering emails or doing online work. 

## 2. Training interventions

Training goes further than education because it includes hands-on practice.

The paper identifies three main types of training:

| Type                           | Example                                               |
| ------------------------------ | ----------------------------------------------------- |
| **Serious games**              | Games such as Anti-Phishing Phil or NoPhish           |
| **Embedded training**          | Simulated phishing emails followed by feedback        |
| **Mindfulness-based training** | Training users to stop, think and check before acting |

A major example discussed is **PhishGuru**, where users receive simulated phishing emails. If they click, they are redirected to a training page explaining what happened and how to avoid similar attacks.

The paper considers embedded training promising because it happens in a realistic context. Instead of learning in an artificial classroom, users learn when they actually make a mistake. 

## 3. Awareness-raising interventions

Awareness-raising interventions happen **during the user’s action**. They try to interrupt or guide the user when they are about to do something risky.

Examples include:

* browser warnings;
* email warnings;
* warning banners;
* forced-attention warnings;
* link-focused warnings;
* security questions;
* fear appeals.

The paper distinguishes between:

| Type                     | Meaning                                               |
| ------------------------ | ----------------------------------------------------- |
| **Passive warnings**     | Show information but do not interrupt the user        |
| **Interactive warnings** | Require the user to make a decision before continuing |

A key finding is that **passive warnings are often ineffective**, because users ignore them or do not notice them. Interactive warnings tend to work better because they force users to stop and think. However, they can also interrupt users and create frustration. 

## 4. Design interventions

Design interventions try to make secure behavior easier through interface design.

Examples include:

* domain highlighting;
* sender highlighting;
* color codes;
* customized login indicators;
* trust logos;
* dynamic security skins;
* browser sidebars;
* tools that suggest safer websites;
* delayed password disclosure.

For example, highlighting the domain in a URL can help users focus on the important part of the link. However, the paper notes that some design interventions have limited success because users may not understand what the indicators mean or may confuse real security indicators with fake trust signals. 

## Attack vectors addressed

The paper also analyses which phishing attack vectors are most studied.

The **chart on page 9, Figure 3**, shows that most interventions focus on **URLs**, with **33 publications** addressing malicious links. Other common vectors include:

| Attack vector      | Number of publications |
| ------------------ | ---------------------: |
| URL                |                     33 |
| Email message      |                     17 |
| Authentication     |                     12 |
| Website            |                     10 |
| SSL/TLS            |                      4 |
| Malware            |                      3 |
| QR code            |                      1 |
| Mobile application |                      1 |

This is an important result because it shows a research imbalance. Most user-oriented interventions focus on links and emails, while very few focus on QR phishing, malicious attachments, mobile apps or malware. 

## Timing of the intervention

The paper also classifies interventions by when they happen in the user’s decision process.

| Timing              | Meaning                                    |
| ------------------- | ------------------------------------------ |
| **Pre-decision**    | Before the user faces a phishing situation |
| **During decision** | While the user is deciding what to do      |
| **Post-decision**   | After the user has already acted           |

Examples:

* **Pre-decision**: training videos, games, classroom education.
* **During decision**: browser warning, email warning, link warning.
* **Post-decision**: embedded training after the user clicks a simulated phishing email.

The paper finds that many interventions happen before or during the decision, but fewer study long-term effects or repeated interventions. The **chart on page 10, Figure 4**, summarizes this distribution. 

## User interaction: passive vs. interactive

The paper also studies whether interventions require active user interaction.

Out of the 64 articles:

* **48** describe interactive interventions;
* **16** describe passive interventions.

Interactive interventions are usually more effective because they force attention, but they also create more friction. Passive interventions are less intrusive, but users often ignore them. 

This creates one of the biggest trade-offs in anti-phishing design:

> Stronger interventions may protect users better, but they can also interrupt work, reduce productivity and cause frustration.

## Main criticism: user burden and friction

One of the strongest points of the paper is that many anti-phishing interventions place too much responsibility on the user.

For example, users may be expected to:

* play training games;
* read warnings;
* inspect URLs;
* answer security questions;
* wait before clicking links;
* remember training content;
* identify suspicious details under time pressure.

The authors argue that phishing detection is usually a **secondary task** for users. A person reading emails is mainly trying to work, answer colleagues, check invoices or complete a task — not perform security analysis. This makes many interventions unrealistic. 

## Digital nudging

The paper suggests that **digital nudges** may be a promising direction.

Digital nudges are small interface design choices that guide users toward safer behavior without forcing them too aggressively.

Examples could include:

* highlighting the real domain of a link;
* showing the domain next to a link;
* using clear just-in-time prompts;
* warning only when risk is meaningful;
* showing social comparison, such as how colleagues responded to similar emails;
* making risks more concrete and understandable.

The paper argues that nudges could reduce phishing risk while creating less friction than intrusive warnings or long training sessions. 

## Cognitive frame shift

Another important idea is that experts detect phishing by shifting from a normal reading mode to an investigation mode.

In simple terms:

1. The user first tries to understand the email normally.
2. Something seems suspicious.
3. The user starts investigating.
4. The user deletes, reports or avoids the phishing attempt.

The problem is that many normal users never make that shift from “this is just an email” to “I should investigate this”. The paper argues that future interventions should help users notice when something is “off” and support that cognitive switch. 

## Research gaps

The paper identifies several major gaps:

1. **Too much focus on URLs**
   Many studies focus on malicious links, but phishing also uses attachments, QR codes, mobile apps and fake authentication flows.

2. **Not enough focus on malware**
   Only a few studies address malicious files, even though phishing is often used to deliver malware and ransomware.

3. **Limited study of long-term effects**
   Many interventions are tested once, but real users face phishing repeatedly over time.

4. **Security fatigue and habituation**
   Users may become tired of repeated warnings and start ignoring them.

5. **Lack of realistic experiments**
   Many studies test users in artificial lab settings, where security is the main task. Real phishing happens while users are focused on something else.

6. **Need for tailored interventions**
   Different users, organizations and contexts may require different types of support.

7. **Need to reduce user effort**
   Future interventions should protect users without overloading them. 

## Relevance for your project

This paper is very relevant for **“Modern Phishing vs. Security Filters”** because it adds the **human side** of phishing defense.

You can use it to argue that:

* technical filters are important, but they will not catch everything;
* users remain part of the defense chain;
* awareness training alone is not enough;
* warnings must be clear, concrete and well placed;
* passive indicators are often ignored;
* overly intrusive warnings can cause frustration;
* phishing defense should combine filters, warnings, interface design and user training;
* future systems should reduce user burden instead of expecting users to act like security experts.

## Final takeaway

The main conclusion is that user-oriented phishing interventions are necessary, but current approaches are fragmented and imperfect.

The strongest idea for your article is:

> Modern phishing defense cannot rely only on technical filters or only on user education. Effective protection requires a combination of automated detection, usable warnings, interface design, realistic training and low-friction interventions that help users make safer decisions without overloading them.

This paper helps you explain why the “human factor” should not simply be treated as the weakest link, but as part of a socio-technical system that needs better support.
