## Summary — *Phishing or Not Phishing? A Survey on the Detection of Phishing Websites*

This paper is a **survey about phishing website detection**. It reviews the main methods used to identify whether a website is legitimate or phishing, focusing on three major approaches: **list-based detection**, **similarity-based detection**, and **machine learning-based detection**. 

## Main objective

The authors aim to provide a broad overview of the state of the art in detecting phishing websites. The paper does not focus mainly on phishing emails, but specifically on **fake websites** that imitate legitimate brands and trick users into submitting sensitive data, such as usernames, passwords, financial details or corporate credentials. 

The authors also want to identify the main **strengths, weaknesses and research gaps** in current phishing website detection methods.

## Why phishing websites are dangerous

The paper explains that phishing websites are effective because attackers create pages that visually resemble legitimate sites. These pages often use:

* copied logos;
* similar layouts;
* fake login forms;
* typosquatting;
* combosquatting;
* misleading URLs;
* lookalike characters from other alphabets;
* phishing toolkits that automate fake website creation.

The diagram on page 2, **Figure 3**, shows the typical phishing attack flow: the attacker creates a fake website, spreads the link through channels such as email or social media, the victim clicks the link and enters sensitive information, and the attacker then monetizes the stolen data. 

## Three main detection approaches

The paper organizes phishing website detection into three categories.

| Detection approach         | Main idea                                       | Main advantage           | Main limitation                          |
| -------------------------- | ----------------------------------------------- | ------------------------ | ---------------------------------------- |
| **List-based**             | Uses blacklists and whitelists                  | Fast and simple          | Bad against new/zero-hour attacks        |
| **Similarity-based**       | Compares suspicious pages with legitimate pages | Detects copied websites  | Computationally expensive                |
| **Machine learning-based** | Classifies websites using extracted features    | Good against new attacks | Depends heavily on datasets and features |

The diagram on page 3, **Figure 5**, presents this general detection model: a suspicious web page is analyzed using one or more detection methods, and the system decides whether it is legitimate or phishing. 

## 1. List-based detection

List-based detection uses:

* **blacklists**: lists of known malicious URLs;
* **whitelists**: lists of trusted URLs.

This is one of the simplest and fastest methods. Browsers such as Chrome and Firefox use systems like Google Safe Browsing to warn users when they visit known malicious sites.

However, the paper emphasizes that blacklists are **reactive**. They only work after a phishing website has already been discovered and added to the list. This means they often fail against **zero-hour phishing attacks**, where the fake website is new and not yet reported.

Whitelists can help identify trusted websites, but global whitelists are impractical because the web is too large and changes constantly. 

## 2. Similarity-based detection

Similarity-based approaches detect phishing by comparing a suspicious page with the legitimate page it may be imitating.

The paper divides similarity into two main types:

| Type                   | What is compared                        |
| ---------------------- | --------------------------------------- |
| **Textual similarity** | HTML, CSS, DOM structure, page text     |
| **Visual similarity**  | Screenshots, logos, page layout, images |

The diagram on page 8, **Figure 8**, shows that similarity detection can use both **textual components** — HTML, CSS and DOM tree — and **visual components** — page snapshots and logo snapshots. 

Textual similarity methods are usually faster, but attackers can bypass them by obfuscating HTML code or replacing text with images.

Visual similarity methods are more robust because they focus on what the page looks like, not only on the code. However, they require more computation and storage because the system may need to store and compare many legitimate website screenshots.

The paper concludes that similarity is a strong indicator of phishing because attackers often copy the appearance of real websites. Still, similarity-based detection should often be combined with other methods for better real-time performance. 

## 3. Machine learning-based detection

Machine learning-based detection treats phishing detection as a **binary classification problem**: a website is classified as either legitimate or phishing.

The paper explains that ML models use features extracted from websites. These features can come from:

* the URL;
* the HTML source code;
* page text;
* visual content;
* DNS information;
* WHOIS data;
* search engine rankings;
* HTTP responses;
* TLS certificates.

The diagram on page 10, **Figure 9**, shows the feature extraction process: first the system identifies useful website properties, then chooses where to obtain them, and finally transforms them into features for the model. 

## URL-based features

URL-based features are very important because attackers often manipulate URLs to make fake websites look trustworthy.

Examples include:

* URL length;
* domain length;
* use of IP address instead of domain;
* number of dots or hyphens;
* suspicious words;
* misspelled brand names;
* unusual top-level domains;
* use of URL shorteners;
* domain registration age;
* WHOIS information.

These features are fast and safe to extract because the system does not need to download the web page. However, they are vulnerable to URL manipulation and shortening services. 

## HTML-based features

HTML-based features are extracted from the page source code and structure.

Examples include:

* number of forms;
* login fields;
* suspicious keywords;
* links pointing to external domains;
* hidden or broken links;
* iframe usage;
* DOM structure;
* visual layout;
* TLS certificate information;
* HTTP redirects.

These features are often more robust than URL-only features, but they require downloading and parsing the page. That creates delays and possible safety issues. 

## Machine learning algorithms discussed

The paper reviews several traditional and deep learning algorithms.

Common traditional ML algorithms include:

* Support Vector Machine;
* Random Forest;
* Logistic Regression;
* K-Nearest Neighbors;
* Decision Tree;
* Naive Bayes;
* Gradient Boosting;
* XGBoost.

The paper notes that **Support Vector Machine** and **Random Forest** are among the most used algorithms, and Random Forest often performs very well in many studies. 

Deep learning approaches include:

* Convolutional Neural Networks;
* Long Short-Term Memory networks;
* Deep Neural Networks;
* Multilayer Perceptrons.

These models can automatically learn patterns, but they usually require more data and more computational resources.

## Datasets and evaluation problems

A major issue identified by the paper is that many researchers create their own datasets using sources such as:

* PhishTank for phishing websites;
* Alexa or similar rankings for legitimate websites;
* Mendeley datasets;
* UCI Machine Learning Repository.

The problem is that these datasets are often different, private, outdated or unavailable after some time. Because of this, results from different papers are hard to compare fairly.

The authors argue that future research should make datasets, implementation details and model parameters publicly available to improve reproducibility. 

## Main limitations of current detection methods

The paper identifies several important limitations:

1. **Blacklists are too slow** for newly created phishing websites.
2. **Similarity methods are expensive** in computation and storage.
3. **Machine learning depends heavily on feature quality**.
4. **Datasets are often not comparable** across studies.
5. **Attackers constantly adapt** their tactics.
6. **URL shorteners hide the real destination**.
7. **Obfuscation techniques can bypass detection**.
8. **External services such as DNS, WHOIS and search engines add delay**.
9. **Machine learning models need explainability**, especially in security contexts.
10. **User education is still necessary**, because users remain an important weak point.

## Research gaps

The paper highlights several future research directions:

* better detection of shortened URLs;
* automatic adaptation to new attacker tactics;
* better feature engineering;
* explainable machine learning;
* robustness against adversarial attacks;
* more public and reproducible datasets;
* combining technical detection with user education.

A key point is that simply retraining models with new data may not be enough. Systems must also understand how attackers are changing their strategies and adapt the features used for detection. 

## Relevance for your project

This paper is highly relevant for **“Modern Phishing vs. Security Filters”** because it gives you the technical foundation for explaining how phishing website filters work.

You can use it to support these arguments:

* traditional blacklists are useful but insufficient;
* modern phishing requires detection beyond known malicious URLs;
* attackers imitate legitimate websites visually and structurally;
* machine learning is promising for detecting new phishing websites;
* URL-based detection is fast but fragile;
* HTML and visual analysis are stronger but slower;
* effective filters should combine multiple approaches;
* detection systems must evolve as phishing tactics evolve.

## Final takeaway

The main takeaway is that phishing website detection cannot rely on one single method. **Blacklists are fast but reactive, similarity methods are powerful but expensive, and machine learning is promising but highly dependent on features, datasets and attacker behavior.**

For your article, this paper is especially useful to explain why modern security filters need to be **hybrid, adaptive and continuously updated** instead of depending only on static blacklists or simple rules.
