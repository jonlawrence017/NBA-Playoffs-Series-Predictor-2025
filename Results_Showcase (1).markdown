# NBA Playoff Predictor: Results Showcase

## Overview
The NBA Playoff Predictor uses machine learning to forecast NBA playoff series outcomes. A TensorFlow neural network, trained on advanced team statistics (e.g., NetRtg, PIE, eFG%) from 2013–2024 seasons, predicts win probabilities for 2025 playoff matchups. Monte Carlo simulations further refine these predictions by modeling thousands of series outcomes. With a test accuracy of 73–74%, the model offers reliable insights into playoff dynamics. This document showcases key results and visualizations, complementing the technical details in the [README](README.md).

## Key Results
- **Model Performance**: The neural network (`NBA_Playoff_NN.h5`) achieved 73–74% accuracy on historical test data, successfully predicting 2025 playoff series outcomes.
- **2025 Predictions**: Series win probabilities for the 2025 playoffs are detailed in `first_round_probabilities_2025_fixed_bracket_series.csv` and visualized in `Visualizations/2025_Round_Percentages.png`.

## Visualizations
Below are key visualizations, created with Tableau and Python, to interpret the model’s predictions and identify patterns in playoff outcomes. Note: For metrics like PIE (Player Impact Estimate), see the [NBA Stats FAQ](https://www.nba.com/stats/help/faq).

### 1. 2025 Round Percentages
This visual illustrates each team’s probability of advancing past each round of the 2025 NBA playoffs, based on model predictions and Monte Carlo simulations.

![2025 Round Percentages](Visualizations/2025_Round_Percentages.png)

**Takeaways**: The chart highlights favorites and potential dark horses in the 2025 playoffs, with probabilities reflecting team strength and matchup dynamics.

### 2. Lower Seed Win Predictions (Upsets)
These scatter plots analyze the model’s success in predicting upsets (lower seed wins). Each dot represents a playoff series where the model predicted an upset (green = correct, red = incorrect). The plots explore patterns using four model features: 
- **T1vT2_Off-Def**: Team 1’s offensive rating minus Team 2’s defensive rating.
- **T2vT1_Off-Def**: Team 2’s offensive rating minus Team 1’s defensive rating.
- **T1-T2_W**: Difference in regular-season wins.
- **T1-T2_PIE**: Difference in Player Impact Estimate.

![Lower Seed Win Predictions: Offense vs. Defense](Visualizations/Lower_Seed_Win_Predictions_OffvDef.png)

**Takeaways**: The distribution of green and red dots appears fairly even, suggesting no clear pattern in upset predictions based on offensive-defensive rating differences. However, small clusters of green and red dots hint at potential localized trends, though insufficient data prevents firm conclusions.

![Lower Seed Win Predictions: Wins vs. PIE](Visualizations/Lower_Seed_Win_Predictions_WvPIE.png)

**Takeaways**: Similar to the OffvDef plot, the even spread of dots indicates no obvious pattern in upset predictions based on wins and PIE differences. Further analysis with more data could clarify any subtle trends.

### 3. Higher Seed Win Predictions (Non-Upsets)
These scatter plots evaluate the model’s success in predicting non-upsets (higher seed wins). Each dot represents a series where the model predicted a higher seed win (green = correct, red = incorrect). The same four features are analyzed to identify prediction patterns.

![Higher Seed Win Predictions: Offense vs. Defense](Visualizations/higher_Seed_Win_Predictions_OffvDef.png)

**Takeaways**: The red dots (incorrect predictions) are interspersed among green dots, indicating no distinct pattern in mispredictions based on offensive-defensive rating differences. Some clustering of red and green dots suggests possible regional trends, but more data is needed for confirmation.

![Higher Seed Win Predictions: Wins vs. PIE](Visualizations/higher_Seed_Win_Predictions_WvPIE.png)

**Takeaways**: The model excels when the difference in wins and PIE between teams is large, as red dots (incorrect predictions) cluster near the origin (small differences). This aligns with expectations: higher seeds with significant advantages in wins and PIE are more predictable winners.

## Conclusion
The NBA Playoff Predictor delivers accurate playoff forecasts (73–74% test accuracy) by leveraging advanced stats and simulations. Visualizations reveal the model’s strengths, particularly in predicting higher seed wins with large performance gaps, while upset predictions show less distinct patterns. Explore the [README](README.md) or `Run_Code` directory for technical details. Feedback is welcome!