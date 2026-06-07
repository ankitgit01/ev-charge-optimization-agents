# EV Dynamic Pricing Agentic AI Framework

## Overview
This repository contains a comprehensive multi-agent artificial intelligence framework designed to optimize electric vehicle (EV) charging networks. By leveraging real-world charging session data and spatiotemporal network data, the system predicts charging demand, dynamically adjusts tariffs to balance grid load, and continuously learns from operational feedback to improve pricing strategies over time.

## Methodology
The framework operates using three interconnected AI agents:

1. **Demand Prediction Agent (Forecasting):** Utilizes machine learning models (XGBoost, LightGBM, Random Forest) to analyze historical data, cyclical time encodings, and rolling lag features. It predicts charger utilization rates and the probability of station congestion before it occurs.

2. **Tariff Pricing Agent (Dynamic Optimization):** A hybrid rule-based and ML engine that translates demand forecasts into optimal dynamic tariffs. It implements progressive surge pricing to deter charging during severe congestion (e.g., utilization >= 80%) and offers discount pricing during idle hours to incentivize off-peak charging and shift user demand.

3. **Monitoring and Learning Agent (Feedback Loop):** Acts as the continuous evaluation mechanism. It treats each operational day as an episode, tracking key performance indicators such as pricing efficiency, revenue gain, and congestion rates. It autonomously adjusts the surge and discount thresholds based on rolling performance signals to continuously improve the policy.

## Technology Stack
* **Language:** Python 3.10+
* **Machine Learning:** Scikit-Learn, XGBoost, LightGBM
* **Data Manipulation:** Pandas, NumPy, SciPy
* **Visualization:** Matplotlib, Seaborn, Plotly
* **Environment:** Jupyter Notebook / Google Colab

## Datasets Used
* **ACN-Data (Caltech/JPL):** Over 30,000 real EV charging sessions accessed via REST API, providing user-level connection, disconnection, and energy delivery metrics.
* **ST-EVCDP (UrbanEV):** High-resolution, 5-minute interval spatiotemporal data covering 18,061 charging piles across Shenzhen, used for network-level congestion analysis.

## How to Run

1. **Clone the Repository:**
   git clone https://github.com/ankitgit01/ev-charge-optimization-agents.git
   cd ev-dynamic-pricing-ai

3. **Install Dependencies:**
   Ensure you have Python installed, then run:
   pip install -r requirements.txt

4. **Obtain API Credentials:**
   Register at ev.caltech.edu/register to get a free ACN-Data API token.

5. **Execute the Notebook:**
   Open EV_Dynamic_Pricing_Agentic_AI.ipynb in Jupyter Notebook or Google Colab. When prompted in the early cells, paste your ACN-Data API token. Run all cells sequentially. 

6. **View Outputs:**
   The final cells will generate a comprehensive summary dashboard and export CSV files containing model scores, pricing outcomes, and episode logs to the submission_outputs directory.

## Key Results
* **Demand Prediction:** Historical lag features and cyclical time encodings successfully captured temporal and spatial dependencies, resulting in highly accurate utilization predictions.
* **Grid Balancing and Revenue:** The dynamic pricing engine demonstrated a positive revenue gain over a standard fixed baseline tariff. By applying off-peak discounts, the framework successfully identified significant portions of sessions eligible for demand shifting.
* **Autonomous Improvement:** Over simulated daily episodes, the Monitoring Agent autonomously optimized policy parameters, yielding a measurable improvement in pricing efficiency and a reduction in peak congestion rates when comparing the final episodes to the initial ones.

## Future Scope
* **Multi-Agent Reinforcement Learning (MARL):** Transitioning the rule-based policy updates to a deep reinforcement learning architecture (e.g., PPO or DQN) for more complex, non-linear pricing strategies.
* **Vehicle-to-Grid (V2G) Integration:** Expanding the pricing models to account for bi-directional charging, allowing users to sell energy back to the grid during extreme surge periods.
* **External Data Integration:** Incorporating real-time weather APIs and local traffic congestion data to improve the accuracy of the Demand Prediction Agent.
* **Live API Deployment:** Wrapping the agents in a FastAPI backend to serve dynamic tariffs in real-time to simulated or physical charging pile endpoints.
