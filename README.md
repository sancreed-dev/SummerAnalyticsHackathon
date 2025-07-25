# SummerAnalyticsHackathon
# Capstone Project Submission: Dynamic Pricing for Urban Parking Lots

## Overview

This report documents the Model 2 implementation for the capstone project on Dynamic Pricing for Urban Parking Lots, as part of the Summer Analytics 2025 program. The project goal is to use real-time data to optimize parking lot pricing dynamically, improving resource utilization and creating a fair, explainable pricing structure.

## 1. Tech Stack Used

- **Programming Language:** Python 3 (Google Colab environment)
- **Key Libraries:**
  - **Pandas, Numpy:** Data handling and numerical computations
  - **Pathway:** Real-time data streaming and simulation
  - **Bokeh:** Interactive visualizations
- **Other Tools:** GitHub for version control and documentation

## 2. Architecture Diagram

Below is a conceptual architecture flow for the Model 2 system. 

    A[Pathway Input Stream] --> B[Feature Extraction]
    B --> C[Demand Scoring Function]
    C --> D[Dynamic Pricing Engine]
    D --> E[Real-time Price Emission]
    E --> F[Bokeh Visualization]
   




## 3. Project Architecture & Workflow

### Data Pipeline

- **Streaming Source:** Pathway reads batched and delayed data for all parking lots.
- **Feature Engineering:** Real-time extraction and normalization of attributes such as:
  - Occupancy rate ($$\frac{Occupancy}{Capacity}$$)
  - Queue length
  - Traffic congestion
  - Special day/event indicator
  - Vehicle type

### Model 2: Demand-Based Pricing

A composite demand score is calculated for each time step and parking lot using the formula:

$$
Demand = \alpha \cdot \left(\frac{Occupancy}{Capacity}\right) + \beta \cdot QueueLength - \gamma \cdot Traffic + \delta \cdot IsSpecialDay + \epsilon \cdot VehicleTypeWeight
$$

- **Weights ($$\alpha, \beta, \gamma, \delta, \epsilon$$)**: Hyperparameters selected empirically based on exploratory data analysis.
- **Price Calculation:**
  - Price starts from a base of $10.
  - At each step:

    $$
    Price_{t} = BasePrice \cdot (1 + \lambda \cdot NormalizedDemand)
    $$

  - **NormalizedDemand** ensures that price stays within logical limits.
  - Price is bounded for smooth variation (not more than 2x or less than 0.5x the base).

### Continuous Operation

- **Pathway** streams records, processes features, scores demand, and updates price in real time for all 14 parking lots.
- **Bokeh** provides visualization of price changes over time and across different lots.

## 4. Additional Documentation

### Demand Function Explanation

- **Occupancy:** Higher occupancy triggers a price increase to manage demand.
- **Queue Length:** Indicates excess demand; positive impact on pricing.
- **Traffic Condition:** Heavily congested areas may discourage increases; negative impact.
- **Special Day:** Increases expected demand, so price is adjusted upward.
- **Vehicle Type:** May add weight (e.g., heavier/larger vehicles pay more).

### Assumptions

- Demand function parameters are tuned empirically for realism and fairness.
- All models are built from scratch, only basic libraries are used as per requirements.
- No external APIs or advanced ML black boxes are utilized.

### Price Smoothing

- All temporal price changes are rate-limited to prevent erratic shifts.
- Demand is normalized for each parking lot individually, considering historical patterns.

### Visualization

- Bokeh charts are included in the notebook for real-time and comparative visualization.
- Visualizations justify price behavior and help inspect the impact of each feature.

## 5. Code Instructions

- All scripts, notebooks, and supporting files are present in the submitted repository.
- The code runs without errors in Google Colab and reproduces all results shown in visualizations.

## 6. Repository Access

- The GitHub repository is set to **public** or proper reviewer access has been provided as per guidelines.

*This documentation ensures all final submission instructions are met for Model 2 of the capstone on dynamic parking lot pricing using real-time analytics.*


