# WNBA PrizePicks Machine Learning Predictor

## Project Overview
This is an end-to-end Python machine learning pipeline designed to scrape live WNBA data, predict player performance statistics (specifically points and rebounds), and identify the highest-probability betting lines on PrizePicks. 

By comparing proprietary machine learning predictions against live projections scraped directly from PrizePicks.com, this project calculates a customized "confidence metric" to systematically recommend the most advantageous lines.

## Repository Structure

The project is broken down into three core Jupyter Notebooks, representing the full data science lifecycle from collection to deployment:

* **`1. PrizePicks Webscraping and Data Analysis.ipynb`**
  * **Data Collection:** Utilizes XPath web scraping to gather live WNBA player data and current PrizePicks lines.
  * **Data Processing:** Handles data cleaning, manipulation, and the calculation of key prior probabilities.
  * **EDA & Feature Engineering:** Explores data through visualizations and correlation matrices to engineer predictive features for the models.

* **`2. PrizePicks Model Building.ipynb`**
  * **Model Training:** Tests various machine learning architectures using different combinations of engineered features.
  * **Optimization:** Leverages XGBoost and GridSearchCV for hyperparameter tuning to ensure the highest accuracy possible when predicting player points and rebounds.

* **`3. PrizePicks Final Model.ipynb`**
  * **Execution Pipeline:** The production script. Running this notebook executes the end-to-end process: scraping real-time data, feeding it into the optimized models, and outputting predictions compared to live PrizePicks lines.
  * **Opportunity Identification:** Automatically filters and ranks the highest-probability predictions based on the custom confidence metric.

## Methodology: The Confidence Metric

To determine which PrizePicks lines offer the highest probability of success, the final model evaluates predictions using a custom confidence function that accounts for sample size, the delta between the prediction and the line, and the model's Root Mean Squared Error (RMSE):

`Confidence = (√sample_size * |point_prediction - Line|) / RMSE`

## Tech Stack

* **Web Scraping:** `requests`, `lxml` (HTML XPath parsing)
* **Data Processing & EDA:** `pandas`, `numpy`
* **Machine Learning:** `xgboost`, `scikit-learn` (GridSearch)

## Future Improvements

To scale this project from a local script to a robust, production-ready application, the following enhancements are planned:

* **Database Integration:** Transitioning from local data manipulation to a structured database (e.g., SQL) for long-term storage of historical odds, predictions, and actual WNBA player outcomes. This will enable continuous performance tracking, backtesting, and model evaluation over time.
* **Interactive Web Dashboard:** Wrapping the final prediction pipeline in a web application framework (such as Streamlit) to create a user-friendly frontend. This will allow for quick, daily visualizations of the highest-probability lines without needing to manually execute Jupyter Notebooks.
* **Advanced Feature Engineering:** Integrating secondary data sources, such as live injury reports, team defensive match-ups, pace-of-play metrics, or even utilizing NLP on sports news to capture player momentum and situational context.
* **Automated Pipeline & MLOps:** Setting up cloud functions or CRON jobs to automatically scrape data daily, evaluate the previous day's model accuracy, and trigger automated retraining pipelines if the model's RMSE begins to drift.
