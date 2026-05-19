# Host Anomaly Detection Using ML

A machine-learning based Linux host anomaly detection system using `strace` syscall tracing and an `Isolation Forest` model.

This project dynamically analyzes Linux executables, extracts behavioral syscall features, and detects suspicious or malicious activity based on anomaly detection.

---

# Features

* Linux syscall tracing using `strace`
* Automated ELF executable scanning
* Feature extraction from syscall logs
* Isolation Forest anomaly detection model
* Malware / benign classification
* CSV dataset generation
* Evaluation metrics and confusion matrix
* Google Colab compatible workflow

---

# Project Workflow

```text
Linux Executable
       ↓
   strace Logging
       ↓
 Feature Extraction
       ↓
 CSV Dataset
       ↓
 Isolation Forest
       ↓
 Malware Detection
```

---

# Project Structure

```text
Host-Anomaly-Detection-Using-ML/
│
├── anomaly_detection.ipynb      # Main Google Colab notebook
├── iforest_strace.joblib        # Trained ML model
├── malware_features_20.csv      # Feature dataset
├── strace_logs/                 # Generated syscall logs
├── README.md
│
└── samples/                     # ELF binaries / malware samples
```

---

# Technologies Used

* Python 3
* Linux `strace`
* pandas
* scikit-learn
* Isolation Forest
* joblib
* Google Colab

---

# Installation

## Clone Repository

```bash
git clone https://github.com/karuppasamyk1411-collab/Host-Anomaly-Detection-Using-ML.git
cd Host-Anomaly-Detection-Using-ML
```

---

# Install Dependencies

```bash
pip install pandas scikit-learn joblib
```

Install Linux tracing utilities:

```bash
sudo apt update
sudo apt install strace file
```

---

# Running in Google Colab

Open the notebook:

```text
anomaly_detection.ipynb
```

The notebook contains:

1. Package installation
2. Syscall tracing using `strace`
3. Feature extraction
4. Model training
5. Malware scoring
6. Model evaluation

---

# Dataset Features

The model expects the following features:

| Feature         | Description                               |
| --------------- | ----------------------------------------- |
| io_rw           | Read/write syscall activity               |
| io_meta         | File metadata operations                  |
| net_total       | Total network activity                    |
| net_ipv4        | IPv4 socket usage                         |
| net_ipv6        | IPv6 socket usage                         |
| net_unix        | UNIX socket usage                         |
| mem_mgmt        | Memory management calls                   |
| process_create  | Process creation activity                 |
| execve          | Program execution calls                   |
| priv_ctrl       | Privilege escalation behavior             |
| errno_total     | Total syscall errors                      |
| errno_perm      | Permission-related errors                 |
| errno_enoent    | Missing file errors                       |
| touch_sensitive | Sensitive file access                     |
| w_x_transition  | Writable-to-executable memory transitions |
| uses_unlink     | File deletion behavior                    |
| duration        | Execution duration                        |
| rate_cps        | Syscalls per second                       |
| err_rate        | Error rate                                |
| net_ratio       | Ratio of network activity                 |
| label           | Malware (-1) / Benign (1)                 |

---

# Training the Model

The notebook trains an `Isolation Forest` model using extracted syscall features.

Example:

```python
from sklearn.ensemble import IsolationForest

model = IsolationForest(
    n_estimators=200,
    contamination=0.1,
    random_state=42
)
```

The trained model is saved as:

```text
iforest_strace.joblib
```

---

# Evaluating the Model

Run evaluation:

```bash
python evaluate_model.py
```

Example output:

```text
--- Evaluation Report ---

              precision    recall  f1-score   support

malware (-1)       0.90      0.85      0.87
 benign (1)        0.88      0.92      0.90
```

---

# Example CSV Format

```csv
io_rw,io_meta,net_total,net_ipv4,net_ipv6,net_unix,mem_mgmt,process_create,execve,priv_ctrl,errno_total,errno_perm,errno_enoent,touch_sensitive,w_x_transition,uses_unlink,duration,rate_cps,err_rate,net_ratio,label
120,45,80,70,0,10,33,4,2,1,25,3,8,1,1,1,12.5,44.2,0.20,0.66,-1
18,9,4,4,0,0,8,1,1,0,2,0,1,0,0,0,3.1,6.4,0.03,0.12,1
```

---

# Isolation Forest Labels

| Label | Meaning           |
| ----- | ----------------- |
| -1    | Malware / Anomaly |
| 1     | Benign / Normal   |

---

# Security Warning

⚠️ Run malware samples only inside:

* Virtual Machines
* Sandboxed environments
* Isolated Linux systems

Do NOT execute malware on your host operating system.

---

# Recommended Environment

* Ubuntu 22.04+
* Python 3.10+
* Google Colab
* Docker / VM preferred

---

# Future Improvements

* Real-time syscall monitoring
* eBPF integration
* Deep learning detection models
* Malware family classification
* Visualization dashboard
* Streaming anomaly detection

---

# Disclaimer

This project is intended for educational and cybersecurity research purposes only.

The author is not responsible for misuse of this project.
