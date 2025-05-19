# NBA Playoff Predictor: Results Showcase

## Overview
The NBA Playoff Predictor leverages machine learning to forecast NBA playoff series outcomes. A TensorFlow neural network, trained on advanced team statistics (e.g., NetRtg, PIE, eFG%) from the 1996–2024 seasons, predicts win probabilities for 2025 playoff matchups. Monte Carlo simulations, run thousands of times per series, estimate each team’s probability of advancing through each playoff round. The model achieves ~74% accuracy for individual series outcomes on historical test data. This document highlights key results and visualizations, complementing the technical details in the [README](README.md).

## Key Results
- **Model Performance**: The neural network (`NBA_Playoff_NN.h5`) delivers 73–74% accuracy on historical test data, reliably predicting 2025 playoff series outcomes.
- **2025 Predictions**: Series win probabilities for the 2025 playoffs are detailed in `first_round_probabilities_2025_fixed_bracket_series.csv` and visualized in `Visualizations/2025_Round_Percentages.png`.

## Visualizations
Below are key visualizations, created with Tableau and Python, to interpret the model’s predictions and explore patterns in playoff outcomes. Note: PIE (Player Impact Estimate) measures a team’s overall statistical contribution; see the [NBA Stats FAQ](https://www.nba.com/stats/help/faq) for details.

### 1. 2025 Round Advancement Probabilities
This visual illustrates each team’s probability of advancing past each round of the 2025 NBA playoffs, derived from model predictions and Monte Carlo simulations.

![2025 Round Advancement Probabilities](Visualizations/2025_Round_Percentages.png)

**Takeaways**: The chart identifies favorites and potential dark horses for the 2025 playoffs, with probabilities reflecting team strength and matchup dynamics based on historical trends.

### 2. Lower Seed Win Predictions (Upsets)
These scatter plots assess the model’s success in predicting upsets (lower seed wins). Each dot represents a playoff series where the model predicted an upset (green = correct, red = incorrect). The plots analyze four model features:
- **T1vT2_Off-Def**: Team 1’s offensive rating minus Team 2’s defensive rating.
- **T2vT1_Off-Def**: Team 2’s offensive rating minus Team 1’s defensive rating.
- **T1-T2_W**: Difference in regular-season wins.
- **T1-T2_PIE**: Difference in Player Impact Estimate.

![Lower Seed Win Predictions: Offense vs. Defense](Visualizations/Lower_Seed_Win_Predictions_OffvDef.png)

**Takeaways**: The even distribution of green and red dots suggests no clear pattern in upset predictions based on offensive-defensive rating differences. Small clusters of correct and incorrect predictions hint at localized trends, but more data is needed for definitive insights.

![Lower Seed Win Predictions: Wins vs. PIE](Visualizations/Lower_Seed_Win_Predictions_WvPIE.png)

**Takeaways**: The spread of dots shows no distinct pattern in upset predictions based on wins and PIE differences, similar to the OffvDef plot. Additional data could reveal subtle trends in model behavior.

### 3. Higher Seed Win Predictions (Non-Upsets)
These scatter plots evaluate the model’s success in predicting non-upsets (higher seed wins). Each dot represents a series where the model predicted a higher seed win (green = correct, red = incorrect). The same four features are analyzed to identify prediction patterns.

![Higher Seed Win Predictions: Offense vs. Defense](Visualizations/Higher_Seed_Win_Predictions_OffvDef.png)

**Takeaways**: Incorrect predictions (red dots) are interspersed among correct ones, indicating no clear pattern in mispredictions based on offensive-defensive rating differences. Some clustering suggests potential trends, but further data is required for confirmation.

![Higher Seed Win Predictions: Wins vs. PIE](Visualizations/Higher_Seed_Win_Predictions_WvPIE.png)

**Takeaways**: The model performs strongly when differences in wins and PIE are large, with incorrect predictions (red dots) clustering near the origin (small differences). This confirms that higher seeds with significant statistical advantages are more predictable winners.

## Conclusion
The NBA Playoff Predictor achieves robust playoff forecasts (~74% accuracy) using advanced stats from 1996–2024 and Monte Carlo simulations. Visualizations highlight the model’s strength in predicting higher seed wins with large performance gaps, while upset predictions remain less patterned. For technical details, see the [README](README.md) or `Run_Code` directory. Feedback is welcome!