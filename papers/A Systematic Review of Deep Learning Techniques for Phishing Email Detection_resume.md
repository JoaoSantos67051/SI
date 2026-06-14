## Summary — *A Systematic Review of Deep Learning Techniques for Phishing Email Detection*

The paper reviews how **deep learning techniques are being used to detect phishing emails**, especially because traditional methods like blacklists, whitelists, signatures and rule-based filters are no longer enough against modern phishing, spear-phishing and zero-day attacks. Attackers increasingly use realistic messages, trusted email services, malicious URLs and attachments to bypass traditional spam filters. 

## Main objective

The authors wanted to understand:

1. which **deep learning models** are being used for phishing email detection;
2. how effective they are compared with traditional machine learning;
3. which datasets and evaluation metrics are used;
4. what limitations still exist in current research. 

## Methodology

The paper is a **Systematic Literature Review (SLR)** following the **PRISMA** methodology. The authors searched papers from **IEEE Xplore, ScienceDirect and ACM Digital Library**, focusing on studies from **2019 to 2024**.

They initially found **443 records**, filtered them through inclusion/exclusion criteria, and selected **33 papers** for detailed analysis. The PRISMA flow diagram on page 3 shows this filtering process. 

## Why deep learning is relevant for phishing detection

The paper explains that deep learning can automatically learn patterns from email data, while traditional machine learning often depends on manual feature extraction. Models such as **CNN, RNN, LSTM, Bi-LSTM, BERT and other transformer-based models** are useful because they can process email text, structure and context.

The authors highlight that deep learning models often achieve very high accuracy, frequently above **95%**, and in some studies above **99%**. However, these results are not always directly comparable because the studies use different datasets, features and evaluation methods. 

## Main types of features used

The reviewed studies classify phishing emails using different parts of the email:

| Feature type        | What it means                                             |
| ------------------- | --------------------------------------------------------- |
| **Email body**      | The main text of the email                                |
| **Header**          | Metadata such as sender, receiver and routing information |
| **Subject**         | Email subject line                                        |
| **URL**             | Links included in the email                               |
| **Attachments**     | Files attached to the email                               |
| **Email structure** | HTML structure, number of links, domains, layout, etc.    |

The paper notes that many studies focus mainly on the **email body**, but this is a limitation because modern phishing may hide malicious content in links, attachments, QR codes or HTML structures. Table 1 on page 6 organizes the reviewed studies by feature type and model used. 

## Deep learning models discussed

The paper covers several models:

* **CNN**: useful for extracting local text or structural patterns.
* **RNN/LSTM/Bi-LSTM**: useful for sequential text analysis.
* **BERT and transformer-based models**: strong for understanding language context.
* **Hybrid and ensemble models**: combine several models to analyze different parts of the email.
* **LLMs**: newer approaches using large language models for phishing classification.

One important finding is that **hybrid and modular architectures** are especially promising because they can analyze multiple email components, such as body, header, URL and attachments, instead of relying on only one source of information. 

## Main results

Many of the reviewed studies achieved strong results. For example:

* some LSTM, CNN and BERT-based approaches achieved around **97–99% accuracy**;
* ensemble models also performed very well;
* systems that analyze more than just the email body tend to be more complete;
* some traditional ML models still performed competitively, but they may struggle with unseen or evolving phishing patterns. 

However, the authors are careful to say that accuracy values cannot always be compared fairly, because studies use different datasets, different metrics and different experimental conditions.

## Key limitations found

The paper identifies several major problems in current phishing email detection research.

### 1. Dataset limitations

Deep learning needs large, diverse and high-quality datasets. However, phishing email datasets are often small, private, outdated or unbalanced. This can cause models to overfit and perform badly in real-world environments. 

### 2. Lack of generalization

Many models perform well on the dataset they were trained on, but the paper argues that they should be tested across different datasets and domains to prove real robustness. 

### 3. Overfocus on email body text

Many studies only analyze the text of the email body. This is not enough for modern phishing, because malicious content can be hidden in URLs, attachments, images, QR codes or obfuscated links. 

### 4. Computational cost

Advanced models such as BERT, ensemble architectures and modular deep learning systems can require high computational resources, making them harder to deploy in real production environments. 

### 5. Difficulty adapting to new attacks

The authors identify adaptability as a major research gap. Phishing changes quickly, so detection systems need to adapt to new attack patterns instead of relying only on old training data. 

## Future research directions

The paper suggests that future phishing detection systems should:

* use more recent and diverse datasets;
* test models across different domains;
* analyze all email components, not only the body;
* include URL obfuscation detection;
* expand shortened URLs during preprocessing;
* decode QR codes;
* improve detection of malicious attachments;
* explore deep online learning and deep reinforcement learning;
* balance detection power with deployment efficiency. 

## Relevance for your project

This paper is very useful for your topic **“Modern Phishing vs. Security Filters”** because it shows that modern phishing is difficult to stop with traditional filters alone. It gives you strong arguments to say that security filters are evolving from simple rule-based systems to AI-based and deep learning-based detection systems.

For your practical part, this paper also supports the idea of creating a simple phishing detection tool that analyzes:

* email text;
* suspicious words;
* URLs;
* shortened links;
* attachment indicators;
* urgency or persuasion cues;
* mismatch between sender and content.

## Critical conclusion

The main conclusion is that **deep learning improves phishing email detection**, but it is not a perfect solution. The biggest challenge is not only achieving high accuracy in experiments, but building systems that work with **new, realistic and constantly evolving phishing attacks**.

For your article, this paper can support a key argument:

> Modern phishing cannot be solved only with traditional filters or only with user education. Effective protection requires layered security, combining technical filters, AI-based detection, email authentication, user awareness and continuous adaptation to new attack techniques.
