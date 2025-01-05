# Recipe Recommendation System

This project implements a recipe recommendation system based on nutritional information, ingredient filters, and exclusions. It provides a flexible framework to filter recipes by maximum nutritional values, include or exclude specific ingredients, and identify vegetarian or non-vegetarian recipes.

## Features

- Filters recipes by maximum nutritional values such as calories, fat, sugar, and protein.
- Supports ingredient-based filtering (include or exclude specific ingredients).
- Identifies vegetarian and non-vegetarian recipes based on ingredient analysis.
- Recommends recipes using a k-Nearest Neighbors (k-NN) algorithm.
- Provides options to customize recommendations, including specific dietary constraints.

## Data

The dataset used for this system contains the following key columns:

- **Nutritional Information**: Calories, FatContent, SaturatedFatContent, CholesterolContent, SodiumContent, CarbohydrateContent, FiberContent, SugarContent, ProteinContent.
- **Ingredients**: RecipeIngredientParts.
- **Recipe Details**: Name, CookTime, PrepTime, RecipeInstructions.

## Prerequisites

- Python 3.7+
- Libraries:
  - pandas
  - numpy
  - matplotlib
  - seaborn
  - scikit-learn
  - tabulate

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/recipe-recommender.git
   cd recipe-recommender
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Add your recipe dataset (`recipes.csv`) to the project directory.

## Usage

### Step 1: Load and Clean Data
The project starts by loading the dataset, cleaning missing values, and filtering columns for analysis.

```python
import pandas as pd

data = pd.read_csv('recipes.csv')
data = data.dropna(how='any')  # Remove rows with missing values
```

### Step 2: Define Filtering Criteria

Specify the maximum values for nutritional content and ingredients to include or exclude.

```python
max_values = {
    "Calories": 200,
    "FatContent": 10,
    "SaturatedFatContent": 5,
    "CholesterolContent": 50,
    "SodiumContent": 100,
    "CarbohydrateContent": 40,
    "FiberContent": 10,
    "SugarContent": 5,
    "ProteinContent": 20,
}

include_ingredients = ["potato", "butter", "salt", "onion"]
exclude_ingredients = []
```

### Step 3: Recommend Recipes

Use the `recommend_by_calories` function to get recipe recommendations based on your criteria.

```python
from recommender import recommend_by_calories

recommended_recipe = recommend_by_calories(
    dataframe=data,
    max_daily_fat=max_values["FatContent"],
    max_nutritional_values=list(max_values.values()),
    ingredient_filter=include_ingredients,
    exclude_ingredients=exclude_ingredients
)

if recommended_recipe is not None:
    print(recommended_recipe.head())
else:
    print("No recipes found matching the criteria.")
```

### Example Output

```plaintext
+--------+-----------------------------------------+-----------------------------------------+------------+--------------+-----------------------+----------------------+-----------------+-----------------------+----------------+----------------+------------------+---------------------------------------------------------------------+---------+
|   Name | RecipeIngredientParts                  | Calories                                 | FatContent | SaturatedFatContent | CholesterolContent | SodiumContent | CarbohydrateContent | FiberContent | SugarContent | ProteinContent | RecipeInstructions                                                 | isVeg   |
+--------+-----------------------------------------+-----------------------------------------+------------+--------------+-----------------------+----------------------+-----------------+-----------------------+----------------+----------------+------------------+---------------------------------------------------------------------+---------+
| Potato Pirozhki With Cabbage                    | [potato, flour, salt, cabbage, onion...]| 33.8                                     | 1.7        | 1.0                  | 17.7               | 93.9          | 3.9                  | 0.5          | 0.4          | 0.9             | [Prepare dough with flour and potatoes...]                       | 1       |
+--------+-----------------------------------------+-----------------------------------------+------------+--------------+-----------------------+----------------------+-----------------+-----------------------+----------------+----------------+------------------+---------------------------------------------------------------------+---------+
```

## Functions

### `extract_data`
Filters recipes based on nutritional values, ingredients to include, and ingredients to exclude.

### `scaling`
Normalizes the nutritional values for k-NN modeling.

### `nn_predictor`
Fits a k-NN model to the data for recipe recommendation.

### `recommend_by_calories`
Combines all steps to recommend recipes based on user-defined criteria.

## Customization

You can customize the recommendation system by:
- Modifying nutritional thresholds.
- Changing the distance metric in the k-NN model.
- Filtering recipes based on custom attributes or dietary preferences.

## Visualization

- The project includes visualizations such as histograms and scatter plots for data exploration.

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

## License

This project is licensed under the MIT License.
