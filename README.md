# 🔐 Hybrid Quantum Communication Protocol: Q-PUF & BB84

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Qiskit](https://img.shields.io/badge/Qiskit-Hardware%20Simulation-purple.svg)
![NetSquid](https://img.shields.io/badge/NetSquid-Network%20Simulation-teal.svg)
![Cybersecurity](https://img.shields.io/badge/Security-Information%20Theoretic-red.svg)

## 📌 Project Overview
This repository contains the implementation of an advanced, two-stage **Defense-in-Depth** quantum security protocol. 

Traditional Quantum Key Distribution (QKD) protocols, while unconditionally secure under the laws of physics, suffer from the "Chicken-and-Egg" dilemma: they require a pre-shared secret key on an authenticated classical channel to prevent Man-in-the-Middle attacks during the sifting phase. 

This project solves this vulnerability by introducing an autonomous **Hardware-bound Authentication** phase using Quantum Physical Unclonable Functions (**Q-PUF**), eliminating the need for pre-shared digital keys, followed by a secure **BB84 QKD** implementation.

**Authors:** Carmine Cataldo, Francesca Pellegrino  
**Course:** Quantum Technologies for Security - *University of Salerno*

---

## 🏗️ System Architecture & Frameworks

The system orchestrates two specialized quantum frameworks to simulate both the microscopic thermodynamic flaws of the hardware and the macroscopic optical network physics.

### Stage 1: Hardware Authentication (Qiskit)
Instead of correcting thermodynamic noise, we exploit it. 
*   **The Q-PUF:** We built a deep Random Quantum Circuit (RQC) with `depth=7`.
*   **The Fingerprint:** Using Qiskit's `NoiseModel`, we assigned unique $T_1$ (Thermal Relaxation) and $T_2$ (Dephasing) parameters to the receiver's chip. 
*   **The Result:** When Alice sends a challenge (rotation angles), the circuit acts as a magnifying glass for these microscopic flaws, generating a highly entangled, hardware-unique probabilistic response (Total Variation Distance).

### Stage 2: Quantum Key Distribution (NetSquid)
Once the hardware is authenticated, the network layer takes over.
*   **The Protocol:** BB84 discrete-event simulation.
*   **The Physics:** We utilized the **Density Matrix Formalism** to realistically model a fiber optic channel with a $2\%$ natural depolarizing noise.

---

## 🛡️ Threat Modeling & Attack Simulation

To mathematically prove the protocol's robustness, an adversary (**Eve**) was introduced into the simulation:
1. **Q-PUF Forgery Attack:** Eve intercepts the Challenge and tries to simulate the Response. *Result:* Even knowing the exact logical circuit (Kerckhoffs's Principle), Eve fails (TVD > Threshold) because she cannot clone the exact thermodynamic noise profile of the legitimate silicon chip.
2. **Intercept-Resend Attack (BB84):** Eve intercepts photons on the fiber channel, measures them, and resends them. *Result:* Dictated by the **No-Cloning Theorem** and Wavefunction Collapse, Eve's intrusion irreversibly alters the states. The simulation correctly outputs a **QBER of ~26.67%** (25% theoretical error + ~2% fiber noise), instantly triggering a protocol abort.

---

## 📂 Repository Structure

*   `/src/` : The main Jupyter/Kaggle Notebook containing the end-to-end Orchestrator.
*   `/results/` : Generated Q-PUF circuit architectures and attack logs.
*   `/docs/` : Academic report (LaTeX/PDF) and presentation slides.

---

## ⚙️ How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/Carm1neBread/Quantum-Secure-Communication-QPUF-QKD.git
   cd Quantum-Secure-Communication-QPUF-QKD
   ```
4. Open and run the Jupyter Notebook located in `/src/`.

   _The notebook is completely self-contained. The first cell will automatically handle the installation of all required dependencies, including fixing C-API version conflicts._

   **Note for External Users:**
   
   The Jupyter Notebook is configured with an interactive fallback. If you run it locally or on Google Colab, a prompt will securely ask for your free `netsquid.org` credentials to install the required network simulator.

   
