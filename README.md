## 🛠️Dynamic Pricing for Urban Parking Lots Capstone Project 2025
** 📖 Introduction**

This project implements a dynamic pricing engine for urban parking spaces, designed to optimize utilization and revenue by adjusting prices in real-time based on various factors like demand, competition, and environmental conditions. It simulates a real-world system where traditional static pricing often leads to inefficiencies such as overcrowding or underutilization.


The core of this project involves developing intelligent, data-driven pricing models from scratch using fundamental libraries, and integrating them into a real-time data streaming and processing pipeline.

## 🎯 Objectives

* Design **three adaptive pricing models**: baseline linear, demand-weighted, and geo-competitive.
* Simulate **real-time price adjustments** as demand changes over time.
* Implement **rerouting logic** to redirect vehicles from full lots to nearby alternatives.
* Provide a **Streamlit dashboard** to visualize price changes and simulate the system interactively.
* Enable smarter city-level parking distribution using data-centric logic.

## 🚀 Tech Stack

**Python**: The primary programming language for all logic and model implementations.

**Pandas:** Used extensively for data manipulation, cleaning, and feature engineering.

**NumPy**: Utilized for numerical operations, especially in mathematical model calculations.

**Pathway** (Conceptual Integration): A powerful framework for building real-time data pipelines, used conceptually in this project for streaming data
ingestion, real-time feature processing, and continuous pricing predictions.

**Bokeh**: Employed for generating interactive, real-time visualizations to monitor and justify pricing behavior.

## 🏗️ Project Architecture and Workflow
The project follows a modular architecture, processing data through several stages to arrive at dynamic pricing recommendations.

**Architecture Diagram**

graph TD

    A[Raw Data Stream: dataset.csv] --> B(Pathway Ingestion: Real-time Data Stream);
    
    B --> C{Pathway Preprocessing & Feature Engineering};
    
    C --> D{Pricing Models};
    
    D -- Model 1: Baseline Linear --> D1[Price_t+1 = Price_t + α * OccupancyRate];
    
    D -- Model 2: Demand-Based --> D2[Demand Function & Price_t = BasePrice * (1 + λ * NormalizedDemand)];
    
    D -- Model 3: Competitive --> D3[Haversine Distance & Competitor Price Factor];
    
    D1 & D2 & D3 --> E(Pathway Output Stream: Real-time Prices);
    
    E --> F[Bokeh Real-time Visualizations];
    
    F --> G[Monitoring & Justification of Pricing];
    

## 🎯Detailed Workflow Explanation

**Data Ingestion (Pathway)**
The dataset.csv file, containing historical parking data (occupancy, queue length, traffic, vehicle type, location, etc.), is conceptually ingested as a real-time data stream using Pathway. Pathway ensures data is streamed with simulated delays while preserving timestamp order.

**Preprocessing & Feature Engineering (Pathway/Pandas/NumPy)**:

**As data streams in, it undergoes preprocessing. This includes**:

Combining LastUpdatedDate and LastUpdatedTime into a single Timestamp.

**Calculating OccupancyRate (Occupancy / Capacity).**

Encoding categorical features like VehicleType (into VehicleTypeWeight) and TrafficConditionNearby (into TrafficConditionEncoded) into numerical representations.

These transformations are designed to be compatible with Pathway's real-time processing capabilities.

**Pricing Models (Pandas/NumPy)**:
The core of the dynamic pricing logic is implemented through three progressively sophisticated models:

### 🔹Model 1: **Baseline Linear Model**:

A simple linear relationship where the next price is adjusted based on the current occupancy rate relative to the previous price. This serves as a foundational reference point.

**Price_t+1 = Price_t + α * OccupancyRate**

Prices are bounded to prevent erratic fluctuations.

### 🔹Model 2: **Demand-Based Price Function**:

A more intelligent model that first constructs a mathematical demand function using multiple features: OccupancyRate, QueueLength, TrafficConditionEncoded, IsSpecialDay, and VehicleTypeWeight.

**Demand = α1·OccupancyRate + α2·QueueLength + α3·Traffic + α4·IsSpecialDay + α5·VehicleTypeWeight**

The calculated raw demand is then normalized to a [0, 1] range.

The normalized demand directly influences the price: **Price_t = BasePrice * (1 + λ * NormalizedDemand)**.

Strict bounds (0.5x to 2x BASE_PRICE) are applied to ensure smooth and explainable price variations.

### 🔹Model 3: **Competitive Pricing Model (Optional)**:

This model introduces location intelligence. It calculates the geographical proximity between parking spaces using the Haversine formula based on Latitude and Longitude.

It then identifies "nearby" competitors based on a defined distance threshold.

The model factors in competitor prices by calculating an AvgCompetitorPrice and a CompetitiveAdvantageFactor.

This competitive factor is integrated into the Model 2 pricing logic, allowing the system to increase prices when competitors are expensive or suggest adjustments when the lot is full and nearby alternatives are cheaper.

**Pathway Output Stream**:

The calculated dynamic prices from the chosen model (or all models for comparison) are continuously emitted as an output stream by Pathway.

**Real-time Visualizations (Bokeh)**:

Bokeh is used to create interactive plots that consume the real-time price data.

## Key visualizations include:

Real-time pricing line plots: Showing price changes over time for individual parking spaces across different models.

Comparison with competitor prices: Illustrating how a specific lot's price compares to its nearby competitors, visually justifying the competitive pricing strategy.

Occupancy Rate vs. Price: Demonstrating the relationship between a lot's occupancy and its dynamically set price.

These visualizations are crucial for monitoring the system's behavior and providing a visual justification for the pricing decisions.

## 📁 Repository Structure



├── dataset.csv           # The raw dataset containing parking lot information.

├── problem statement.pdf     # Detailed project description and requirements.

└── dynamic_pricing_notebook.ipynb # The main Jupyter Notebook containing all code.

└── README.md                 # This file.

## 🔮 Future Work

* Integrate **live traffic APIs** (e.g., Google Maps) for real-time congestion updates.
* Build a **driver-facing mobile app** that displays optimal nearby parking with live prices.
* Add **reinforcement learning** to self-tune model weights based on revenue vs fairness.
* Use **map-based visualization** for geographic monitoring of all lots.
* Deploy the app publicly using **Streamlit Cloud or AWS Lambda**.

## 📝 Usage

**Clone the repository**:

git clone <repository-url>
cd dynamic-parking-pricing

**Upload dataset.csv**: Ensure dataset.csv is in the same directory as the Jupyter notebook, especially if running in Google Colab.

**Open the Jupyter Notebook**: Open dynamic_pricing_notebook.ipynb in Google Colab or a local Jupyter environment.

**Install Dependencies**: Run the initial cells to install necessary libraries (Pandas, NumPy, Bokeh).

**pip install pandas numpy bokeh**

**Execute Cells**: Run all cells sequentially to perform data preprocessing, model calculations, and generate visualizations.

**Pathway Integration (Conceptual)**: The Pathway section is conceptual. To run a live Pathway application, you would need to set up a Pathway environment and adapt the conceptual code to a runnable streaming pipeline.

**🤝 Contributing**
Feel free to fork this repository, implement further enhancements, or suggest improvements!

## 🌟 Acknowledgements

This project was developed as part of Summer Analytics Course 2025 Academic Work at **Indian Institute of Technology (IIT) Guwahati**.

Special thanks to:

* **Pathway** – for real-time data streaming tools.
* **Streamlit** – for rapid dashboard development.
* **OpenStreetMap** – for geospatial context.
* **Plotly & Bokeh** – for powerful interactive plotting.


