# Hyperparameter Optimization

Hyperparameter Optimization is the process of finding the best set of hyperparameters for a machine learning model to maximize its performance. Unlike model parameters, which are learned during training, hyperparameters are predefined settings (e.g., learning rate, number of trees in a random forest, kernel type in an SVM) that control the training process. Proper tuning of these hyperparameters can significantly improve the model's accuracy and efficiency.

## Common Techniques for Hyperparameter Optimization
1. **Grid Search** (e.g., `GridSearchCV`)
2. **Random Search** (e.g., `RandomizedSearchCV`)

<br>

## GridSearchCV
`GridSearchCV` performs an exhaustive search over a specified parameter grid. It evaluates every possible combination of hyperparameter values to find the one that yields the best performance based on a scoring metric.

### How GridSearchCV Works:
1. **Define a parameter grid:** Specify the hyperparameters and their possible values.
   ```python
   param_grid = {
       'n_estimators': [50, 100, 200],
       'max_depth': [10, 20, None],
       'min_samples_split': [2, 5, 10]
   }
   ```
2. **Iterate through combinations:** For every combination of hyperparameter values, the model is trained and evaluated using cross-validation.
3. **Compute performance metric:** Evaluate the performance for each combination.
4. **Select the best model:** Choose the hyperparameter combination with the best score.

### Example Code:
```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

# Initialize model
model = RandomForestClassifier()

# Define parameter grid
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [10, 20, None],
    'min_samples_split': [2, 5, 10]
}

# Set up GridSearchCV
grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=5, scoring='accuracy')

# Fit the model
grid_search.fit(X_train, y_train)

# Best hyperparameters
print("Best Hyperparameters:", grid_search.best_params_)
```

<br>

## RandomizedSearchCV
`RandomizedSearchCV` selects random combinations of hyperparameters from the parameter grid. It does not test all combinations but samples a fixed number of settings.

### How RandomizedSearchCV Works:
1. **Define a parameter grid:** Specify hyperparameters and ranges, which can include continuous distributions.
   ```python
   param_dist = {
       'n_estimators': [50, 100, 200],
       'max_depth': [10, 20, None],
       'min_samples_split': [2, 5, 10],
       'max_features': ['sqrt', 'log2', None]
   }
   ```
2. **Random sampling:** Randomly sample a fixed number of combinations.
3. **Evaluate combinations:** Evaluate performance for sampled hyperparameter combinations using cross-validation.
4. **Select the best model:** Choose the combination with the highest score.

### Advantages over GridSearchCV:
- More efficient with large hyperparameter spaces.
- Allows control over the number of iterations (`n_iter`).

### Example Code:
```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import RandomForestClassifier
from scipy.stats import randint

# Initialize model
model = RandomForestClassifier()

# Define parameter distributions
param_dist = {
    'n_estimators': randint(50, 200),
    'max_depth': [10, 20, None],
    'min_samples_split': randint(2, 10),
    'max_features': ['sqrt', 'log2', None]
}

# Set up RandomizedSearchCV
random_search = RandomizedSearchCV(estimator=model, param_distributions=param_dist,
                                   n_iter=10, cv=5, scoring='accuracy', random_state=42)

# Fit the model
random_search.fit(X_train, y_train)

# Best hyperparameters
print("Best Hyperparameters:", random_search.best_params_)
```

<br>

## Key Differences Between GridSearchCV and RandomizedSearchCV

| **Aspect**            | **GridSearchCV**                               | **RandomizedSearchCV**                        |
|------------------------|-----------------------------------------------|-----------------------------------------------|
| Search Method          | Exhaustive search over all combinations.      | Random sampling of hyperparameter combinations. |
| Efficiency             | Computationally expensive for large grids.   | Faster for large hyperparameter spaces.       |
| Flexibility            | Tests all combinations.                      | Can include distributions for parameters.     |
| Parameter Space        | Fixed grid of values.                        | Can define ranges or distributions.           |

<br>

## Choosing Between the Two

- Use **GridSearchCV** when:
  - The hyperparameter space is small.
  - You want to test all combinations.
- Use **RandomizedSearchCV** when:
  - The hyperparameter space is large.
  - You want faster results with approximate optimization.

Both methods are implemented in Scikit-learn and are powerful tools for model tuning.

