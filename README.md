# Bayesian Diagnostics: Medical Decisions under Uncertainty
*A mini project exploring how Bayesian reasoning improves medical decision-making under uncertainty — part of my AI Safety & Ethics portfolio.*

## Introduction
Medical diagnostics are one of the clearest examples of how **statistical uncertainty shapes critical decisions**. No test is perfect: there will always be false positives and false negatives. This means that doctors, patients, and healthcare systems must **update their beliefs as new evidence emerges**, making choices based on probabilities rather than absolute certainty.

This dilemma mirrors what happens in **artificial intelligence**: machine learning models also operate under uncertainty and limited accuracy, requiring decision-makers to understand risks before placing full trust in their outputs. By studying medical diagnostics through Bayesian tools, we can not only see how probabilities shift with new evidence, but also reflect on **governance and accountability** in systems that directly impact human lives.

---

## Key Terms

**Sensitivity**  
The probability that a test correctly identifies a person who actually has the disease.  
- High sensitivity → few false negatives.  
- Example: A COVID-19 test with 95% sensitivity will correctly detect 95 out of 100 infected patients.  

**Specificity**  
The probability that a test correctly identifies a person who does not have the disease.  
- High specificity → few false positives.  
- Example: A mammogram with 90% specificity will correctly reassure 90 out of 100 healthy patients.  

**Prevalence**  
The proportion of people in a population who have the disease at a given time.  
- Strongly affects how useful a test result is.  
- Example: A rare disease (low prevalence) means most positive results could actually be false positives.  

**Prior Odds**  
The probability of disease before the test result, expressed as odds rather than percentages.  
- Derived from prevalence or other prior knowledge.  
- Example: If prevalence is 1 in 100, the prior odds are 1:99.  

**Likelihood Ratio (LR)**  
A measure of how much a test result changes the odds of disease.  
- **Positive LR (LR+)** = Sensitivity ÷ (1 – Specificity) → how much odds increase after a positive test.  
- **Negative LR (LR–)** = (1 – Sensitivity) ÷ Specificity → how much odds decrease after a negative test.  
- Example: An LR+ of 10 means a positive test makes the disease 10 times more likely compared to before testing.  

---

## Case 1: Mammogram for Breast Cancer (women aged 40–49)

- **Prevalence:** ~1% (about 1 in 100 women in this age group has breast cancer).  
- **Sensitivity:** ~85% (the test catches 85% of true cases).  
- **Specificity:** ~90% (10% false positives).  

These numbers are often quoted in teaching examples (the “mammography paradox”), and they make Bayesian reasoning very clear: with such a low prevalence, most positives are still false alarms.

---

## Case 2: Rapid Antigen Test for COVID-19 (high-prevalence outbreak)

- **Prevalence:** ~20% (e.g., in a high-exposure group at peak outbreak).  
- **Sensitivity:** ~80% (rapid tests miss some cases, especially in early infection).  
- **Specificity:** ~98% (few false positives).  

These values are consistent with CDC/WHO reports during the pandemic. The contrast here is interesting: prevalence is high, so even a modest sensitivity still produces useful results, but false negatives become a real risk.

---

## Case 1 — Screening Mammogram: Contingency Table

**Assumptions (illustrative but realistic):**  
Prevalence = 1%, Sensitivity = 85%, Specificity = 90%.  

### Contingency Table (per 1,000 screened)

|                      | **Test +** | **Test –** | **Total** |
|----------------------|-----------:|-----------:|----------:|
| **Disease (1%)**     | **8.5** TP | **1.5** FN | 10        |
| **No disease (99%)** | **99** FP  | **891** TN | 990       |
| **Total**            | 107.5      | 892.5      | 1,000     |

### Key Metrics  

- **PPV (Positive Predictive Value)** = 8.5 / (8.5 + 99) ≈ **7.9%**  
- **NPV (Negative Predictive Value)** = 891 / (891 + 1.5) ≈ **99.8%**  
- **LR+ (Positive Likelihood Ratio)** = Sens / (1 – Spec) = 0.85 / 0.10 = **8.5**  
- **LR– (Negative Likelihood Ratio)** = (1 – Sens) / Spec = 0.15 / 0.90 ≈ **0.167**  
- **Posterior probability after positive test** ≈ **7.9%**  

___

**Interpretation**  
Even with a reasonably accurate test, the very **low prevalence** of breast cancer in this age group means that most positive results are false alarms. This is the classic “mammography paradox.” Bayesian reasoning highlights that the **base rate** is just as important as test accuracy when interpreting medical results.  

From an AI ethics perspective, this shows why **accuracy alone can be misleading** — in both medicine and machine learning, context and prevalence strongly shape decision quality.  
___

## Case 2 — Rapid Antigen Test for COVID-19: Contingency Table

**Assumptions (illustrative but realistic):**  
Prevalence = 20%, Sensitivity = 80%, Specificity = 98%.  

### Contingency Table (per 1,000 tested)

|                      | **Test +** | **Test –** | **Total** |
|----------------------|-----------:|-----------:|----------:|
| **Disease (20%)**    | **160** TP | **40** FN  | 200       |
| **No disease (80%)** | **16** FP  | **784** TN | 800       |
| **Total**            | 176        | 824        | 1,000     |

### Key Metrics

- **PPV (Positive Predictive Value)** = 160 / (160 + 16) ≈ **90.9%**  
- **NPV (Negative Predictive Value)** = 784 / (784 + 40) ≈ **95.1%**  
- **LR+ (Positive Likelihood Ratio)** = 0.80 / 0.02 = **40**  
- **LR– (Negative Likelihood Ratio)** = 0.20 / 0.98 ≈ **0.204**  
- **Posterior probability after positive test** ≈ **90.9%**

___

### Interpretation

With **higher prevalence**, a positive antigen test is highly informative: most positives are true cases (PPV ≈ 91%).  
However, **false negatives** (40 out of 1,000) remain significant and must be managed carefully.  

This example shows how **context changes diagnostic value**: the same test that struggles in low-prevalence settings becomes reliable in high-prevalence ones.  
For AI and governance, the lesson is clear — **outputs cannot be interpreted in isolation**; decision-makers must account for prevalence, uncertainty, and limitations.

___

### Simulations


