# Red Light, Green Light: Should He Go?
### SMT Data Challenge 2026 | Baseball Analytics & Fan Engagement

## Project Overview

**Red Light, Green Light: Should He Go?** is a baseball analytics project developed for the 2026 SMT Data Challenge.

The project explores whether player-tracking data and machine learning can help identify patterns associated with successful stolen base attempts at second base.

The project has two main objectives:

1. **Baseball Analytics:** Analyze offensive and defensive movement data to classify stolen base attempts as successful or unsuccessful.
2. **Fan Engagement:** Transform machine learning findings into a visual, scoreboard-style experience that makes stolen base attempts more exciting and easier for fans to understand.

The central question is:

**Can defensive movement patterns help predict whether a runner will successfully steal second base?**

## Data Sources

The project uses baseball tracking data provided through the SMT Data Challenge.

Three main datasets were analyzed:

- **Ball Events:** Used to identify catcher throws and defensive catches.
- **Player Positioning:** Used to analyze runner and defensive player movements.
- **Lineups:** Used to support the identification of potential stolen base attempts.

The analysis focuses on runners advancing from first base to second base and the defensive movements of the second baseman and shortstop.

## Technologies Used

- Python
- Polars
- pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Great Tables
- Jupyter Notebook

### Why Polars?

One of the most valuable learning experiences during this challenge was learning **Polars**, a DataFrame library for Python.

Before this project, I primarily used pandas for data manipulation. After working with Polars throughout the challenge, I found its expressions, filtering, and DataFrame operations particularly useful for handling baseball tracking data.

Polars has become my preferred tool over pandas for many data preparation tasks.

## Methodology

### 1. Data Cleaning and Preparation

SMT tracking data was filtered and organized to identify plays involving potential stolen base attempts.

The analysis included identifying base occupancy, comparing runner positions, examining lineup information, and matching catcher throws to defensive catches.

### 2. Feature Engineering

Movement features were prepared for machine learning, including:

| Feature | Description |
|---|---|
| `dcov_step_defense` | Defensive distance covered during a measured movement step |
| `i_vel_defense` | Instantaneous defensive velocity |
| `i_accel_defense` | Instantaneous defensive acceleration |
| `i_jerk_defense` | Instantaneous rate of change in defensive acceleration |
| `throw_time` | Time between the catcher throwing the ball and a defensive player receiving it |

### 3. Machine Learning

The target variable was `steal_successful`:

- `0` = Failed steal
- `1` = Successful steal

The analysis explored logistic regression, decision trees, forward feature selection, and hyperparameter tuning with GridSearchCV.

Forward feature selection was used to identify useful feature combinations, while ROC AUC was used to evaluate classification performance during cross-validation.

### 4. Model Evaluation

Four decision tree experiments were compared.

| Test | Features | Test Accuracy | Description |
|---|---:|---:|---|
| 1 | 4 | 74% | Defensive movement features only |
| 2 | 7 | 82% | Included runner positioning |
| 3 | 6 | 82% | Included additional runner movement |
| 4 | 4 | 100% | Suspected data leakage |

**Important:** The 100% accuracy result was not accepted as a valid final model. It raised concerns about data leakage because some runner movement features may reveal the outcome after the steal occurred.

The defensive-only model was selected as the more conservative result, although additional validation would be needed before applying it to live game predictions.

## Key Findings

- Defensive distance covered, velocity, acceleration, and jerk provided useful signals for classifying steal outcomes.
- Recorded catcher-to-second-baseman throws averaged approximately **2.42 seconds**.
- Recorded catcher-to-shortstop throws averaged approximately **2.41 seconds**.
- The observed steal success rate was **70.00%** for plays with a recorded second-baseman catch and **62.75%** for plays with a recorded shortstop catch.
- Runner-related movement features introduced potential data leakage, demonstrating the importance of selecting features available at the intended prediction time.

These findings describe patterns in the analyzed sample and do not establish causal relationships or guarantee future steal outcomes.

## Fan Engagement Concept

The project's second objective was to translate statistical analysis into a scoreboard visualization.

The **Red Light, Green Light** concept presents a simplified decision tree with two potential outcomes:

- **Green Light:** The model predicts a successful steal.
- **Red Light:** The model predicts a failed steal.

The goal is to help fans understand the strategy behind stolen base attempts while creating a more engaging stadium experience.

The visualization is a prototype rather than a validated real-time prediction system.

## Project Files

The repository may include:

- Jupyter notebooks containing data preparation and machine learning analysis
- Model evaluation results
- Steal success summary tables
- Throw-time distribution figures
- Forward feature selection figures
- Decision tree and scoreboard concept graphics
- Final research paper and supplemental documentation

## Future Improvements

Potential improvements include:

- Expanding analysis to additional games and steal attempts
- Verifying stolen base outcomes against official play records
- Including pitcher delivery time and catcher pop time
- Adding ball tracking and defensive throw direction
- Improving model validation and preventing data leakage
- Testing steals of third base and home plate
- Developing an interactive scoreboard prototype

## Acknowledgements

Special thanks to the SMT Data Challenge organizers and the contributors who provided technical resources, tutorials, and project guidance.

I would also like to acknowledge:

- **Dr. Meredith Wills** — Office hours and model evaluation feedback
- **Cameron Adams** — Office hours and project guidance
- **Billy Fryer** — Office hours and technical support
- **Andrew Steenkamer** — Project support
- **Yu-Hao Yeh** — Python animation code reference

Additional support came from SMT Data Challenge tutorials and community discussions through the Discord paper-writing, Python-help, and R-help channels.

## References

- [Scikit-learn Documentation](https://scikit-learn.org/stable/)
- [Polars Documentation](https://docs.pola.rs/)
- [pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [Seaborn Documentation](https://seaborn.pydata.org/)
- [TeamRankings](https://www.teamrankings.com/)
- SMT Data Challenge — Provided baseball tracking datasets and tutorials

## Data Availability

The analysis uses data provided through the SMT Data Challenge. Redistribution of the original SMT datasets is subject to the challenge's data-access and sharing requirements.

## Project Status

**2026 SMT Data Challenge submission completed.**

The project is intended for research, learning, and fan-engagement prototyping. The predictive models are exploratory and require further validation before operational use.
