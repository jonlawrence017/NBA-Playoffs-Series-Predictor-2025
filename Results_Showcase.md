# NBA Playoff Predictor: Results Showcase

## Overview
The NBA Playoff Predictor is a machine learning project designed to forecast NBA playoff series outcomes. Using a neural network trained on advanced team statistics (e.g., NetRtg, PIE, eFG%, TS%, and others from 2013-2024 seasons), the model predicts win probabilities for playoff matchups. Monte Carlo simulations further refine these predictions by simulating series outcomes thousands of times, accounting for variability. This project achieved a test accuracy of 73-74% on historical playoff data, demonstrating robust predictive power.

This document highlights key results and visualizations, complementing the technical details in the [README](README.md).

## Key Results
- **Model Performance**: The neural network, implemented in TensorFlow (`NBA_Playoff_NN.h5`), achieved 73-74% accuracy on test data, correctly predicting series outcomes for the 2025 playoff bracket.
- **Feature Selection**: Features like NetRtg, PIE, eFG%, and TS% were selected for their strong correlation with playoff success, validated through permutation importance and domain knowledge.
- **Monte Carlo Simulations**: Simulations (stored in `Monte_Carlo_Output`) provided probabilistic outcomes, such as the likelihood of lower-seeded teams upsetting higher seeds.
- **2025 Predictions**: For the 2025 playoffs, the model generated series win probabilities, detailed in `first_round_probabilities_2025_fixed_bracket_series.csv`.

## Visualizations
Below are key visualizations created to interpret the model’s predictions and insights, built using Tableau and Python.

### 1. Lower Seed Win Predictions: Offensive vs. Defensive Ratings
This plot shows the relationship between teams’ offensive and defensive ratings and their predicted win probabilities as lower seeds. Teams with higher offensive ratings and balanced defensive metrics tend to have higher upset potential.

![Lower Seed Win Predictions](Visualizations/Lower_Seed_Win_Predictions_OffvDef.png)

### 2. Monte Carlo Simulation: Series Outcome Probabilities
This visualization illustrates the distribution of series outcomes for a sample 2025 first-round matchup, based on 10,000 Monte Carlo simulations. The plot highlights the probability of each team winning in 4, 5, 6, or 7 games.

![Monte Carlo Series Outcomes](Visualizations/Monte_Carlo_Series_Probabilities.png)

### 3. Feature Importance
This bar chart displays the relative importance of input features (e.g., NetRtg, PIE) in the neural network’s predictions, derived from permutation importance analysis.

![Feature Importance](Visualizations/Feature_Importance.png)

## Conclusion
The NBA Playoff Predictor successfully combines machine learning and simulation techniques to forecast playoff outcomes with high accuracy. The visualizations above provide intuitive insights into the model’s predictions, highlighting key factors driving team success. For technical details, see the [README](README.md) or explore the code in `Run_Code`.

Feel free to reach out with questions or feedback about the project!
