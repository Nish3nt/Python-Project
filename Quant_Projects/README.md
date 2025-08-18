# Predictive Market-Making Strategy with LightGBM

This project outlines a comprehensive, end-to-end workflow for developing and backtesting a short-term, predictive trading strategy using high-frequency cryptocurrency data. The goal is to build a market-making algorithm that uses machine learning to predict price movements and dynamically adjust its quoting strategy to maximize profitability while managing risk.


# Introduction
High-frequency trading (HFT) strategies rely on micro-scale market signals to make rapid decisions. This project uses a limit order book (LOB) to build features that capture short-term supply and demand dynamics. A LightGBM model is trained to predict the direction of the mid-price, and these predictions are then used to inform a market-making simulation. The project's strength lies in its focus on realism, incorporating key market frictions like latency, order queueing, and inventory management.

# Methodology
The project follows a standard quantitative research pipeline:

Data Ingestion & Cleaning: Raw LOB data is loaded and standardized. A robust auto-detection mechanism identifies key columns (timestamps, bid/ask prices) and normalizes the data into a consistent format.

Feature Engineering: Features relevant to market microstructure are engineered, including:

Spread: The difference between the best bid and ask prices.

Imbalance: A measure of order book pressure across multiple levels.

Microprice: A volume-weighted mid-price that reflects liquidity distribution.

Volatility: A rolling measure of short-term price fluctuations.

Labeling: A binary target variable is created to predict whether the mid-price will move up or down over a short horizon (e.g., 50ms). The notebook includes an adaptive fallback mechanism to ensure a viable and balanced target, even with sparse data.

Model Training: A LightGBM model is trained to predict the labels. A time-series cross-validation scheme is used to prevent data leakage and provide an honest assessment of the model's out-of-sample performance. A Logistic Regression model serves as a simple baseline.

Strategy Simulation: A custom, queue-aware backtest simulator is used to run the market-making strategy. It incorporates:

Latency: The delay between a decision and an order's placement.

Order Queueing: Simulates waiting for fills at a specific price level.

Dynamic Sizing: Adjusts order sizes based on the model's confidence and current inventory.

PnL and Risk Tracking: Monitors mark-to-mid profit and loss, position, and transaction costs.

Performance Analysis: The strategy's performance is evaluated using metrics relevant to trading, such as ROC AUC, Precision@K, and an equity curve to visualize PnL over time. A latency sensitivity analysis demonstrates how performance degrades with increasing delays.

# Project Structure
The project is implemented in a single Jupyter Notebook for simplicity and self-containment.

Cells 1-2: Environment and data setup.

Cells 3-4: Data loading, cleaning, and preparation.

Cell 5: Feature engineering and target labeling.

Cells 6-8: Model training and evaluation.

Cells 9-11: Strategy simulation and performance analysis.

Cell 12: Project conclusion and key takeaways.
