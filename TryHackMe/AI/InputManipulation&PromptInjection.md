# Input Manipulation & Prompt Injection: Core Knowledge

An analysis of trust boundaries inside Large Language Model applications, specifically focusing on prompt exploitation vectors and system subversion.

---

## 1. The Core Architectural Flaw
The primary systemic weakness of LLM integration is the lack of separation between code (instructions) and data (user input). 

```text
[Hidden System Rules] + [Untrusted User Input] ➔ Processed with EQUAL Authority by the Model