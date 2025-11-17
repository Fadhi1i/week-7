# Designing Responsible and Fair AI Systems

**Assignment:** AI Ethics
**Author:** FADHILI ANICETUS

---

## Part 1: Theoretical Understanding

### 1. Short Answer Questions

**Q1: Define algorithmic bias and provide two examples.**

- **Definition:** Algorithmic bias describes systematic and repeatable errors in an AI system that result in unfair outcomes, privileging one group of people over another. It often arises from biased training data that reflects historical inequalities or from flawed model design.
- **Example 1 (Recruiting):** An AI hiring tool trained on 10 years of resumes from a male-dominated tech company "learns" that male candidates are preferable, and penalizes resumes that include words like "women's" (e.g., "women's chess club captain").
- **Example 2 (Criminal Justice):** A risk assessment tool used for bail hearings (like COMPAS) is trained on data with historical racial disparities in arrests. The AI learns to associate certain proxies (like zip codes) with a higher risk, resulting in minority defendants being incorrectly flagged as high-risk more often than white defendants.

**Q2: Explain the difference between transparency and explainability.**

- **Transparency** is about the _system_. It means being open about how a model was built, what data was used, and where it is deployed. It's like a food label listing all the ingredients.
- **Explainability** (or XAI) is about a _specific decision_. It is the ability to explain _why_ a model made a particular prediction (e.g., "Why was this person's loan denied?"). It's like the chef explaining _how_ the ingredients were combined to make the dish taste a certain way.

Both are important because transparency builds public trust, while explainability provides the mechanism for accountability and allows users to challenge a specific, unfair outcome.

**Q3: How does GDPR impact AI development in the EU?**
GDPR (General Data Protection Regulation) heavily impacts AI by enforcing a "data protection by design" approach.

1.  **Data Minimization:** It restricts developers from collecting more data than is "strictly necessary" for the AI's stated purpose.
2.  **Lawful Basis for Processing:** AI systems cannot just "scrape" data. They must have explicit user consent or another legal basis to process personal data.
3.  **Right to Explanation:** Under Article 22, EU citizens have a right to "meaningful information about the logic involved" in automated decisions, which pushes companies to invest in explainability.

### 2. Ethical Principles Matching

- **A) Justice:** Fair distribution of AI benefits and risks.
- **B) Non-maleficence:** Ensuring AI does not harm individuals or society.
- **C) Autonomy:** Respecting users’ right to control their data and decisions.
- **D) Sustainability:** Designing AI to be environmentally friendly.

_(The correct matches are B, C, D, A)_

---

## Part 2: Case Study Analysis

### Case 1: Biased Hiring Tool (Amazon)

- **Source of Bias:** The primary source was **biased training data**. The model was trained on Amazon's own resume data from the previous 10 years. Because the tech industry (and Amazon) was male-dominated, the AI learned to associate male-typical language with success and penalized resumes containing "women's" or all-women's college names.
- **Three Fixes:**
  1.  **Data-Level (Pre-processing):** Do not use historical resumes as-is. Instead, augment the dataset with under-represented groups (e.g., using "Reweighing" techniques in AIF360) to ensure a balanced number of successful male and female examples.
  2.  **Model-Level (In-processing):** Implement an "Adversarial Debiasing" model. This involves training a second model that tries to predict the "gender" from the first model's decision. The main model is then penalized if the second model is successful, forcing it to learn patterns that are not proxies for gender.
  3.  **Feature-Level:** Explicitly remove all gender-specific pronouns and proxy variables (like "women's chess club") from the data _before_ training.
- **Fairness Metrics:**
  1.  **Disparate Impact Ratio:** Measures the selection rate of women vs. men. A fair model should have a ratio close to 1.0 (e.g., if 10% of men are selected, at least 8% of women should be, for a ratio of 0.8).
  2.  **Equal Opportunity Difference:** Checks that the "True Positive Rate" is the same for all groups. (i.e., "Of all the _qualified_ women, what percentage did the AI select?" vs. "Of all the _qualified_ men, what percentage did the AI select?").

### Case 2: Facial Recognition in Policing

- **Ethical Risks:**
  1.  **Wrongful Arrests:** Studies (e.g., by NIST) have repeatedly shown that facial recognition systems have much higher false positive rates for minorities, particularly Black and Asian individuals. This directly leads to misidentification and wrongful arrests.
  2.  **Mass Surveillance & "Chilling Effect":** Deploying facial recognition on public cameras creates a system of mass surveillance, violating the right to privacy and anonymity. This can create a "chilling effect" where people are afraid to attend protests or visit sensitive locations (like a mental health clinic).
  3.  **Lack of Due Process:** A person "flagged" by an AI has no way to challenge the algorithm, effectively being treated as guilty-by-machine.
- **Policies for Responsible Deployment:**
  1.  **Human-in-the-Loop (Mandatory):** An AI match must **never** be the sole basis for an arrest. It can only be used as a "tip" that a trained human officer must then independently verify _before_ taking action.
  2.  **Ban on Mass Surveillance:** Public-facing, real-time facial recognition should be banned. Its use should be restricted to "post-event" investigations with a court-ordered warrant (e.g., "scan this video from the bank robbery").
  3.  **Independent Audits:** Before any police department can purchase a system, it must be certified by an independent, third-party auditor to test its accuracy and bias across all demographic groups.

---

## Part 4: Ethical Reflection

**Project:**

I will ensure my project adheres to ethical AI principles by focusing on three key areas. First, for **Justice and Fairness**, the crop yield model must not be biased against small-scale farmers who may have "noisier" or less-complete data. I will address this by testing the model's accuracy on different farm sizes. Second, for **Privacy and Data Governance**, farmers own their data. I will ensure all data is anonymized and that the farmer's consent is required before their data is used to retrain the global model. Third, for **Transparency**, I will not just provide a yield "prediction" but also an "explanation" (e.g., "Yield is low due to poor Nitrogen levels"), so the farmer can take a concrete, actionable step.

---

## Bonus Task: 1-Page Policy Proposal

### Guideline: Ethical AI Use in Healthcare

**Preamble:** This guideline ensures that all AI systems used at [Healthcare Institution] are safe, fair, and trustworthy, augmenting the capabilities of our clinical staff and improving patient outcomes.

**1. Patient Consent & Autonomy**

- **Explicit Consent:** Patients must be explicitly informed if an AI system is being used in their diagnosis or treatment. This information must be in plain, non-technical language.
- **"Right to Opt-Out":** Patients have the right to refuse an AI-assisted diagnosis or treatment (where feasible) in favor of a traditional-only workflow, without penalty to their quality of care.
- **Data Use:** Patient consent must be separate for 1) clinical care and 2) use in AI training. Data used for AI training must be de-identified and anonymized.

**2. Bias Mitigation & Fairness**

- **Mandatory Audits:** No AI system may be deployed until it has passed a "Fairness Audit" on a dataset representative of our diverse patient population (including different ethnicities, genders, and ages).
- **Key Metric (Equal Opportunity):** The "True Positive Rate" must be equal across all demographic groups. An AI tool for detecting skin cancer must be equally effective on all skin tones.
- **Data Sourcing:** All training data must be sourced from multiple, diverse hospitals to avoid regional or demographic bias.

**3. Transparency & Accountability**

- **Clinical Oversight (Human-in-the-Loop):** An AI recommendation is **never** a final decision. It is a "second opinion" or "triage tool" for a qualified human clinician who holds final responsibility.
- **Explainability (XAI):** Any system providing a recommendation (e.g., "high risk of sepsis") must also provide the _key factors_ it used to make that decision (e.g., "because of high lactate and abnormal white blood cell count").
- **Accountability:** A clinical review board will be responsible for auditing all deployed AI systems annually and will serve as the point of contact for any patient or clinician challenging an AI-driven outcome.
