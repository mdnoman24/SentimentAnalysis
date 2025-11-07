## 🧠 Project Description

**Project29 – Full Sentiment Analysis** is a complete end-to-end **data analytics and NLP pipeline** designed to analyze hotel review datasets.  
It performs **statistical analysis** — including mean, standard deviation, and kurtosis — to evaluate rating consistency and identify **ambiguous hotel ratings** using a dynamic **ε-threshold (epsilon)** approach based on standard deviation.

The project integrates **Natural Language Processing (NLP)** models such as **TextBlob**, **VADER**, and **spaCy** for textual sentiment scoring, enabling both polarity and subjectivity assessment of review content.  
Data aggregation, feature computation, and visualization are implemented in **Python (Pandas, NumPy, Matplotlib)**, producing analytical outputs such as the **Proportion of Ambiguous Hotels per Star Category**.

All intermediate and final outputs (CSV, Excel, Parquet) are automatically exported into a unified **SQLite database** for structured storage, downstream querying, or visualization in BI tools (e.g., Power BI, Tableau).  
The notebook-based architecture ensures **reproducibility**, **scalability**, and **flexibility** for extending the analysis to other review-driven or sentiment-based datasets.



# ⚙️ Installation & Setup Guide

This guide walks you through everything needed to set up and run **Project29 – Full Sentiment Analysis**.

---

## 🧩 1. System Requirements

| Requirement | Recommended |
|--------------|-------------|
| **Python** | 3.9 – 3.12 |
| **OS** | Windows / macOS / Linux |
| **RAM** | 4 GB minimum (8 GB recommended) |
| **Disk Space** | 2–3 GB depending on dataset size |

Optional (for NLP models):
- **GPU:** NVIDIA CUDA-compatible (for Transformers or PyTorch acceleration)

---

## 📦 2. Install Python & Virtual Environment

### 🐍 Install Python
Download and install from [python.org/downloads](https://www.python.org/downloads/).

### 🧱 Create a Virtual Environment
To keep dependencies isolated:

```bash
# Create virtual environment
python -m venv .venv

# Activate (Mac/Linux)
source .venv/bin/activate

# Activate (Windows)
.venv\Scripts\activate



📚 3. Install Required Libraries

🔹 Core Data Libraries


pip install pandas numpy matplotlib scikit-learn scipy openpyxl pyarrow sqlite3


🛠️ 4. Project Configuration

In your notebook or Python script, make sure the output directories are created:

import os

# Folder for exported CSV, Excel, and Parquet data
OUTPUT_DIR = os.path.join(os.getcwd(), "OUTPUT_DIR")
os.makedirs(OUTPUT_DIR, exist_ok=True)

# Folder for database exports
DB_FOLDER = os.path.join(os.getcwd(), "DB_Output")
os.makedirs(DB_FOLDER, exist_ok=True)


🚀 5. Running the Project

Launch Jupyterjupyter lab
# or
jupyter notebook


Open Project29_Full_Sentiment_Analysis.ipynb and run the cells sequentially.

⸻

💾 6. Database Export (Optional but Recommended)

At the end of your notebook, add this code block to convert all output files into a single database:

import os, sqlite3, pandas as pd
from pathlib import Path

DB_FOLDER = os.path.join(os.getcwd(), "DB_Output")
os.makedirs(DB_FOLDER, exist_ok=True)
DB_PATH = os.path.join(DB_FOLDER, "project_data.db")
conn = sqlite3.connect(DB_PATH)

# Loop through all output files
all_files = [
    os.path.join(OUTPUT_DIR, f)
    for f in os.listdir(OUTPUT_DIR)
    if f.lower().endswith((".csv", ".xlsx", ".parquet"))
]

for file_path in all_files:
    file_name = Path(file_path).stem
    if file_path.endswith(".csv"):
        df = pd.read_csv(file_path)
    elif file_path.endswith(".xlsx"):
        df = pd.read_excel(file_path)
    elif file_path.endswith(".parquet"):
        df = pd.read_parquet(file_path)
    df.to_sql(file_name, conn, if_exists="replace", index=False)

conn.commit()
conn.close()
print(f"✅ All data saved to database: {DB_PATH}")


🧠 7. Verify Installation

Run this in your notebook to confirm dependencies:

import pandas as pd, numpy as np, matplotlib, sklearn, sqlite3
print("✅ All core libraries are installed and working!")


