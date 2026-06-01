# Lagged Causal Signals in Industrial Failure Diagnosis

## Overview

This project presents an exploratory simulation study of lag-aware root-cause diagnosis in industrial machine failures.

The project uses a synthetic multivariate time-series simulation of an industrial machine operating under changing regimes, with noisy sensor measurements, maintenance delay events, gradual component wear, and rare failure events.

The goal is to compare simple contemporaneous correlation with lag-aware statistical analysis for identifying candidate root-cause signals.

## Research Questions

The project addresses three questions:

1. How informative is a naive correlation-based ranking when failures are rare and binary?
2. Can lag-aware statistical analysis recover meaningful time-ordered relationships in a simulated degradation process?
3. Can candidate root-cause signals be distinguished from late-stage symptoms in a transparent and interpretable way?

## Simulation Design

The synthetic system represents a simplified industrial machine operating over 1,500 time steps.

The machine switches between three operating regimes:

Normal operation
High-load operation
Unstable operation

The simulated degradation logic is:

operating_regime -> load / speed / pressure
load, speed, pressure -> temperature
temperature, maintenance_delay, load -> wear
wear, pressure -> vibration
pressure, temperature, maintenance_delay, wear, vibration -> failure

The generated dataset contains 45 failure events, corresponding to a failure rate of 3%. This creates an imbalanced rare-event setting similar to practical industrial failure diagnosis problems.

## Methodology

The project compares several diagnostic approaches:

Correlation-based baseline
Computes contemporaneous correlations between each variable and the binary failure indicator.
Lagged dependency scoring
Computes lagged correlations between source variables and target variables across several time lags.
Granger-style time-ordered analysis
Tests whether past values of one variable help predict the current value of another variable.
Root-cause signal ranking
Combines lag-aware dependency information and Granger-style evidence to rank candidate diagnostic signals.
Predictive validation
Trains a logistic regression model with lagged features using a time-based train-test split.
Key Findings
Naive contemporaneous correlations with failure are weak and difficult to interpret.
Lag-aware analysis recovers several meaningful time-ordered relationships from the simulated degradation process, including:
load -> temperature
temperature -> wear
wear -> vibration
wear -> failure
The exploratory root-cause ranking highlights degradation-related variables such as wear, vibration, temperature, load, and pressure.
A logistic regression model with lagged features achieves a test ROC AUC of 0.804.
Lag-aware methods provide a more structured diagnostic view than correlation alone.
The results should be interpreted as exploratory time-ordered predictive evidence, not as definitive causal discovery.
Local Failure Case Study

The project includes a local pre-failure analysis for one failure event.

The analysis compares average values of key degradation-related variables shortly before the failure with an earlier baseline window. In this case, temperature, vibration, and wear increase substantially before the failure, supporting the interpretation of a degradation-driven failure pattern.

## Limitations

This project is intentionally small and stylized. Its main limitations are:

The dataset is synthetic rather than empirical.
The simulated causal structure is simplified and known by design.
Granger-style tests indicate time-ordered predictive signals, not definitive causality.
The approach does not estimate causal effect sizes.
Hidden confounding, feedback loops, and non-stationarity are only partially represented.
Future Work

## Possible extensions include:

Testing more rigorous causal discovery methods.
Incorporating engineering domain constraints.
Modelling stronger non-stationarity in operating conditions.
Adding maintenance logs or text-based failure descriptions.
Estimating causal effects using methods such as Double Machine Learning or Causal Forests.
Applying the framework to empirical industrial sensor data.

## Report

The full project report is available here:

industrial_failure_lagged_causal_signals_report.pdf

## Repository Structure 

industrial_failure_lagged_causal_signals.ipynb — Jupyter notebook with the simulation study
industrial_failure_lagged_causal_signals_report.pdf — Project report
requirements.txt — Python dependencies
README.md — Project description
How to Run
