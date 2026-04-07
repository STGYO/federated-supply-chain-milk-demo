# Federated Learning for Supply Chain Optimization (Milk)

## Overview

This project simulates a Federated Learning (FL) system to optimize the supply chain for a perishable product (Milk). It predicts future demand using a distributed LSTM (Long Short-Term Memory) model, keeping raw data local to each client and sharing only model updates.

## System Architecture

How the system works:

1. Local training: Each client trains a local LSTM model on private sales data.
2. Federated averaging: Clients send model weights (not raw data) to the server.
3. Aggregation: The server averages weights into a global model.
4. Privacy: Differential privacy noise is added to model updates.
5. Optimization: The forecast drives order quantity decisions while balancing profit, waste, and emissions.

![System Architecture](architecture.png)

## Key Features

- Federated LSTM forecasting without sharing raw client data.
- Differential privacy noise injection for extra protection.
- Optimization logic for inventory, spoilage, and carbon-cap feasibility.
- Streamlit dashboard for simulation, charts, and what-if analysis.

## Setup and Run

1. Install dependencies:

```bash
pip install -r requirements.txt
```

1. Start the dashboard:

```bash
streamlit run app.py
```

## Real Data Mode (Implemented)

- Place client CSV files inside DATASETS.
- Example file names: client_1_amul_gujarat.csv, client_2_mother_dairy_delhi.csv, client_3_sudha_bihar.csv.
- In the Streamlit sidebar, set Data Source to real.
- In the Streamlit sidebar, set Dataset Directory to DATASETS.

The app now loads real client data directly from CSV and uses:

- demand as the forecasting target.
- disruption_prob for safety-stock risk logic.
- emission_factor for carbon-impact checks.

If fewer client CSV files are found than the selected client count, remaining clients are automatically backfilled with synthetic data.

## Project Structure

- main.py: Core logic for federated training, data management, and optimization.
- app.py: Streamlit dashboard.
- requirements.txt: Python dependencies.
