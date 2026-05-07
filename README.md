# Executive Report: Used Car Pricing Analysis
### Objective:
The goal of this analysis was to identify the specific factors that drive used car prices and build a predictive model to help fine-tune inventory valuation. By analyzing over 426,000 listings, we aimed to move beyond basic estimates and provide a more precise tool for managing trade-ins and sales.

## Key Findings: What Drives Market Value?
Our analysis confirmed that used car valuation is a balance between objective usage metrics and the vehicle's specific configuration. No single factor dictates the price; rather, it is the combination of these elements that provides an accurate market picture.

* Core Foundation: car age (```year```) and mileage (```odometer```) with basic specs(```manufacturer``` and ```transmission```) remain the fundamental drivers of value. However, using these features in isolation resulted in a high margin of error.

* Critical Refinement: accuracy improved significantly once we integrated the vehicle's "context"—specifically its condition, fuel type, and category (e.g., Truck vs. Sedan). These features work alongside mileage to explain price variances that numbers on the dashboard cannot capture alone.

* Consistency Across Models: We tested three different mathematical approaches (Linear, Ridge, and Lasso). The fact that all three produced nearly identical results suggests that the pricing patterns in the data are very stable and reliable for use in inventory planning.

* The Limits of Complexity: We experimented with more complex mathematical transformations (Polynomials), but they only offered a minor improvement. This indicates that the raw features (like the actual condition and type of the car) are the true drivers of value, not complex mathematical curves.

* Brand Premium: The model identifies morgan, tesla, and porsche as the strongest positive drivers of price. Vehicles from these manufacturers command a significant "brand premium" that resists standard depreciation trends better than economy brands.

* Utility Premium: There is a clear market preference for diesel engines and truck/pickup categories. These vehicles are treated as high-value assets by consumers.

* Condition as a Value Floor: The strongest negative driver identified was "salvage" status. This status creates a value floor that no amount of low mileage can overcome.

## Model Performance
We utilized *GridSearchCV* to stress-test thousands of parameter combinations across the dataset.
Ridge Regression proved to be the most consistent model, as it effectively handled the large variety of ```manufacturers``` and ```types``` without being skewed by outliers.

| Model Phase | Features Included | Average Error (RMSE) |
| :--- | :--- | :--- |
| **Initial Baseline** | Year, Odometer, Manufacturer, Transmission | ```~$12,000``` |
| **Standard Model** | + Condition, Fuel, Type | ```$8,266``` |
| **Final Optimized Model** | + Degree 2 Polynomial Transformation | ```$7,923```

### Business Impact:
With an average vehicle price of $75,199 in this dataset, the final model is accurate within approximately 11%. This represents a 33.9% improvement over the initial baseline, significantly reducing the risk of overpaying for inventory or underpricing a sale.

## Recommendation
The modeling phase has extracted the maximum value from the current dataset. We have successfully reduced "pricing noise" by over one-third, and the model is now validated for use in inventory management.

* Deployment: The Ridge Regression model is recommended for deployment. It was the most stable performer across the large dataset and provides a much more reliable price than a basic estimate.

* Operational Focus: To maintain high accuracy, the dealership should focus on standardizing condition reports. Since ```condition``` was a high-impact factor in lowering the model's error, consistent grading will lead to the most reliable price forecasts.

* Future Improvements: The similarity between all our test results suggests we have hit a "ceiling" with the current data. To further improve precision, future data collection should focus on standardizing ```model``` naming and remove noises: While car model (e.g., F-150, Camry) is a major price driver, the current dataset contains nearly 30,000 unique model variations. This extreme variation makes it difficult for the regression to include this as a reliable feature without introducing noise. Cleaning this input will allow us to move ```model``` from a source of noise to a primary feature, likely driving accuracy even higher.


# Repository Structure
* prompt_II.ipynb: The main technical analysis, including data cleaning, feature engineering (Polynomials), and model evaluation.

* data/: directory containing the used car dataset

* images/: images referenced in the jupiter notebook

# How to Use
1. Clone this repository:
   ```bash
   git clone [https://github.com/KyungHee1251/UsedCarPriceModel.git](https://github.com/KyungHee1251/UsedCarPriceModel.git)
   ```
2. Open the notebook:
   ```
   jupyter notebook prompt_II.ipynb
   ```
