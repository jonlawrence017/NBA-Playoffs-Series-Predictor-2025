# NBA Playoff Predictor
This repository contains a machine learning pipeline to predict NBA playoff game and series outcomes for the 2024-2025 season using a neural network. I built this project to combine my love for NBA basketball and data science, showcasing my skills in Python, machine learning, and visualization. Note: Datasets are not included due to restrictions from NBA.com and Sports-Reference.com; my method for obtaining them is below.

## Table of Contents
- [Purpose](#purpose)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Feature Selection](#feature-selection)
- [Jupyter Notebooks](#jupyter-notebooks)
- [Data Sources](#data-sources)
- [Visualizations](#visualizations)
- [Results](#results)
- [Usage](#usage)

## Purpose
The NBA Playoff Predictor forecasts NBA playoff series outcomes using a neural network trained on advanced team statistics. Key features include:
- A Tkinter GUI for easy series predictions.
- Monte Carlo simulations to estimate playoff bracket probabilities (first round, conference semifinals, finals, and champion).
- Data preprocessing to clean and structure historical (1996-2024) and current (2024-2025) NBA stats.
- Visualizations comparing lower and higher seed win predictions and statistical relationships to analyze model performance.
- Output tables for Tableau visualizations of playoff probabilities.

## Repository Structure
```
NBA-Playoffs-Series-Predictor-2025/
├── Models/
│   ├── NBA_Playoff_NN.h5                  # Trained neural network model
│   └── scaler.pkl                         # StandardScaler for feature normalization
├── Monte_Carlo_Output/
│   ├── champion_probabilities_2025_fixed_bracket_series.csv  # Champion probabilities
│   ├── conf_finals_probabilities_2025_fixed_bracket_series.csv  # Conference finals probabilities
│   ├── conf_semi_probabilities_2025_fixed_bracket_series.csv    # Conference semifinals probabilities
│   ├── first_round_probabilities_2025_fixed_bracket_series.csv  # First-round probabilities
│   └── tableau_nba_playoff_probs_2025.csv  # Tableau-ready probability table
├── Run_Code/
│   ├── Statistical_Analysis.ipynb       # Analyzes correlations for feature selection
│   ├── Create_Master_DF.ipynb         # Preprocesses historical data
│   ├── Parse_Advanced_Stats_25.ipynb  # Preprocesses 2024-2025 stats
│   ├── Create_NN.ipynb                 # Trains neural network and generates visualizations
│   ├── Monte_Carlo.ipynb              # Runs Monte Carlo simulations
│   ├── Individual_Playoff_Matchups_GUI.ipynb  # Launches prediction GUI
│   └── Create_Tableau_Table.ipynb      # Generates Tableau-ready table
├── Visualizations/
│   ├── Lower_Seed_Win_Predictions_OffvDef.png  # Lower seed win predictions (Offensive vs. Defensive Rating)
│   ├── Lower_Seed_Win_Predictions_WvPIE.png   # Lower seed win predictions (Wins vs. PIE)
│   ├── PIE_vs_series_margin.png               # PIE difference vs. series margin
│   ├── Round_Percentages.png                  # Round-by-round prediction percentages
│   ├── higher_Seed_Win_Predictions_OffvDef.png # Higher seed win predictions (Offensive vs. Defensive Rating)
│   ├── higher_Seed_Win_Predictions_WvPIE.png  # Higher seed win predictions (Wins vs. PIE)
│   └── net     # NetRtg difference vs. series margin
├── README.md
└── requirements.txt                       # Python package dependencies
```

## Prerequisites
- **Python Version**: 3.9.13
- **Packages**: Listed in `requirements.txt`:
  - matplotlib==3.9.4
  - matplotlib-inline==0.1.7
  - numpy==1.26.4
  - pandas==2.2.3
  - PyPDF2==3.0.1
  - scikit-learn==1.6.1
  - tensorflow==2.10.0
  - tensorflow-estimator==2.10.0
  - tensorflow-io-gcs-filesystem==0.31.0
- **Additional Dependency**: Tkinter (required for the GUI, typically included with Python). If missing, install it:
  - Ubuntu: `sudo apt-get install python3-tk`
  - macOS: Usually pre-installed; if not, install via `brew install python-tk`
  - Windows: Included with Python installer; reinstall Python if missing.

To set up the environment:
1. Clone the repository:
   ```bash
   git clone https://github.com/jonlawrence017/NBA-Playoffs-Series-Predictor-2025.git
   cd NBA-Playoffs-Series-Predictor-2025
   ```
2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Verify Tkinter availability:
   ```bash
   python -c "import tkinter"
   ```
   If the import fails, install Tkinter as described above.

## Feature Selection
The features for the neural network were selected through statistical analysis conducted in `(0)Statistical_Analysis.ipynb`. This analysis examined correlations, statistical significance, and win percentages for various team statistics against playoff series outcomes (Winner_Wins and Series_Margin) from 1996-2024. The process involved:
- **Correlation Analysis**: Pearson correlation coefficients were calculated for each statistic (e.g., NetRtg, PIE, eFG%) against Winner_Wins and Series_Margin. For Series_Margin, NetRtg showed the highest correlation (r = 0.2543, p < 0.0001), followed by eFG% (r = 0.2293, p < 0.0001) and PIE (r = 0.2274, p < 0.0001), indicating strong predictive power.
- **Statistical Significance**: Features with p-values < 0.05 were prioritized to ensure statistical reliability. For Series_Margin, 12 features (e.g., NetRtg, PIE, eFG%, Seed) were significant.
- **Win Percentage Analysis**: The percentage of series won by teams with higher values of each statistic was computed. NetRtg led with 73.66% of series won by the team with the higher value, followed by PIE (73.17%) and Wins (72.44%).
- **Feature Selection Outcome**: Based on high correlations, statistical significance, and win percentages, the key features selected for the neural network included NetRtg, PIE, eFG%, OffRtg, DefRtg, Wins, Losses, and Seed. These features capture offensive and defensive efficiency, overall team performance, and playoff seeding, which are critical for predicting series outcomes.

This rigorous statistical approach ensured that the neural network was trained on the most relevant and impactful features, enhancing its predictive accuracy.

## Jupyter Notebooks

Below is a detailed breakdown of each notebook’s inputs and outputs. Note: All input datasets must be obtained manually (see [Data Sources](#data-sources)).

### Statistical_Analysis.ipynb
- **Purpose**: Analyzes correlations and win percentages to select neural network features.
- **Inputs**:
  - `Data/Master_DF.csv`: Master dataset with historical playoff data.
- **Outputs**:
  - `Visualizations/netrtg_vs_series_margin.png`: Scatter plot of NetRtg difference vs. series margin.
  - `Visualizations/PIE_vs_series_margin.png`: Scatter plot of PIE difference vs. series margin.

### Create_Master_DF.ipynb
- **Purpose**: Preprocesses historical playoff outcomes and advanced stats.
- **Inputs**:
  - `Data/Playoff_Outcomes.csv`: Historical playoff game outcomes (exported from Basketball-Reference.com).
  - `Data/Advanced_Stats_96-24.pdf`: Historical advanced team stats (1996-2024, manually copied from NBA.com).
- **Outputs**:
  - `Data/Advanced_Stats_96-24.csv`: Parsed historical stats.
  - `Data/Master_DF.csv`: Master dataset with features.
  - `Data/Parsed_Playoff_Outcomes.csv`: Parsed playoff outcomes.

### Parse_Advanced_Stats_25.ipynb
- **Purpose**: Preprocesses 2024-2025 advanced stats.
- **Inputs**:
  - `Data/Advanced_Stats_25.pdf`: 2024-2025 team advanced stats (manually copied from NBA.com).
- **Outputs**:
  - `Data/Advanced_Stats_25.csv`: Parsed 2024-2025 stats.

### Create_NN.ipynb
- **Purpose**: Trains a neural network and generates visualizations.
- **Inputs**:
  - `Data/Master_DF.csv`: Master dataset for training.
- **Outputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained neural network model.
  - `Models/scaler.pkl`: StandardScaler for feature normalization.
  - `Visualizations/Lower_Seed_Win_Predictions_OffvDef.png`: Scatter plot (Offensive vs. Defensive Rating).
  - `Visualizations/Lower_Seed_Win_Predictions_WvPIE.png`: Scatter plot (Wins vs. PIE).
  - `Visualizations/Round_Percentages.png`: Bar plot of prediction percentages.
  - `Visualizations/higher_Seed_Win_Predictions_OffvDef.png`: Scatter plot (Offensive vs. Defensive Rating).
  - `Visualizations/higher_Seed_Win_Predictions_WvPIE.png`: Scatter plot (Wins vs. PIE).

### Monte_Carlo.ipynb
- **Purpose**: Runs Monte Carlo simulations for playoff probabilities.
- **Inputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained model.
  - `Models/scaler.pkl`: StandardScaler.
  - `Data/Advanced_Stats_25.csv`: 2024-2025 stats.
- **Outputs**:
  - `Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv`: First-round probabilities.
  - `Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv`: Conference semifinals probabilities.
  - `Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv`: Conference finals probabilities.
  - `Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv`: Champion probabilities.

### Individual_Playoff_Matchups_GUI.ipynb
- **Purpose**: Launches a Tkinter GUI for predictions.
- **Inputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained model.
  - `Models/scaler.pkl`: StandardScaler.
  - `Data/Advanced_Stats_25.csv`: 2024-2025 stats.
- **Outputs**:
  - Interactive GUI displaying predicted winner and probability (no file output).

### Create_Tableau_Table.ipynb
- **Purpose**: Generates a table for Tableau visualizations.
- **Inputs**:
  - `Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv`
- **Outputs**:
  - `Monte_Carlo_Output/tableau_nba_playoff_probs_2025.csv`: Tableau-ready table.

## Data Sources
Datasets are not included due to restrictions from NBA.com and Sports-Reference.com. To replicate the project, you must obtain the following datasets manually:
- **Advanced_Stats_25.pdf**: 2024-2025 team advanced stats. Copy and paste data from [NBA.com/stats](https://www.nba.com/stats) into a PDF or CSV, following their rules (stats are for viewing only, not downloading).
- **Advanced_Stats_96-24.pdf**: Historical advanced team stats (1996-2024). Copy and paste data from [NBA.com/stats](https://www.nba.com/stats) into a PDF or CSV, following their rules.
- **Playoff_Outcomes.csv**: Historical playoff game outcomes (1996-2024). Export manually from [Basketball-Reference.com](https://www.basketball-reference.com) using the “Share & Export” feature, following their Terms of Service.
- **Note**: Do not share the datasets or any files created from them publicly, as this violates NBA.com and Sports-Reference.com’s rules. Use datasets only for private analysis and follow all terms.

## Visualizations
The project includes several visualizations to analyze model performance and statistical relationships, stored in the `Visualizations/` folder. These are safe to share and include:
- **Lower_Seed_Win_Predictions_OffvDef.png**: Scatter plot of lower seed win predictions based on Offensive vs. Defensive Rating.
- **Lower_Seed_Win_Predictions_WvPIE.png**: Scatter plot of lower seed win predictions based on Wins vs. PIE.
- **PIE_vs_series_margin.png**: Scatter plot showing the relationship between PIE difference and series margin.
- **Round_Percentages.png**: Bar plot of prediction percentages across playoff rounds.
- **higher_Seed_Win_Predictions_OffvDef.png**: Scatter plot of higher seed win predictions based on Offensive vs. Defensive Rating.
- **higher_Seed_Win_Predictions_WvPIE.png**: Scatter plot of higher seed win predictions based on Wins vs. PIE.
- **netrtg_vs_series_margin.png**: Scatter plot showing the relationship between NetRtg difference and series margin.

These visualizations provide insights into the model’s predictive accuracy and the impact of key statistics on playoff outcomes.

## Results
The neural network, trained on features such as NetRtg, PIE, eFG%, OffRtg, DefRtg, Wins, Losses, and Seed, achieved a testing accuracy of approximately 73-74% in predicting NBA playoff series outcomes. This performance demonstrates the model’s ability to capture key statistical relationships in historical data (1996-2024) and apply them to the 2024-2025 season. However, there is room for improvement. Future work includes:
- **Increasing Model Complexity**: Enhancing the neural network architecture, such as adding more layers or experimenting with different activation functions, to capture more nuanced patterns in the data.
- **Incorporating Additional Features**: Including player availability data (e.g., injuries, minutes played by key players) to account for individual contributions and team dynamics, which could improve prediction accuracy.
- **Further Validation**: Conducting additional testing, such as expanding the dataset or using alternative evaluation metrics, to ensure robustness.

These enhancements aim to push the model’s accuracy higher and make it a more reliable tool for playoff predictions.

## Usage
This project is a portfolio piece to demonstrate my data science skills and is not for commercial use. Please contact me at jonlawrence00@gmail.com for permission to use, modify, or share the code. To replicate the project, obtain the datasets as described in [Data Sources](#data-sources) and follow the [Order of Operations](#order-of-operations). Do not share any datasets or files derived from NBA.com or Sports-Reference.com without their explicit permission.
