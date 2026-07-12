# AI System Reconnaissance: Core Knowledge

A technical overview of discovering and mapping AI infrastructure, identifying machine learning frameworks, and fingerprinting exposed AI/ML application interfaces (APIs).

---

## 1. The AI Infrastructure Stack
A production AI environment is not a singular server. It relies on unique service ecosystems that introduce unfamiliar ports and endpoints into an enterprise network:

* **Model Serving Endpoints:** Deliver predictions/inferences to external applications.
* **Vector Databases:** Store high-dimensional mathematical representations (embeddings) of sensitive documents, images, or files.
* **Training/Tracking Servers:** Track model history, hyper-parameters, and artifact builds.

## 2. Network Discovery (AI Common Ports)
Standard infrastructure scanners like `nmap` must look for specific ports hosting AI components to properly define the attack surface:

| Port | Typical Default Service | Description |
| :--- | :--- | :--- |
| `5000` | MLflow | Open-source platform for managing the ML lifecycle. |
| `6333` / `6334` | Qdrant / Weaviate | Vector search engines and databases. |
| `8000` - `8002` | Triton Inference Server | NVIDIA multi-framework inference hosting. |
| `8888` | Jupyter Notebooks | Interactive development environments (frequently unauthenticated). |

### Scan Strategy Example
nmap -p 5000,6333,6334,8000,8001,8002,8888 -sV <Target_IP_or_Subnet>

### 3. Fingerprinting Frameworks & API Schema

Once a service is exposed, metadata endpoints and error handling disclose the internal frameworks being used:HTTP Header Analysis: Platforms like MLflow or Triton can display distinctive headers (e.g., specific Server fields or custom headers indicating an NVIDIA product stack).Inference Endpoint Probing: Querying base structural routes (e.g., GET /v2/models) often returns structured JSON indicating the name, version, and underlying architecture of active models.Deliberate Error Generation: Submitting a malformed payload to a prediction endpoint (e.g., -d '{"bad": "data"}') forces detailed debugging errors that spill exact fields and framework identities (e.g., TensorFlow vs PyTorch format requirements).gRPC Reflection: If gRPC services run on ports like 8001, enabling reflection allows attackers to use grpcurl to pull down the entire production API schema automatically without credentials.

### 4. Unauthenticated Data and Extrospection

Vector databases hold massive security weight. On unauthenticated instances:Weaviate (GET /v1/meta & /v1/schema): Returns active server versions, system parameters, and exact data class configurations.  The Vectorizer Trap: The schema reveals which text embedding model converts incoming inputs into vectors. Identifying this model enables attackers to reconstruct semantic payloads or target down-stream classification weaknesses.Reference: TryHackMe - AI System Reconnaissance