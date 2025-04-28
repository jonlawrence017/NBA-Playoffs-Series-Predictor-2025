# NBA Playoff Predictor

This repository contains a machine learning pipeline to predict NBA playoff game and series outcomes for the 2024-2025 season using a neural network trained on advanced team statistics. The project includes data preprocessing, model training, Monte Carlo simulations for playoff bracket probabilities, a Tkinter-based GUI for predictions, and outputs for Tableau visualizations.

## Table of Contents
- [Purpose](#purpose)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Order of Operations](#order-of-operations)
- [Inputs and Outputs](#inputs-and-outputs)
- [License](#license)

## Purpose
The NBA Playoff Predictor forecasts NBA playoff game and series outcomes using a neural network trained on advanced team statistics (e.g., PIE, eFG%, NetRtg). Key features include:
- A Tkinter GUI for user-friendly game predictions.
- Monte Carlo simulations to estimate playoff bracket probabilities (first round, conference semifinals, finals, and champion).
- Data preprocessing to parse and clean historical (1996-2024) and current (2024-2025) NBA stats.
- Visualizations comparing lower and higher seed win predictions.
- Output tables for Tableau visualizations of playoff probabilities.

This project is ideal for sports analytics enthusiasts, data scientists, or anyone interested in applying machine learning to NBA data.

## Repository Structure
```
NBA-Playoffs_Series-Predictor-2025/
├── Data/
│   ├── Advanced_Stats_25.csv              # 2024-2025 team advanced stats (web scraped from nba.com)
│   ├── Advanced_Stats_25.pdf              # PDF version of 2024-2025 stats
│   ├── Advanced_Stats_96-24.csv           # Historical advanced stats (1996-2024, web scraped from nba.com)
│   ├── Advanced_Stats_96-24.pdf           # PDF version of historical stats
│   ├── Playoff_Outcomes.csv               # Historical playoff game outcomes (exported from Sports-Reference.com)
│   ├── master_playoff_advanced_stats.csv  # Processed historical playoff stats with winners/losers
│   └── parsed_playoff_outcomes.csv        # Parsed playoff outcomes
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
│   ├── (1a)Create_Master_DF.ipynb         # Creates master playoff dataset
│   ├── (1b)Parse_Advanced_Stats_25.ipynb  # Parses 2024-2025 advanced stats
│   ├── (2)Create_NN.ipynb                 # Trains neural network model and analyzes lower/higher seed winners
│   ├── (3a)Monte_Carlo.ipynb              # Runs Monte Carlo simulations
│   ├── (3b)Individual_Playoff_Matchups_GUI.ipynb                      # Launches prediction GUI
│   └── (4)Create_Tableau_Table.ipynb      # Generates Tableau-ready table
├── Visualizations/
│   ├── Lower_Seed_Win_Predictions_OffvDef.png  # Plot of lower seed win predictions (OffRtg vs. DefRtg)
│   ├── Lower_Seed_Win_Predictions_WvPIE.png   # Plot of lower seed win predictions (Wins vs. PIE)
│   ├── Round_Percentages.png                  # Plot of round-by-round prediction percentages
│   ├── higher_Seed_Win_Predictions_OffvDef.png # Plot of higher seed win predictions (OffRtg vs. DefRtg)
│   └── higher_Seed_Win_Predictions_WvPIE.png  # Plot of higher seed win predictions (Wins vs. PIE)
├── README.md
└── requirements.txt                       # Python package dependencies
```

## Prerequisites
- **Python Version**: 3.9.13
- **Packages**: The required packages are listed in `requirements.txt`:
  - matplotlib==3.9.4
  - matplotlib-inline==0.1.7
  - numpy==1.26.4
  - pandas==2.2.3
  - PyPDF2==3.0.1
  - scikit-learn==1.6.1
  - tensorflow==2.10.0
  - tensorflow-estimator==2.10.0
  - tensorflow-io-gcs-filesystem==0.31.0
- **Additional Dependency**: Tkinter (required for the GUI, typically included with Python but may need installation on some systems, e.g., `sudo apt-get install python3-tk` on Ubuntu).

To set up the environment:
1. Clone the repository:
   ```bash
   git clone https://github.com/jonlawrence017/NBA-Playoffs_Series-Predictor-2025.git
   cd NBA-Playoffs_Series-Predictor-2025
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
   If Tkinter is missing, install it (e.g., `sudo apt-get install python3-tk` on Ubuntu or equivalent for your system).

## Order of Operations
The notebooks in the `Run_Code/` folder are prefixed with numbers (1a, 1b, 2, etc.) indicating the recommended execution order:
1. **(1a)Create_Master_DF.ipynb**: Combines historical data to create the master playoff dataset.
2. **(1b)Parse_Advanced_Stats_25.ipynb**: Parses 2024-2025 advanced stats for predictions.
3. **(2)Create_NN.ipynb**: Trains the neural network model and saves it.
4. **(3a)Monte_Carlo.ipynb**: Runs Monte Carlo simulations for playoff probabilities.
5. **(3b)Individual_Playoff_Matchups_GUI.ipynb**: Launches the Tkinter GUI for game predictions.
6. **(4)Create_Tableau_Table.ipynb**: Generates a table for Tableau visualizations.

Run each notebook in order, ensuring all inputs are available. Execute notebooks using Jupyter:
```bash
jupyter notebook Run_Code/<notebook_name>.ipynb
```

## Inputs and Outputs
Below is a detailed breakdown of each notebook’s inputs and outputs.

### (1a)Create_Master_df.ipynb
- **Purpose**: Combines historical playoff outcomes and advanced stats to create a master dataset for training.
- **Inputs**:
  - `Data/Playoff_Outcomes.csv`: Historical playoff game outcomes (from Sports-Reference.com).
  - `Data/Advanced_Stats_96-24.pdf`: Historical advanced team stats (1996-2024, from nba.com).
- **Outputs**:
  - `Data/Advanced_Stats_96-24.csv`: parsed advanced team stats
  - `Data/master_playoff_advanced_stats.csv`: Master dataset with winner/loser stats and features.
  - `Data/parsed_playoff_outcomes.csv`: Parsed playoff outcomes for further processing.

### (1b)Parse_Advanced_Stats_25.ipynb
- **Purpose**: Parses 2024-2025 advanced stats from CSV or PDF for predictions.
- **Inputs**:
  - `Data/Advanced_Stats_25.pdf`: 2024-2025 team advanced stats (web scraped from nba.com).
- **Outputs**:
  - `Data/Advanced_Stats_25.csv`: parsed 2024-2025 team advanced stats

### (2)Create_NN.ipynb
- **Purpose**: Trains a neural network to predict playoff game outcomes and analyzes lower vs. higher seed winners.
- **Inputs**:
  - `Data/master_playoff_advanced_stats.csv`: Master dataset for training.
- **Outputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained neural network model.
  - `Models/scaler.pkl`: StandardScaler for feature normalization.
  - `Visualizations/Lower_Seed_Win_Predictions_OffvDef.png`: Scatter plot of lower seed win predictions (OffRtg vs. DefRtg).
  - `Visualizations/Lower_Seed_Win_Predictions_WvPIE.png`: Scatter plot of lower seed win predictions (Wins vs. PIE).
  - `Visualizations/higher_Seed_Win_Predictions_OffvDef.png`: Scatter plot of higher seed win predictions (OffRtg vs. DefRtg).
  - `Visualizations/higher_Seed_Win_Predictions_WvPIE.png`: Scatter plot of higher seed win predictions (Wins vs. PIE).

### (3a)Monte_Carlo.ipynb
- **Purpose**: Runs Monte Carlo simulations to estimate playoff bracket probabilities.
- **Inputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained neural network model.
  - `Models/scaler.pkl`: StandardScaler for feature normalization.
  - `Data/Advanced_Stats_25.csv`: 2024-2025 team stats for predictions.
- **Outputs**:
  - `Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv`: First-round series probabilities.
  - `Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv`: Conference semifinals probabilities.
  - `Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv`: Conference finals probabilities.
  - `Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv`: Champion probabilities.

### (3b)Individual_Playoff_Matchups_GUI.ipynb
- **Purpose**: Launches a Tkinter GUI for users to select teams and view game predictions.
- **Inputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained neural network model.
  - `Models/scaler.pkl`: StandardScaler for feature normalization.
  - `Data/Advanced_Stats_25.csv`: 2024-2025 team stats for predictions.
- **Outputs**:
  - Interactive GUI displaying predicted winner and win probability (no file output).

### (4)Create_Tableau_Table.ipynb
- **Purpose**: Generates a table of playoff probabilities for Tableau visualizations.
- **Inputs**:
  - `Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv`
- **Outputs**:
  - `Monte_Carlo_Output/tableau_nba_playoff_probs_2025.csv`: Tableau-ready table of probabilities.
