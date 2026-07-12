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
```bash
nmap -p 5000,6333,6334,8000,8001,8002,8888 -sV <Target_IP_or_Subnet>