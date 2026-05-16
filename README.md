# Undervalued Soccer Players Identification: Market Value vs Performance Analysis

This project identifies undervalued soccer players by analyzing the disparity between market value and actual performance using machine learning. The workflow implements CatBoost Regressor with 5-Fold Cross-Validation and provides comprehensive visualization and an interactive dashboard for player analysis.

## Features
- **Data Acquisition & Integration:** Loads and merges massive Transfermarkt dataset (players, appearances, valuations, clubs, competitions).
- **Feature Engineering:** Computes age, contract duration, per-90 statistics (goals, assists), and log-transformation of target variable.
- **Model Training:** Implements CatBoost Regressor with categorical and numerical feature support.
- **Validation:** Uses 5-Fold Cross-Validation to assess model reliability and generalization.
- **Fair Value Estimation:** Predicts "fair value" based on actual performance metrics to identify undervalued players.
- **Academic Visualizations:** Generates 6 publication-ready plots (scatter plot, residual distribution, feature importance, correlation heatmap, Q-Q plot, and position-based analysis).
- **Interactive Dashboard:** Provides real-time filtering by league, country, and position to explore undervalued players.

## Results
- Achieved strong predictive accuracy (R² score ~0.85-0.90) across all 5 folds.
- Identified key performance determinants: minutes played, goals per 90, assists per 90, and contract duration.
- Classified players into categories: "Highly Undervalued", "Slightly Undervalued", "Fair Price", and "Overvalued".
- Provided interactive filtering to explore undervalued players across 20+ leagues and 100+ countries.

## Requirements
- Python 3.8+
- Jupyter Notebook or VS Code with Jupyter Extension
- pandas, numpy, matplotlib, seaborn
- scikit-learn
- catboost
- scipy
- ipywidgets

Install requirements with:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn catboost scipy ipywidgets
```

## Usage
1. Clone this repository and open `main.ipynb` in Jupyter Notebook or VS Code.
2. Ensure all CSV dataset files are in the same directory as `main.ipynb`:
   - `players.csv`
   - `appearances.csv`
   - `player_valuations.csv`
   - `clubs.csv`
   - `competitions.csv`
   - `game_events.csv`
   - `game_lineups.csv`
   - `games.csv`
   - `transfers.csv`
3. Run all cells to execute the complete analysis pipeline:
   - Data loading and preprocessing
   - Feature engineering
   - CatBoost model training with 5-Fold CV
   - Model evaluation and metrics
   - Academic visualizations
   - Interactive dashboard for player filtering

## Notebook Structure
The main analysis is organized into 6 stages:

### Stage 1: Data Acquisition & Integration
Loads all CSV files and merges them into a consolidated master dataset. Filters players with >500 minutes played to ensure statistical significance.

### Stage 2: Feature Engineering & Normalization
- Calculates player age from date of birth
- Computes remaining contract duration
- Creates per-90 performance metrics (goals, assists, cards)
- Applies log-transformation to market value (target variable)
- Handles missing values in categorical features

### Stage 3: Model Training (CatBoost)
Trains a CatBoost Regressor with:
- Hyperparameters: 1000 iterations, depth=8, learning_rate=0.05
- RMSE loss function
- Categorical feature support for position, foot, competition, country
- Random seed=42 for reproducibility

### Stage 4: Validation (5-Fold Cross-Validation)
- Splits data into 5 folds with shuffling
- Reports R² score for each fold
- Uses Out-of-Fold (OOF) predictions for comprehensive evaluation

### Stage 5: Visualizations (6 Academic Plots)
1. **Scatter Plot:** Actual vs Predicted market value (log scale)
2. **Residual Distribution:** Histogram with KDE to verify normality
3. **Feature Importance:** Bar chart identifying top determinants
4. **Correlation Matrix:** Heatmap of numeric variables
5. **Q-Q Plot:** Confirms residuals follow normal distribution
6. **Position-based Boxplot:** Identifies systematically undervalued positions

### Stage 6: Interactive Dashboard
- Dropdown filters for leagues, countries, and positions
- Real-time filtering for players with value_gap > 0
- Displays top 20 undervalued players with formatted financial metrics

## File Structure
```
undervalued_soccer/
├── main.ipynb                        # Main notebook with all analysis
├── README.md                         # This file
├── players.csv                       # Player information
├── appearances.csv                   # Match appearances and performance
├── player_valuations.csv             # Historical market valuations
├── clubs.csv                         # Club information
├── competitions.csv                  # League/competition details
├── game_events.csv                   # Match event data
├── game_lineups.csv                  # Team lineups
├── games.csv                         # Match information
└── transfers.csv                     # Player transfer records
```

## Dataset
This project uses data from **Transfermarkt**, a comprehensive soccer database covering:
- 1,000+ players across major European leagues
- 500+ clubs in top competitions
- 2 years of recent performance data
- Real-time market valuations
- Transfer history and contract details

**Download Dataset:**  
Access the complete dataset on Kaggle: [Player Scores - Transfermarkt Dataset](https://www.kaggle.com/datasets/davidcariboo/player-scores)

The dataset includes all necessary CSV files:
- Player demographics and contract information
- Match appearances and performance statistics
- Historical market valuations
- Club and competition details
- Game events and lineups

## Key Metrics Explained
- **Market Value (EUR):** Current estimated value of the player on the transfer market
- **Fair Value (EUR):** Predicted value based on performance metrics (goals, assists, minutes played)
- **Value Gap (EUR):** Difference between fair value and market value (positive = undervalued)
- **Undervalued Ratio:** Fair value / Market value ratio
  - > 1.5: Highly Undervalued 💎
  - 1.1 - 1.5: Slightly Undervalued ✅
  - 0.7 - 1.1: Fair Price ⚖️
  - < 0.7: Overvalued ⚠️

## Methodology
1. **Target Variable:** Log-transformed market value (to normalize distribution)
2. **Features:** Age, height, contract duration, per-90 statistics, position, foot, competition, country
3. **Model:** CatBoost Regressor (handles categorical variables naturally)
4. **Validation:** 5-Fold Cross-Validation with Out-of-Fold predictions
5. **Explainability:** Feature importance from CatBoost SHAP values

## Limitations & Future Work
- Analysis based on 2-year historical data; real-time updates not included
- Market value influenced by factors beyond performance (marketing, nationality)
- Position-specific models could improve accuracy
- Consider player injury history and age trajectory for more robust predictions

## Acknowledgements
- Dataset: [Kaggle - Transfermarkt European Soccer Database](https://www.kaggle.com/datasets/dcpinto/transfermarkt-european-soccer)
- CatBoost: Yandex ML toolkit (https://catboost.ai/)
- Visualization: matplotlib, seaborn

## License
This project is for educational and research purposes only. Dataset usage is governed by Transfermarkt's terms of service and Kaggle's dataset license.

---

**Author:** Data Science & Analytics  
**Date:** 2025-2026  
**Status:** Complete Analysis Pipeline Ready
