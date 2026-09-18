# TryHackMe: AI Forensics Cheatsheet & Room Notes

This room explores the practical role of **Artificial Intelligence (AI)** and **Machine Learning (ML)** within Digital Forensics and Incident Response (DFIR) [1.1.2, 1.4.5]. It covers AI concepts, limitations, and walks through an incident response simulation at a compromised software company named **RobbCo** [1.3.8].

---

## 📘 Part 1: Core Theoretical Concepts

### 1. Key AI Advantages in DFIR [1.1.8, 1.3.4]
* **Automated Data Processing:** Parallel computation cuts weeks of analysis down to hours [1.1.8].
* **Pattern Recognition:** Models like *Isolation Forests* map normal baselines to surface hidden anomalies without rigid rules [1.3.4, 1.3.8].
* **Alert Prioritization:** AI scores severity dynamically, trimming out alert noise for fatigue-prone analysts [1.3.4, 1.1.8].

### 2. Critical Evaluation Metrics [1.3.1]
* **Accuracy:** Overall rate of correct guesses. Can be deceptive if a dataset is severely imbalanced [1.3.1].
* **Precision:** $\frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}$. Higher precision maps to fewer false alarms [1.3.1].
* **Recall:** $\frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$. Measures how thoroughly the model catches actual threats [1.3.1].

### 3. AI Limitations & Challenges [1.1.5]
* **Non-determinism:** The exact same input can trigger different model outputs across separate runs [1.3.7].
* **Explainability & Legal Bias:** Challenges validating automated choices in court environments [1.1.5].

---

## 🕵️‍♂️ Part 2: Practical Investigation — "The Digital Trail"

### 🧪 Investigation Lab Commands
To activate the machine learning analysis environment and run the classification scripts [1.3.8]:
```bash
# Step 1: Spin up the Python virtual environment
source /opt/dfir-env/bin/activate

# Step 2: Classify anomalous authentications
python3 /opt/dfir-lab/classify_logs.py /var/log/auth.log

# Step 3: Run the entropy/file structure anomaly scanner
python3 /opt/dfir-lab/file_anomalies.py
```

### 🎯 Case Summary & Flag Reference Table

| Question / Artifact Objective | Investigation Source / Artifact [1.4.1, 1.4.6] | Value / Flag [1.4.2] |
| :--- | :--- | :--- |
| **Initial Access Timestamp** | `auth.log` analysis (`classify_logs.py`) [1.3.8] | **`03:01:02`** [1.4.2] |
| **Initial Attack Method** | Vector targeting user `j.morgan` [1.3.8] | **`Phishing`** [1.4.2] |
| **Attacker Email Address** | Found within `/tmp/invoice_dump.txt` [1.4.1] | **`akeane@poseidonenergy.net`** [1.4.2] |
| **Privilege Escalation Command** | Checked inside `/home/j.morgan/.bash_history` [1.4.6] | **`sudo nano /home/r.house/.ssh/authorized_keys`** [1.4.2] |
| **Stolen Code Archive Path** | Staged payload identified by high entropy [1.3.6] | **`/dev/shm/.core_dump_2025.tgz.enc`** [1.4.2] |

---

## 🧠 Key Takeaways
1. **AI is a Spotlight, Not a Verdict:** The scripts highlight suspicious points, but human intuition connects the dots via context clues like `.bash_history` [1.3.6].
2. **Living off the Land:** The attacker escalated privileges silently using valid `sudo` adjustments to SSH configs instead of explosive exploits [1.3.6].