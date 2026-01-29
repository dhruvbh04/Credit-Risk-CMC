# Coupled Markov Chain Approach to Credit Risk Modeling

This repository contains the implementation and analysis of a **Coupled Markov Chain (CMC)** model for corporate credit rating transitions. The project replicates and extends the framework proposed by **Wozabal and Hochreiter (2012)** and applies it to a modern dataset to study the interaction between firm-level idiosyncratic risks and systematic macroeconomic effects.

This project was conducted at **BITS Pilani, Goa Campus**, under the guidance of **Prof. Mayank Goel**.

---

## 📄 Project Overview

Traditional credit risk models often assume independent rating transitions across firms. However, empirical evidence shows **default clustering during economic downturns**, indicating the presence of strong systemic effects.

This project models credit rating migrations as a mixture of:

- **Idiosyncratic Dynamics** – Firm-specific rating movements  
- **Systematic Dynamics** – Economy-wide movements driven by a latent macroeconomic state  

The main objective is to estimate:

- **Coupling parameters** that quantify how strongly firms are tied to the macroeconomy  
- **Latent economic state probabilities** using **Maximum Likelihood Estimation (MLE)**  

---

## 📚 Theoretical Background

The model is based on the following paper:

> Wozabal, D., & Hochreiter, R. (2012).  
> *A coupled Markov chain approach to credit risk modeling.*  
> Journal of Economic Dynamics and Control, 36(3), 403–415.

---

## 🧠 The Model

The credit rating \( X_n^t \) of company \( n \) at time \( t \) is modeled as a stochastic mixture:

\[
X_n^t = \delta_n^t \xi_n^t + (1 - \delta_n^t) \eta_n^t
\]

Where:

- \( \xi_n^t \): Idiosyncratic (firm-specific) component  
- \( \eta_n^t \): Systematic (macroeconomic) component  
- \( \delta_n^t \): Bernoulli mixing variable  
- \( q_{m,s} \): Coupling probability for rating class \( m \) and sector \( s \)

---

## ⚙️ Optimization Methods

The likelihood function of the CMC model is **non-convex**. Two optimization techniques are used:

- **Particle Swarm Optimization (PSO)**  
  - Global, heuristic optimizer  
  - Effective for parameter space exploration  

- **Sequential Least Squares Programming (SLSQP)**  
  - Gradient-based constrained optimizer  
  - Used for refinement and constraint satisfaction  

---

## 📂 Repository Structure

├── ASPProjectDhruvPrabhsimar.ipynb # Main notebook (Preprocessing, MLE, PSO/SLSQP)
├── ProjectReportDhruvPrabhsimar.pdf # Detailed report and results
├── 1-s2.0-S0165188911001850-main.pdf # Reference paper (Wozabal & Hochreiter, 2012)
└── README.md # Project documentation


---

## 📊 Data Availability

- **Dataset:** Corporate Credit Rating with Financial Ratios  
- **Source:** Kaggle  

### Preprocessing
- Raw ratings (AAA, AA+, etc.) are aggregated into:
  - **4 non-default rating classes**
  - **1 default state**
- This matches the methodology of the reference paper.

---

## 🚀 Installation & Usage

### Prerequisites

- Python 3  
- Required libraries:

```bash
pip install numpy pandas scipy pyswarm
