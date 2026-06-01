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

- Normal operation
- High-load operation
- Unstable operation

The simulated degradation logic is:

```text
operating_regime → load / speed / pressure
load, speed, pressure → temperature
temperature, maintenance_delay, load → wear
wear, pressure → vibration
pressure, temperature, maintenance_delay, wear, vibration → failure
