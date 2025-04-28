# NBA Playoff Predictor
This repository contains a machine learning pipeline to predict NBA playoff game outcomes using a neural network trained on advanced team statistics. The project includes data preprocessing, model training, Monte Carlo simulations for playoff bracket probabilities, a Tkinter-based GUI for predictions, and a table for Tableau visualizations.

# Table of Contents
(i) Purpose
(ii) Repository Structure
(iii) Prerequisites
(iv) Order of Operations
(v) Inputs and Outputs

# (i) Purpose
The NBA Playoff Predictor aims to forecast the outcomes of NBA playoff games and series for the 2024-2025 season. It leverages a neural network trained on historical and current advanced team statistics (e.g., PIE, eFG%, NetRtg) to predict game winners and probabilities. Key features include:

A Tkinter GUI for user-friendly game predictions.
Monte Carlo simulations to estimate playoff bracket probabilities (e.g., first round, conference semifinals, finals, and champion).
Data preprocessing to parse and clean historical and current NBA stats.
Output tables for Tableau visualizations of playoff probabilities.

This project is ideal for sports analytics enthusiasts, data scientists, or anyone interested in applying machine learning to NBA data.

# (ii) Repository Structure
nba-playoff-predictor/
├── Data/
│   ├── Advanced_Stats_25.csv              # 2024-2025 team advanced stats
│   ├── Advanced_Stats_25.pdf              # PDF version of 2024-2025 stats from (web scraped from nba.com)
│   ├── Advanced_Stats_96-24.csv           # Historical advanced stats (1996-2024)
│   ├── Advanced_Stats_96-24.pdf           # web scraped PDF version of historical stats (web scraped from nba.com)
│   ├── Folder_Description                 # Metadata/description (optional)
│   ├── Playoff_Outcomes.csv               # Historical playoff game outcomes (exported from Sports-Reference.com)
│   ├── master_playoff_advanced_stats.csv  # Processed historical playoff stats with winners/losers
│   └── parsed_playoff_outcomes.csv        # Parsed playoff outcomes
├── Models/
│   ├── Folder_Description                 # Metadata/description (optional)
│   ├── NBA_Playoff_NN.h5                  # Trained neural network model
│   └── scaler.pkl                         # StandardScaler for feature normalization
├── Monte_Carlo_Output/
│   ├── Folder_Description                 # Metadata/description (optional)
│   ├── champion_probabilities_2025_fixed_bracket_series.csv  # Champion probabilities
│   ├── conf_finals_probabilities_2025_fixed_bracket_series.csv  # Conference finals probabilities
│   ├── conf_semi_probabilities_2025_fixed_bracket_series.csv    # Conference semifinals probabilities
│   ├── first_round_probabilities_2025_fixed_bracket_series.csv  # First-round probabilities
│   └── tableau_nba_playoff_probs_2025.csv  # Tableau-ready probability table
├── Run_Code/
│   ├── (1a)Create_Master_df.ipynb         # Creates master playoff dataset
│   ├── (1b)Parse_Advanced_Stats_25.ipynb  # Parses 2024-2025 advanced stats
│   ├── (2)Create_NN.ipynb                 # Trains neural network model and analyzes lower and higher seed winners seperately
│   ├── (3a)Monte_Carlo.ipynb              # Runs Monte Carlo simulations
│   ├── (3b)GUI.ipynb                      # Launches prediction GUI
│   ├── (4)Create_Tableau_Table.ipynb      # Generates Tableau-ready table
│   └── Folder_Description                 # Metadata/description (optional)
├── Visualizations/                        # Empty; for user-generated plots
└── README.md

# (iii) Prerequisites
Python Version: 3.9.13
Packages: 
  matplotlib==3.9.4
  matplotlib-inline==0.1.7
  numpy==1.26.4
  pandas==2.2.3
  PyPDF2==3.0.1
  scikit-learn==1.6.1
  tensorflow==2.10.0
  tensorflow-estimator==2.10.0
  tensorflow-io-gcs-filesystem==0.31.0



To set up the environment:

(a) Clone the repository:
git clone https://github.com/jonlawrence017/NBA-Playoffs_Series-Predictor-2025.git
cd NBA-Playoffs_Series-Predictor-2025

(b) Create and activate a virtual environment:
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

(c) Install dependencies: 
pip install -r requirements.txt
note: be sure to download requirements.txt from this ... to you working directory


# (iv) Order of Operations
The notebooks in the Run_Code/ folder are prefixed with numbers (1a, 1b, 2, etc.) indicating the recommended execution order. Below is the sequence:

(1a)Create_Master_df.ipynb: Combines historical data to create the master playoff dataset.
(1b)Parse_Advanced_Stats_25.ipynb: Parses 2024-2025 advanced stats for predictions.
(2)Create_NN.ipynb: Trains the neural network model and saves it.
(3a)Monte_Carlo.ipynb: Runs Monte Carlo simulations for playoff probabilities.
(3b)GUI.ipynb: Launches the Tkinter GUI for game predictions.
(4)Create_Tableau_Table.ipynb: Generates


Run each notebook in order, ensuring all inputs are available. Notebooks can be executed using Jupyter:
jupyter notebook Run_Code/<notebook_name>.ipynb

# (v) Inputs and Outputs
Below is a detailed breakdown of each notebook’s inputs and outputs.
**(1a)Create_Master_df.ipynbb**

Purpose: Combines historical playoff outcomes and advanced stats to create a master dataset for training.
Inputs:
Data/Playoff_Outcomes.csv: Historical playoff game outcomes.
Data/Advanced_Stats_96-24.csv: Historical advanced team stats (1996-2024).


Outputs:
Data/master_playoff_advanced_stats.csv: Master dataset with winner/loser stats and features.
Data/parsed_playoff_outcomes.csv: Parsed playoff outcomes for further processing.


Notes: Uses pandas for data merging and cleaning.

**(1b)Parse_Advanced_Stats_25.ipynb**

Purpose: Parses 2024-2025 advanced stats from CSV or PDF for use in predictions.
Inputs:
Data/Advanced_Stats_25.csv: 2024-2025 team advanced stats.
Data/Advanced_Stats_25.pdf: PDF version (optional, used if CSV is unavailable).


Outputs:
Cleaned 2024-2025 stats (may be saved as intermediate CSV or used in memory).


Notes: Uses PyPDF2 for PDF parsing and pandas for data cleaning.

**(2)Create_NN.ipynb**

Purpose: Trains a neural network to predict playoff game outcomes.
Inputs:
Data/master_playoff_advanced_stats.csv: Master dataset for training.


Outputs:
Models/NBA_Playoff_NN.h5: Trained neural network model.
Models/scaler.pkl: StandardScaler for feature normalization.
Visualizations (optional, saved to Visualizations/ if enabled): Scatter plots of features (e.g., T1-T2_W vs. T1-T2_PIE).


Notes: Uses tensorflow for model training with 5-fold cross-validation, L2 regularization, and dropout.

**(3a)Monte_Carlo.ipynb**

Purpose: Runs Monte Carlo simulations to estimate playoff bracket probabilities.
Inputs:
Models/NBA_Playoff_NN.h5: Trained neural network model.
Models/scaler.pkl: StandardScaler for feature normalization.
Data/Advanced_Stats_25.csv: 2024-2025 team stats for predictions.


Outputs:
Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv: First-round series probabilities.
Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv: Conference semifinals probabilities.
Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv: Conference finals probabilities.
Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv: Champion probabilities.


Notes: Simulates multiple playoff scenarios using the trained model.

**(3b)GUI.ipynb**

Purpose: Launches a Tkinter GUI for users to select teams and view game predictions.
Inputs:
Models/NBA_Playoff_NN.h5: Trained neural network model.
Models/scaler.pkl: StandardScaler for feature normalization.
Data/Advanced_Stats_25.csv: 2024-2025 team stats for predictions.


Outputs:
Interactive GUI displaying predicted winner and win probability (no file output).


Notes: Uses tkinter for the GUI and pandas for data handling.

**(4)Create_Tableau_Table.ipynb**

Purpose: Generates a table of playoff probabilities for Tableau visualizations.
Inputs:
Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv
Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv
Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv
Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv


Outputs:
Monte_Carlo_Output/tableau_nba_playoff_probs_2025.csv: Tableau-ready table of probabilities.


Notes: Aggregates Monte Carlo outputs for visualization.


