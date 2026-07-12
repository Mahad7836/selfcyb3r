# AI/ML Security Threats Notes
These notes cover the fundamental concepts of Artificial Intelligence (AI) and Machine Learning (ML), how they are constructed, the specific threats they face, and how they can be used defensively in cybersecurity.

## 1. The Building Blocks of AI
Understanding the core components of AI is essential before analyzing security risks.

Machine Learning (ML): A subset of AI where models are trained to make predictions based on data.

Deep Learning (DL): A specialized method of learning that does not require human-labeled data. It can automatically extract features from raw, unstructured input (like images or text).

Neural Networks: The architecture behind Deep Learning, inspired by the human brain.

Input Layer: The very first layer of a neural network that receives and handles incoming raw data.

Synapses: The weighted connections between nodes (neurons) in the network, meant to simulate the synapses in a biological brain.

Semi-Supervised Learning: A category of machine learning that combines both labelled and unlabelled data during training. This is useful when labeling data is expensive or time-consuming.

## 2. Large Language Models (LLMs)
LLMs are a specific application of Deep Learning that have revolutionized natural language processing.

Large Language Models (LLMs): The type of AI model responsible for major advancements in tools like ChatGPT. They are designed to understand and generate human-like text.

Transformer: The specific neural network architecture introduced by Google in 2017 that powers modern LLMs. It allows models to process data in parallel rather than sequentially.

Pre-training: The initial training stage where an LLM processes massive amounts of text data to learn general language patterns before being fine-tuned for specific tasks.

## 3. AI Security Threats
As AI adoption grows, so does the attack surface. Threats can target the models themselves or use AI to enhance traditional attacks.

### Frameworks
ATLAS: A framework developed by MITRE (Adversarial Threat Landscape for Artificial-Intelligence Systems) to guide the understanding of AI-specific cyber threats and tactics.

## Specific Attacks
### Model Theft: An attack where an adversary clones a proprietary AI model by repeatedly interacting with its API and using the outputs to train a copycat model.

### Data Poisoning: Injecting malicious or misleading data into a model's training set to corrupt its behavior or bias its decisions.

### Prompt Injection: Manipulating the input (prompt) given to an LLM to override its safety guidelines or original instructions.

### Privacy Leakage: When a model inadvertently reveals sensitive information included in its training data (e.g., PII).

## AI-Enhanced Attacks
### Deepfakes: A generative AI technique that can replicate a specific person's voice or appearance with high realism, often used for fraud or disinformation.

### Phishing: AI has made phishing emails significantly harder to detect by generating fluent, context-aware, and convincing messages, removing the grammatical errors typical of older phishing attempts.

## 4. Defensive AI
AI is not just a threat vector; it is a powerful tool for defenders (Blue Teams).

Efficiency: According to IBM, AI helps organizations identify and contain data breaches 108 days faster than those without AI automation.

Threat Hunting: AI aids this proactive cybersecurity task by helping analysts imagine and predict attacker behaviors they might not have otherwise considered.

Model Monitoring: Tools like SHAP and LIME are used for Explainable AI (XAI). They help defenders understand why a model made a specific decision, which is critical for detecting bias or manipulation.


# Summary
AI vs ML vs DL: AI is the broad science; ML is the subset of prediction; DL is the subset using neural networks.
Offensive AI: Attackers use AI to scale attacks (phishing) and target AI systems (poisoning/theft).
Defensive AI: Defenders use AI to automate detection and response, significantly reducing breach lifecycles.