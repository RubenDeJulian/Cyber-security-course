# h1 CyberScience

Course: Cyber Security (ICB705AS3YE-2)  
Author: Ruben De Julian  
Date: 26 October 2026  

---

## a) Science Hunt: Selection Process and Chosen Article

To locate a peer-reviewed academic review article related to the course topics, I applied the criteria outlined by Karvinen (2025):

1. **Search queries**: In Google Scholar, I used title-constrained searches:
   - `intitle:review "threat modeling"`
   - `intitle:review "MITRE ATT&CK"`
2. **Filters**:
   - Timeframe: 2024 to 2026 to ensure current findings.
   - Document type: Review article / comprehensive survey.
3. **Publication venue verification**: I confirmed the journal's classification in the Finnish Publication Forum (JUFO portal). The selected journal, *ACM Computing Surveys* (CSUR), holds a JUFO Level 3 rating.
4. **Selected article details**:
   - **Authors**: Bader Al-Sada and Alireza Sadighian
   - **Year**: 2024
   - **Title**: *MITRE ATT&CK: State of the Art and Way Forward*
   - **Journal**: ACM Computing Surveys, 57, 1, article 12, pp. 1–37.
   - **DOI**: https://doi.org/10.1145/3687300

---

## b) Review the Review: Article Summary

Al-Sada and Sadighian (2024, 1–37) review the academic literature surrounding the MITRE ATT&CK knowledge base across threat modeling, threat intelligence, and defensive evaluations.

* **Key areas being researched**:
  * Mapping audit logs, network flows, and telemetry to adversary techniques instead of relying on static indicators (Al-Sada & Sadighian 2024, 6–10).
  * Integrating ATT&CK with established threat modeling approaches, such as STRIDE, to evaluate coverage gaps (Al-Sada & Sadighian 2024, 4–5, 12).
  * Automated extraction of techniques from unstructured threat intelligence reports using natural language processing (Al-Sada & Sadighian 2024, 14–17).
  * Extending the taxonomy to cover cloud environments, container ecosystems, and industrial control systems (Al-Sada & Sadighian 2024, 3–4).

* **Widely agreed points**:
  * Focusing on adversary tactics, techniques, and procedures (TTPs) provides more durable defense value than blocking transient indicators such as IP addresses or file hashes (Al-Sada & Sadighian 2024, 2–3).
  * Traditional linear kill chains do not capture the non-linear, multi-stage nature of enterprise intrusions; matrix-style structures provide a more accurate representation (Al-Sada & Sadighian 2024, 4).
  * Threat modeling based on observed adversary behaviors helps security teams allocate limited defensive resources effectively (Al-Sada & Sadighian 2024, 2).

* **Open questions and challenges**:
  * ATT&CK catalogs individual actions but does not explicitly represent the chronological order or dependencies between steps (Al-Sada & Sadighian 2024, 31–33).
  * Distinguishing between benign administrative activity and adversarial technique execution remains difficult and generates significant false positives in practice (Al-Sada & Sadighian 2024, 32).
  * Definitions require ongoing maintenance to address newer attack surfaces, such as microservice environments and automated attack tools (Al-Sada & Sadighian 2024, 33–34).

---

## c) Threat Modeling Quickrun

### 1. Company and Assets
* **Company**: TicketGO OÜ (primary ticketing and event access management platform).
* **Crown jewels**:
  * User credentials and tokenized payment records.
  * Availability and latency of the ticket reservation API during high-demand on-sale events.
  * Integrity of digital ticket validation tokens (preventing duplication or unauthorized generation).

### 2. Bad Guys: Capability, Opportunity, Intent (COI)
* **Ticket scalpers / bot operators**:
  * *Capability*: High technical capability using headless browsers, distributed residential proxy pools, and custom reservation scripts.
  * *Opportunity*: Publicly exposed checkout and ticket reservation endpoints that must process requests rapidly.
  * *Intent*: Hold and acquire high-demand ticket inventory in bulk to resell on secondary markets for profit.
* **Extortion actors / opportunistic attackers**:
  * *Capability*: Moderate capability scanning for exposed API keys, misconfigured cloud storage, or outdated container dependencies.
  * *Opportunity*: Complex cloud deployments with multiple administrative access points.
  * *Intent*: Encrypt or exfiltrate customer databases to demand ransom payments.

### 3. Risk Identification and Valuation

Annual loss expectancy is estimated using the formula:

$$\text{Estimated Annual Cost} = \text{Annual Likelihood} \times \text{Financial Impact per Occurrence}$$

1. **Risk 1: Inventory denial of service via automated reservation abuse**
   * Description: Automated scripts exhaust available cart reservations for major events without completing purchases, blocking legitimate users.
   * Likelihood: 60% per year (0.60).
   * Impact: €40,000 (direct loss of transaction revenue, customer support overhead, and promoter penalties).
   * Estimated annual value: $0.60 \times €40,000 = \text{€24,000 / year}$.

2. **Risk 2: Production database compromise via leaked cloud secret**
   * Description: A hardcoded cloud service credential or database token committed to code is identified and used to exfiltrate and corrupt customer records.
   * Likelihood: 10% per year (0.10).
   * Impact: €350,000 (regulatory compliance notifications under GDPR, forensic investigation, system restoration, and customer loss).
   * Estimated annual value: $0.10 \times €350,000 = \text{€35,000 / year}$.

### 4. Decision on the Highest-Value Risk (META Framework)
* **Selected risk**: Risk 2 (Production database compromise, €35,000 / year).
* **Action chosen**: **Mitigate**.
* **Implemented controls**:
  * Replace long-lived cloud credentials in deployment pipelines with short-lived OpenID Connect (OIDC) tokens.
  * Enforce pre-commit git hooks and repository scanning to block secrets from being pushed.
  * Restrict database network access strictly to internal subnets and require hardware-backed multi-factor authentication (MFA) for administrative access.

---

## Sources

Al-Sada, B. & Sadighian, A. 2024. MITRE ATT&CK: State of the Art and Way Forward. ACM Computing Surveys, 57, 1, article 12, pp. 1–37. https://doi.org/10.1145/3687300.

Karvinen, T. 2025. Start Your Research with a Review Article. URL: https://terokarvinen.com/review-article/. Accessed: 26 October 2026.

Karvinen, T. 2026. Cyber Security - 2026 late autumn. URL: https://terokarvinen.com/. Accessed: 26 October 2026.

---

### AI Disclosure Note
Generative AI (Gemini 3.8 Flash via ChatLLM Teams) was consulted to assist with initial literature discovery queries and formatting the bibliography according to institutional standards. The summary synthesis, threat scenario parameters, and quantitative evaluations were defined and verified directly by the author.
