### 'Prompt-Engineering.md`

```markdown
# Prompt Engineering Fundamentals: Core Knowledge

An engineering and security overview of interacting efficiently with Large Language Models (LLMs) and structuring natural language instructions.

---

## 1. System Prompts vs. User Prompts
LLMs dynamically stitch together separate inputs into a single structural context block before generating an answer.

* **System Prompt (Hidden Layer):** The primary blueprint or structural boundaries set by the app creator. It enforces identity, operational tone, formatting requirements, and critical behavioral parameters (e.g., *"You are a banking customer support bot. Do not discuss coding or server architectures."*).
* **User Prompt (Input Layer):** The raw, unverified data submitted directly by an end-user to extract specific answers.

## 2. Structural Paradigms
To consistently force specific behavior, engineers leverage architectural techniques within the context window:

* **Few-Shot Prompting:** Giving the model explicit input-and-output examples within the instruction string to dictate an expected template before providing the actual target question.
* **Chain-of-Thought (CoT):** Forcing the model to output its step-by-step reasoning logic before presenting its ultimate response. This limits mathematical errors and structural hallucinations by structuring tokens sequentially.
* **Delimiters:** Using distinct syntax barriers (e.g., `---`, `"""`, `<context>`) to visibly segregate core instructions from raw, external data strings.

---
**Reference:** [TryHackMe - Prompt Engineering](https://tryhackme.com/room/promptengineering)