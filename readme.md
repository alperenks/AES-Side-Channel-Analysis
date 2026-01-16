# AES-128 Side-Channel Analysis (DPA Simulation)

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Educational-orange.svg)

## 📌 Project Overview
This repository contains a **Differential Power Analysis (DPA)** simulation targeting the **AES-128 encryption algorithm**. The project demonstrates how cryptographic hardware implementations can be vulnerable to physical attacks, specifically through power consumption leakage.

Using statistical analysis (Difference of Means), the script successfully recovers the **128-bit Secret Key** byte-by-byte without any knowledge of the internal state of the cipher, relying solely on power trace data.

## 🎯 Key Features
* **Power Trace Processing:** Analyzes simulated power consumption data corresponding to AES operations.
* **Leakage Modeling:** Utilizes the AES S-Box output to model power consumption for specific bit transitions.
* **Statistical Attack Engine:** Implements the **Difference of Means** method to distinguish the correct key candidate from incorrect guesses.
* **Signal Visualization:** Visualizes raw power traces and the resulting differential peaks to verify the attack's success.

## ⚙️ Technical Methodology

The attack follows these core engineering steps:

1.  **Data Acquisition:** Ingesting $N$ power traces ($T$) and their corresponding plaintext inputs ($P$).
2.  **Hypothesis Generation:** For each key byte guess ($K_{guess} \in [0, 255]$), we calculate the intermediate value:
    $$V = SBox[ P \oplus K_{guess} ]$$
3.  **Partitioning:** Traces are split into two sets based on the value of a target bit (0 or 1) in the intermediate value $V$.
4.  **Differential Analysis:** We compute the difference between the means of these two sets.
    $$\Delta = | \mu_{group1} - \mu_{group0} |$$
    The correct key guess yields the highest differential spike (ghost peak), exposing the secret key.

## 📊 Results & Visualization

### 1. Power Trace Sample
*The raw power consumption signal captured during the encryption process.*

[Power Trace]
<img width="1017" height="479" alt="power_traces" src="https://github.com/user-attachments/assets/e51e9112-667b-4845-b086-fec1eaaac366" />

### 2. Attack Success (Key Recovery)
*The graph below shows the differential spike for the correct key byte. The highest peak indicates the correct hexadecimal value.*

[Attack Result]
<img width="1009" height="557" alt="correlation_graph" src="https://github.com/user-attachments/assets/6ca80919-d5bb-43d8-b396-b5057994033d" />

## 🚀 Installation & Usage

### Requirements
* Python 3.8+
* Jupyter Notebook

* NumPy, Matplotlib, SciPy

### Setup
1. Clone the repository:
   ```bash
   git clone [https://github.com/alperenks/AES-Side-Channel-Analysis.git](https://github.com/alperenks/AES-Side-Channel-Analysis.git)
