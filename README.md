Coupled Markov Chain Approach to Credit Risk Modeling

This repository contains the implementation and analysis of a Coupled Markov Chain (CMC) model for corporate credit rating transitions. This project replicates and extends the framework proposed by Wozabal and Hochreiter (2012), applying it to a modern dataset to analyze the interplay between idiosyncratic firm risks and systematic macroeconomic effects.

This project was conducted at BITS Pilani, Goa Campus under the guidance of Prof. Mayank Goel.

📄 Project Overview

Standard credit risk models often assume independent rating transitions. However, empirical evidence shows that defaults cluster during economic downturns. This project models credit rating migrations as a mixture of:

Idiosyncratic Dynamics: Firm-specific movements.

Systematic Dynamics: Market-wide movements driven by a latent economy state.

The core objective is to estimate the coupling parameters (how strongly firms are tied to the economy) and the probability distribution of the latent economic states using Maximum Likelihood Estimation (MLE).

📚 Theoretical Background

The model is based on the paper:

Wozabal, D., & Hochreiter, R. (2012). A coupled Markov chain approach to credit risk modeling. Journal of Economic Dynamics and Control, 36(3), 403-415.

The Model

The rating $X_n^t$ of company $n$ at time $t$ is modeled as a stochastic mixture:

$$X_n^t = \delta_n^t \xi_n^t + (1 - \delta_n^t) \eta_n^t$$

Where:

$\xi_n^t$: Idiosyncratic component (firm-specific risk).

$\eta_n^t$: Systematic component (macroeconomic risk).

$\delta_n^t$: A Bernoulli mixing variable determined by the coupling probability $q_{m,s}$ (for rating class $m$ and sector $s$).

We implement two optimization algorithms to maximize the non-convex Likelihood function:

Particle Swarm Optimization (PSO): A heuristic global optimizer.

Sequential Least Squares Programming (SLSQP): A gradient-based local optimizer for refining constraints.

📂 Repository Structure

├── ASPProjectDhruvPrabhsimar.ipynb    # Main source code (Preprocessing, MLE, PSO/SLSQP)
├── ProjectReportDhruvPrabhsimar.pdf   # Detailed project report and findings
├── 1-s2.0-S0165188911001850-main.pdf  # Original reference paper (Wozabal & Hochreiter)
└── README.md                          # Project documentation


📊 Data Availability

The model was trained using the Corporate Credit Rating with Financial Ratios dataset.

Source: Kaggle

Preprocessing: The raw ratings (AAA, AA+, etc.) were aggregated into 4 non-default classes and 1 default state to match the methodology of the reference paper.

🚀 Installation & Usage

Prerequisites

The project requires Python 3 and the following libraries:

pip install numpy pandas scipy pyswarm


Running the Project

Download the dataset from the Kaggle link above.

Place the CSV file in the root directory.

Open ASPProjectDhruvPrabhsimar.ipynb in Jupyter Notebook or Google Colab.

Run the cells sequentially to:

Process the data and generate the transition matrix $P$.

Run the PSO optimization loop.

Run the SLSQP optimization loop.

Visualize the estimated $Q$ matrix and $P_\chi$ distribution.

📈 Key Results

Our analysis yielded the following insights, detailed in ProjectReportDhruvPrabhsimar.pdf:

Optimization Performance:

SLSQP outperformed PSO in terms of convergence speed and solution cleanliness. It achieved a Log-Likelihood of 12.26.

Coupling Structure ($Q$ Matrix):

High-rated firms (Classes 0-1) exhibited high $q$ values ($\approx 1.0$), indicating their rating changes are primarily idiosyncratic (firm-specific).

Low-rated firms showed stronger coupling with the systematic economy, confirming they are more vulnerable to market downturns.

Latent Economy States ($P_\chi$):

The dominant economic state was found to be (1, 1, 1, 1) (non-deterioration across all classes) with a probability of ~0.62.

This closely replicates the findings of the original paper ($\approx 0.67$), validating the model implementation.

👥 Contributors

Dhruv Bhardwaj (2022B4A31271G)

Prabhsimar Singh (2022B4A31257G)

Department of Mathematics, BITS Pilani Goa Campus

🔗 References

Wozabal, D., & Hochreiter, R. (2012). A coupled Markov chain approach to credit risk modeling. Journal of Economic Dynamics and Control.

Delwadia, K. (2023). Corporate Credit Rating with Financial Ratios. Kaggle.