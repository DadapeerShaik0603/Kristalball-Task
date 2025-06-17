# Bar Inventory Forecasting System

## Overview

This project develops a data-driven forecasting and inventory recommendation system for a national hotel chain's bars to address inventory management challenges. Using historical sales data, the system predicts item-level demand for beverages (e.g., rum, vodka, wine) and recommends optimal stock levels to minimize stockouts, reduce overstocking, and enhance customer satisfaction. The core implementation is in a Jupyter Notebook (`Task - Kristalball.ipynb`), leveraging ARIMA for time-series forecasting.

## Objectives

- **Accurate Demand Forecasting**: Predict daily consumption for each bar, alcohol type, and brand.
- **Optimal Inventory Management**: Recommend stock levels to prevent stockouts and reduce holding costs.
- **Operational Efficiency**: Provide actionable insights for bar managers to streamline purchasing and improve customer experiences.
- **Cost Reduction**: Minimize wastage from excess inventory.

## Project Structure

- **`Task - Kristalball.ipynb`**: Main Jupyter Notebook containing the workflow, including data loading, preprocessing, forecasting, and inventory recommendations.
- **`Consumption Dataset.xlsx`**: Input dataset with historical sales and inventory data (not included in the repository).
- **`README.md`**: This file, providing project overview and instructions.
- **`Project_Summary.md`**: Summary of the business problem, assumptions, model choice, performance, and real-world application (optional artifact).
- **`Project_Summary.tex`**: LaTeX source for a PDF summary of the project (optional artifact).

## Setup Instructions

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab
- Required Python libraries:
  - `pandas`
  - `numpy`
  - `statsmodels`
  - `openpyxl` (for Excel file reading)

### Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy statsmodels openpyxl
   ```
3. Ensure the `Consumption Dataset.xlsx` file is placed in the project directory or update the file path in the notebook.
4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
5. Open `Task - Kristalball.ipynb` to run the analysis.

## Usage

1. **Run the Notebook**:
   - Execute cells in `Task - Kristalball.ipynb` sequentially to load data, preprocess, and generate forecasts.
   - The notebook loads `Consumption Dataset.xlsx`, processes data for six bars (Anderson’s, Brown’s, Johnson’s, Smith’s, Taylor’s, Thomas’s), and forecasts consumption for June 19, 2025.

2. **Key Components**:
   - **Data Loading**: Imports historical data (6,575 rows, 8 columns) covering bar sales from January 2023 to January 2024.
   - **Preprocessing**: Checks for nulls and duplicates (none found) and prepares data for forecasting.
   - **Forecasting**: Uses the `BarInventoryForecastOptimizer` class with ARIMA (order: 1,1,1) to predict daily consumption and recommend stock levels (forecast × 1.3 safety buffer).
   - **Output**: Generates forecasts for each bar, e.g., Anderson’s Bar recommends 103.39 ml of Captain Morgan rum for June 19, 2025.

3. **Example Output**:
   ```plaintext
   Anderson's Bar | 2025-06-19 | Rum | Captain Morgan | Forecasted: 79.53 ml | Stock to Maintain: 103.39 ml
   Brown's Bar | 2025-06-19 | Rum | Malibu | Forecasted: 122.77 ml | Stock to Maintain: 159.60 ml
   ```

## Assumptions

- Historical demand patterns (2023–2024) remain stable into 2025.
- Missing dates in the time series have zero consumption.
- ARIMA with fixed (1,1,1) order is sufficient for all items.
- A 30% safety buffer adequately accounts for demand variability.

## Limitations

- **No Model Evaluation**: Lacks validation metrics (e.g., MAE, RMSE) to assess forecast accuracy.
- **Fixed ARIMA Parameters**: May not capture complex patterns for all items.
- **Data Anomalies**: Near-zero opening balances (e.g., 8.526513e-14 ml) suggest potential data quality issues.
- **No External Factors**: Does not account for holidays, promotions, or events affecting demand.

## Future Improvements

- **Feature Engineering**: Implement planned features (e.g., Day of Week, Season) to capture temporal patterns.
- **Model Optimization**: Use grid search for ARIMA parameters or explore SARIMA/Prophet for seasonality.
- **Performance Evaluation**: Add train-test splits and error metrics to validate forecasts.
- **Data Validation**: Investigate and correct anomalies in inventory balances.
- **Scalability**: Optimize for larger datasets (e.g., parallel processing for multiple bars).
- **Visualization**: Add charts to display forecasted consumption and stock levels.

## Real-World Application

In a hotel, the system would integrate with inventory software, providing daily stock recommendations (e.g., via dashboards) to guide purchasing. Bar managers would use forecasts to ensure high-demand items (e.g., Smirnoff vodka) are stocked while avoiding excess inventory for low-demand items (e.g., Budweiser beer). Automation could enable nightly updates, improving efficiency and customer satisfaction.

## Scalability and Production Considerations

- **Challenges**: Processing large datasets for many bars could slow ARIMA fitting; external factors (e.g., events) may disrupt forecasts.
- **Monitoring**: Track forecast accuracy (MAE/RMSE), stockout/overstock incidents, data quality, and manager adoption in production.

## Contributing

Contributions are welcome! Please submit issues or pull requests for bug fixes, feature enhancements, or documentation improvements.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
