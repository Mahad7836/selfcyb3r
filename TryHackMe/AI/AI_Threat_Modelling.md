# 🤖 TryHackMe: AI Threat Modelling

## 📌 Overview
This room covers the fundamentals of threat modelling applied specifically to Artificial Intelligence (AI) and Machine Learning (ML) systems. It bridges the gap between traditional security frameworks and the unique vulnerabilities introduced by AI.

## 🎯 Prerequisites
- Basic understanding of traditional Threat Modelling concepts (e.g., STRIDE).
- Knowledge of Web Application Security and Security Principles.
- Foundational understanding of AI/ML concepts.

---

## 🧠 Unique Characteristics of AI Models
Traditional software follows explicit rules (deterministic). AI models, particularly Large Language Models (LLMs) and Deep Neural Networks, present new challenges:

1. **Non-deterministic Behaviour:** AI models can produce completely different outputs for the exact same input, making testing, auditing, and incident reproduction extremely difficult.
2. **The "Black Box" Problem:** Deep neural networks lack the explainability of traditional application logic. You cannot step through a model's reasoning line-by-line. Defenders must focus on input-output behaviour and failure modes rather than code-level inspection.

---

## 🏭 The AI Model Lifecycle
To model threats, you must understand how an AI model goes from raw data to a production environment:

1. **Data Collection:** Gathering the raw information.
2. **Cleaning and Labelling:** Preparing the data for the model.
3. **Model Training:** The compute-intensive process where the model "learns".
4. **Validation and Packaging:** Testing the model against holdout data.
5. **Inference:** Deploying the model into production to make live predictions/generations.

---

## 📦 Key AI Assets & Their Impact
Traditional applications protect databases and source code. AI introduces an entirely new set of assets that require protection:

| Asset | What It Is | Why It Matters (Impact of Compromise) |
| :--- | :--- | :--- |
| **Training Data** | The datasets used to teach the model its behaviour. | Poisoning this data corrupts the model's outputs at the source. The damage is baked into the model itself. |
| **Model Weights / Parameters** | The numerical values that define what the model has actually learned. | These *are* the model. Stealing them means an attacker has a functional copy of your AI, stealing months of compute and heavy investment. |
| **Embedding Vectors** | Numerical representations of text/data used for retrieval (e.g., in RAG pipelines). | Poisoning or manipulating embeddings alters what information models see at query time, skewing the final output. |
| **System Prompts** | Invisible instructions that define the model's behaviour, constraints, and persona. | Leaking these reveals security controls, business logic, and guardrails, giving attackers a roadmap to bypass them. |
| **Feature Stores** | Preprocessed data repositories that feed real-time model inputs. | Tampering with features changes what the model "sees" at inference time, without touching the model itself. |
| **Model Registry / Artifacts** | Stored versions of trained models ready for deployment. | A compromised registry allows attackers to swap a legitimate model for a backdoored one seamlessly. |

---

## 🛡️ STRIDE Applied to AI

STRIDE is a traditional threat modelling framework, but AI blurs the lines between these categories. 

| Threat Category | Property Violated | Traditional Meaning | AI Context |
| :--- | :--- | :--- | :--- |
| **S** - Spoofing | Authenticity | Pretending to be someone/something else | Spoofing inputs to trick a model's classification. |
| **T** - Tampering | Integrity | Modifying data or code | *Training Data Poisoning* (diffuse, delayed, invisible damage) or modifying feature stores. |
| **R** - Repudiation | Non-repudiability | Denying an action occurred | Lack of logging for specific AI inferences or generated outputs. |
| **I** - Information Disclosure | Confidentiality | Exposing sensitive data | Prompt leaking, model inversion, or extracting training data from the model. |
| **D** - Denial of Service | Availability | Making a system unavailable | Resource exhaustion via complex prompts (Sponge Attacks). |
| **E** - Elevation of Privilege | Authorisation | Gaining unpermitted access | Bypassing LLM guardrails (Jailbreaking) to execute restricted commands. |

> **Note on STRIDE in AI:** Adversarial manipulation of model behaviour doesn't fit neatly into one category. Crafting inputs to make a model hallucinate or bypass safety guardrails is often a mix of Tampering, Spoofing, and Elevation of Privilege.

---

## 📚 Further Reading & Resources
- **MITRE ATLAS:** The ATT&CK framework adapted for Artificial Intelligence systems.
- **OWASP AI Exchange:** Broad AI security guidance covering agentic AI, LLMs, and non-LLM systems.
- **OWASP Top 10 for LLM Applications:** Crucial reading for securing Generative AI deployments.

---
*Notes compiled from the TryHackMe AI Threat Modelling room.*