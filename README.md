# CPO Luxury Compact SUV Price Analysis & Finder
### CSS Bootcamp Final Project | UC San Diego

## Overview
How can we tell whether a Certified Pre-Owned (CPO) luxury SUV is actually a good deal?
Two vehicles from the same model year can have very different listing prices depending on mileage, model, and other characteristics. This project uses real CPO vehicle listings from the San Diego market to examine how these basic characteristics are associated with listing price.

The project focuses on three luxury compact SUVs:
- Mercedes-Benz GLC 300
- BMW X3
- Audi Q5

Vehicle listings were collected directly from the auto.dev API, cleaned and analyzed in Python, and used to build regression models for estimating expected listing prices.
The final step turns the analysis into a simple **CPO Finder**, which allows users to filter real listings based on their preferred brand, budget, mileage, and model year.

## Presentation
The final project presentation is available here:
📊 **[View Final Presentation](CSSprojectpresentation.pdf)**
- **`Css bootcamp project.pdf`** — Final project presentation

## Research Question
**Can basic vehicle characteristics predict the listing price of Certified Pre-Owned luxury SUVs in the San Diego market?**

The analysis focuses on three main predictors:
- Model year
- Mileage
- Vehicle model


## Project Workflow
1. **Data Collection** — Collect real CPO listings through the auto.dev API
2. **Data Cleaning** — Extract and clean vehicle, price, mileage, and dealer information
3. **Exploratory Data Analysis** — Compare price distributions across models, years, and mileage
4. **Regression Analysis** — Estimate how vehicle characteristics are associated with listing price
5. **Prediction** — Generate expected prices using the fitted model
6. **CPO Finder** — Filter real CPO listings based on user-defined purchasing preferences

## Data
The dataset contains Certified Pre-Owned listings within approximately 100 miles of ZIP code **92122 (San Diego, CA)**.

The main variables include:

| Variable | Description |
|---|---|
| `year` | Vehicle model year |
| `make` | Manufacturer |
| `model` | Vehicle model |
| `trim` | Vehicle trim |
| `price` | Dealer listing price |
| `miles` | Vehicle mileage |
| `dealer` | Listing dealership |
| `city` | Dealer city |
| `state` | Dealer state |
| `cpo` | Certified Pre-Owned status |

The repository includes both the original API dataset (`all_cars.csv`) and the cleaned dataset used for analysis (`all_cars_clean.csv`).


## Exploratory Analysis
The exploratory analysis revealed clear relationships between vehicle characteristics and listing price.

### Model Year and Price
Newer CPO vehicles generally had higher listing prices. Across the three models, model year showed a strong positive relationship with price, suggesting that vehicle age is one of the most important factors in the CPO market.

### Mileage and Price
Higher-mileage vehicles generally had lower listing prices. However, mileage alone did not explain all of the variation in price, since vehicles with similar mileage could still differ substantially depending on model and model year.

### Differences Across Models
Price distributions also differed across the Mercedes-Benz GLC 300, BMW X3, and Audi Q5. This motivated including vehicle model together with year and mileage in the final regression model.

## Regression Model
To estimate expected listing prices, I fitted an Ordinary Least Squares (OLS) regression model using:
- Model year
- Mileage
- Vehicle model

The model can be represented conceptually as:
`Price = β₀ + β₁(Year) + β₂(Mileage) + β₃(Model) + ε`

This approach allows the effects of mileage and model year to be estimated while controlling for differences between the three vehicle models.

## From Regression to Prediction
To evaluate performance on unseen data, the dataset was split into:

- **80% training data**
- **20% test data**

The OLS model was fitted using only the training set, and predictions were then generated for the held-out test set.

| Metric | Test Result | Interpretation |
| ------ | ----------: | -------------- |
| R² | **0.811** | The model explained approximately 81.1% of the variation in listing prices in the test data. |
| MAE | **$2,881.01** | Predictions differed from actual listing prices by about $2,881 on average. |

These results suggest that model year, mileage, and vehicle model together provide substantial predictive information about CPO listing prices, although meaningful price variation remains unexplained.
In other words, the model explained about **81% of the variation in listing prices**, while its predictions were approximately **$2,881 away from the actual listing price on average**.

## CPO Finder
To make the analysis more practical, I also built an interactive **CPO Finder** in Python.

The Finder allows a user to specify:
- Preferred brand
- Maximum budget
- Maximum mileage
- Minimum model year
- Preferred sorting method (price or mileage)

The program then filters the available CPO listings and returns vehicles that match the user's requirements.
Currently supported models are:
- BMW X3
- Audi Q5
- Mercedes-Benz GLC 300

This component turns the project from a purely statistical analysis into a simple decision-support tool for exploring real vehicle listings.



## Getting Started
1. Clone the repository:

```bash
git clone https://github.com/mr-knio/CSS-final-project-CPO-filter.git
cd CSS-final-project-CPO-filter
```

2. Open `CPO_FilterProject.ipynb` in Jupyter Notebook.

3. To reproduce the analysis without making new API requests, start from the section that loads the provided cleaned dataset:
```python
import pandas as pd
all_cars = pd.read_csv("all_cars_clean.csv")
```

4. Run the remaining analysis cells to reproduce the exploratory analysis, regression model, model evaluation, and CPO Finder.

> The original API collection code is included in the notebook for reproducibility, but rerunning it requires a valid auto.dev API key.


## Limitations

This project has several important limitations:

- The analysis uses **listing prices**, not final transaction prices.
- The dataset represents listings available during a specific collection period within approximately 100 miles of San Diego.
- Important vehicle characteristics such as accident history, optional equipment, drivetrain, condition, and dealer fees are not fully captured.
- The analysis focuses only on three CPO luxury compact SUV models.
- The regression results represent associations in this dataset and should not be interpreted as causal effects.

## Presentation
**Slides:** [View project presentation](https://docs.google.com/presentation/d/1LAmtY7-QEz8Nzd4LMjXDs9umTo04yUDr7xCYsoAtn5k/edit?slide=id.gc6f90357f_0_31#slide=id.gc6f90357f_0_31)


## Repository Structure

```text
.
├── CPO_FilterProject.ipynb
├── CSS bootcamp project.pdf
├── all_cars.csv
├── all_cars_clean.csv
└── README.md
```

- `CPO_FilterProject.ipynb` — Full API collection, data cleaning, exploratory analysis, regression, prediction, and CPO Finder
- `all_cars.csv` — Original dataset collected from the API
- `all_cars_clean.csv` — Cleaned dataset used for the final analysis

## Tools

- Python
- Pandas
- Matplotlib
- Statsmodels
- Scikit-learn
- Requests
- Jupyter Notebook
- Auto.dev API

## Author
**Yufei Meng**  
Computational Social Science  
University of California San Diego

## Note
> **Important:** A lower-than-predicted price does not necessarily mean that a vehicle is objectively a "good deal." Vehicle condition, accident history, options, drivetrain, dealer fees, and other characteristics are not fully captured by the model.
