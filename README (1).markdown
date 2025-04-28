# NBA Playoff Predictor

This repository contains a machine learning pipeline to predict NBA playoff game and series outcomes for the 2024-2025 season using a neural network. The project includes data preprocessing, model training, Monte Carlo simulations for playoff bracket probabilities, a Tkinter-based GUI for predictions, and outputs for Tableau visualizations. Note: Datasets are not included due to licensing restrictions from NBA.com and Sports-Reference.com; instructions for obtaining them are provided below.

## Table of Contents
- [Purpose](#purpose)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Order of Operations](#order-of-operations)
- [Inputs and Outputs](#inputs-and-outputs)
- [Data Sources](#data-sources)
- [Usage](#usage)

## Purpose
The NBA Playoff Predictor forecasts NBA playoff game and series outcomes using a neural network trained on advanced team statistics. Key features include:
- A Tkinter GUI for user-friendly game predictions.
- Monte Carlo simulations to estimate playoff bracket probabilities (first round, conference semifinals, finals, and champion).
- Data preprocessing to clean and structure historical (1996-2024) and current (2024-2025) NBA stats.
- Visualizations comparing lower and higher seed win predictions to analyze model performance.
- Output tables for Tableau visualizations of playoff probabilities.

This project is ideal for sports analytics enthusiasts, data scientists, or anyone interested in applying machine learning to NBA data.

## Repository Structure
```
NBA-Playoffs_Series-Predictor-2025/
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
│   ├── (1a)Create_Master_DF.ipynb         # Preprocesses historical data
│   ├── (1b)Parse_Advanced_Stats_25.ipynb  # Preprocesses 2024-2025 stats
│   ├── (2)Create_NN.ipynb                 # Trains neural network and generates visualizations
│   ├── (3a)Monte_Carlo.ipynb              # Runs Monte Carlo simulations
│   ├── (3b)Individual_Playoff_Matchups_GUI.ipynb  # Launches prediction GUI
│   └── (4)Create_Tableau_Table.ipynb      # Generates Tableau-ready table
├── Visualizations/
│   ├── Lower_Seed_Win_Predictions_OffvDef.png  # Lower seed win predictions (Offensive vs. Defensive Rating)
│   ├── Lower_Seed_Win_Predictions_WvPIE.png   # Lower seed win predictions (Wins vs. PIE)
│   ├── Round_Percentages.png                  # Round-by-round prediction percentages
│   ├── higher_Seed_Win_Predictions_OffvDef.png # Higher seed win predictions (Offensive vs. Defensive Rating)
│   └── higher_Seed_Win_Predictions_WvPIE.png  # Higher seed win predictions (Wins vs. PIE)
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
   If the import fails, install Tkinter as described above.

## Order of Operations
The notebooks in the `Run_Code/` folder are prefixed with numbers (1a, 1b, 2, etc.) indicating the recommended execution order:
1. **(1a)Create_Master_DF.ipynb**: Preprocesses historical data to create a master dataset.
2. **(1b)Parse_Advanced_Stats_25.ipynb**: Preprocesses 2024-2025 stats for predictions.
3. **(2)Create_NN.ipynb**: Trains the neural network and generates visualizations.
4. **(3a)Monte_Carlo.ipynb**: Runs Monte Carlo simulations for playoff probabilities.
5. **(3b)Individual_Playoff_Matchups_GUI.ipynb**: Launches the Tkinter GUI for predictions.
6. **(4)Create_Tableau_Table.ipynb**: Generates a table for Tableau visualizations.

Run each notebook in order, ensuring all inputs are available. Execute notebooks using Jupyter:
```bash
jupyter notebook Run_Code/<notebook_name>.ipynb
```

## Inputs and Outputs
Below is a detailed breakdown of each notebook’s inputs and outputs. Note: All input datasets must be obtained manually (see [Data Sources](#data-sources)).

### (1a)Create_Master_DF.ipynb
- **Purpose**: Preprocesses historical playoff outcomes and advanced stats.
- **Inputs**:
  - `Data/Playoff_Outcomes.csv`: Historical playoff game outcomes (exported from Basketball-Reference.com).
  - `Data/Advanced_Stats_96-24.pdf`: Historical advanced team stats (1996-2024, manually copied from NBA.com).
- **Outputs**:
  - `Data/Advanced_Stats_96-24.csv`: Parsed historical stats.
  - `Data/master_playoff_advanced_stats.csv`: Master dataset with features.
  - `Data/parsed_playoff_outcomes.csv`: Parsed playoff outcomes.
- **Notes**: Uses `PyPDF2` for PDF parsing and `pandas` for data processing. Do not share output datasets publicly.

### (1b)Parse_Advanced_Stats_25.ipynb
- **Purpose**: Preprocesses 2024-2025 advanced stats.
- **Inputs**:
  - `Data/Advanced_Stats_25.pdf`: 2024-2025 team advanced stats (manually copied from NBA.com).
- **Outputs**:
  - `Data/Advanced_Stats_25.csv`: Parsed 2024-2025 stats.
- **Notes**: Uses `PyPDF2` for PDF parsing and `pandas` for data cleaning. Do not share output datasets publicly.

### (2)Create_NN.ipynb
- **Purpose**: Trains a neural network and generates visualizations.
- **Inputs**:
  - `Data/master_playoff_advanced_stats.csv`: Master dataset for training.
- **Outputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained neural network model.
  - `Models/scaler.pkl`: StandardScaler for feature normalization.
  - `Visualizations/Lower_Seed_Win_Predictions_OffvDef.png`: Scatter plot (Offensive vs. Defensive Rating).
  - `Visualizations/Lower_Seed_Win_Predictions_WvPIE.png`: Scatter plot (Wins vs. PIE).
  - `Visualizations/Round_Percentages.png`: Bar plot of prediction percentages.
  - `Visualizations/higher_Seed_Win_Predictions_OffvDef.png`: Scatter plot (Offensive vs. Defensive Rating).
  - `Visualizations/higher_Seed_Win_Predictions_WvPIE.png`: Scatter plot (Wins vs. PIE).
- **Notes**: Uses `tensorflow` for training with 5-fold cross-validation. Visualizations are safe to share.

### (3a)Monte_Carlo.ipynb
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
- **Notes**: Outputs are safe to share, as they are model-generated probabilities.

### (3b)Individual_Playoff_Matchups_GUI.ipynb
- **Purpose**: Launches a Tkinter GUI for predictions.
- **Inputs**:
  - `Models/NBA_Playoff_NN.h5`: Trained model.
  - `Models/scaler.pkl`: StandardScaler.
  - `Data/Advanced_Stats_25.csv`: 2024-2025 stats.
- **Outputs**:
  - Interactive GUI displaying predicted winner and probability (no file output).
- **Notes**: Uses `tkinter` for the GUI and `pandas` for data handling.

### (4)Create_Tableau_Table.ipynb
- **Purpose**: Generates a table for Tableau visualizations.
- **Inputs**:
  - `Monte_Carlo_Output/first_round_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_semi_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/conf_finals_probabilities_2025_fixed_bracket_series.csv`
  - `Monte_Carlo_Output/champion_probabilities_2025_fixed_bracket_series.csv`
- **Outputs**:
  - `Monte_Carlo_Output/tableau_nba_playoff_probs_2025.csv`: Tableau-ready table.
- **Notes**: Output is safe to share, as it aggregates model-generated probabilities.

## Data Sources
Datasets are not included due to licensing restrictions from NBA.com and Sports-Reference.com. Users must obtain the following datasets manually:
- **Advanced_Stats_25.pdf**: 2024-2025 team advanced stats. Manually copy and paste data from [NBA.com/stats](https://www.nba.com/stats) into a PDF or CSV, ensuring compliance with their Terms of Use and FAQ (stats are for viewing only, not downloading).
- **Advanced_Stats_96-24.pdf**: Historical advanced team stats (1996-2024). Manually copy and paste data from [NBA.com/stats](https://www.nba.com/stats) into a PDF or CSV, ensuring compliance with their Terms of Use and FAQ.
- **Playoff_Outcomes.csv**: Historical playoff game outcomes (1996-2024). Export manually from [Basketball-Reference.com](https://www.basketball-reference.com) using the “Share & Export” feature, ensuring compliance with their Terms of Service.
- **Attribution**: Always credit the sources (e.g., “Data sourced from NBA.com” and “Data provided by Basketball-Reference.com”).
- **Note**: Do not share the obtained datasets or their processed outputs (e.g., `master_playoff_advanced_stats.csv`, `parsed_playoff_outcomes.csv`) publicly, as this violates the data owners’ policies. Use datasets only for private analysis, ensuring compliance with all terms.

## Usage
This project is shared for demonstration purposes as part of my portfolio. Please contact me at [your-email] for permission to use, modify, or distribute the code. To replicate the project, obtain the required datasets as described in [Data Sources](#data-sources) and follow the [Order of Operations](#order-of-operations). Do not share any datasets or processed outputs derived from NBA.com or Sports-Reference.com without explicit permission from the respective owners.