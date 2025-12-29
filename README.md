🚨 AML Alert Prioritization using Machine Learning & Network Analysis

A system to rank suspicious financial transactions so investigators focus on the highest-risk alerts first.

📌 Problem Statement

Banks process millions of transactions every day.
Traditional AML (Anti-Money Laundering) systems generate huge numbers of alerts, but over 95% are false positives.

The real challenge is not detection — it is prioritization.

Which alerts should investigators look at first?

This project builds a data-driven AML alert ranking system that assigns risk scores to suspicious transactions and creates a priority queue for investigation teams — similar to how large fintech companies handle compliance at scale.

Instead of just predicting fraud, this system ranks alerts by risk, which is how modern AML operations work.


📊 Dataset

We use the PaySim synthetic banking dataset, which simulates:

Transfers

Cash-outs

Fraud patterns

Money laundering behavior

The raw dataset contains 6M+ transactions, which is too large and unrealistic to directly feed into a model.
So we first simulate a real bank rule engine.

⚙️ Rule-Based Alert Engine

Banks never send all transactions to machine learning. They first apply rules to filter suspicious activity.

Example rules:

High transaction amounts

Cash-outs

Transfers

This reduces the dataset from:

6 million → ~300,000 alerts

This makes the problem:

Computationally feasible

Realistic

Aligned with real AML pipelines

⏱️ Time-Aware Feature Engineering

Money laundering is not about one transaction — it is about patterns over time.

For each customer, we compute rolling behavioral features:

Features	Meaning:

txns_5	Number of transactions in last 5

txns_20	Number of transactions in last 20

amt_5	Total amount in last 5

amt_20	Total amount in last 20

max_20	Largest transaction in last 20

unique_receivers	Number of distinct recipients

These capture real laundering signals:

Structuring

Smurfing

Fund dispersion

Sudden spending spikes

🧠 Risk Scoring Model

We train an XGBoost model to predict a continuous AML risk score.

This is not fraud classification.
This is risk ranking.

The model learns patterns such as:

Frequent high-value transfers

Rapid cash-outs

Many recipients

Sudden changes in behavior

Model Output:

Risk score ∈ [0, 1]

Higher score = more suspicious


This allows the bank to sort alerts by risk and investigate the most dangerous ones first.

📈 Ranking Evaluation — NDCG

In AML, only the top of the investigation queue matters.

We evaluate the model using NDCG (Normalized Discounted Cumulative Gain) — a ranking metric used in:

Google Search

Recommendation systems

Financial risk engines

Results:

NDCG@10 = 0.87  

NDCG@50 = 0.83


This means that real fraud is consistently pushed to the top of the alert list.

🌐 Money Laundering Network Analysis

Criminals do not work alone — they operate in networks.

We build a transaction graph:

Nodes → Accounts

Edges → Money transfers

This reveals:

Hub accounts

Money mules

Circular laundering

Smurfing networks

Investigators can visually trace how money flows through suspicious networks.

🏦 Why This Project Matters

This project mirrors how modern AML platforms work:

Traditional AML	This System

Rules only	Rules + ML

Binary alerts	Risk ranking

Manual review	ML-guided priority

Transaction-level	Behavioral + network view

This makes it highly relevant for:

Banks

FinTech companies

Payment processors

Regulators

🛠️ Tech Stack:

Python

Pandas

XGBoost

NetworkX

Scikit-Learn

Matplotlib

🚀Future Work:

Deployment

Adding more real wod datasets

AI features for better explainability
