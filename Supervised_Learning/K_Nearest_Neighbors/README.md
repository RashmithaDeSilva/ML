# K-Nearest Neighbors (KNN)

It can be used in regression problems and classification problems and most use cases the classification problem.

K-Nearest Neighbors (KNN) is a simple and widely used machine learning algorithm, primarily for classification and regression tasks. It operates based on similarity, making predictions by identifying the most similar examples in the training dataset.

<br>

## How KNN Works

1. **Training Phase:**
   - KNN is considered a "lazy learner" because it doesn’t explicitly learn a model during training. Instead, it stores the entire training dataset.

2. **Prediction Phase (for new data):**
   - **Step 1:** Calculate the distance between the new data point and all points in the training dataset. Common distance metrics include:
     - **Euclidean distance** (most common)
     - Manhattan distance
     - Minkowski distance
   - **Step 2:** Identify the **K nearest neighbors** (data points closest to the new data point based on the chosen distance metric).
   - **Step 3:** For:
     - **Classification:** Assign the most common class label among the K neighbors.
     - **Regression:** Calculate the average (or weighted average) of the target values of the K neighbors.

<br>

## Key Parameters of KNN

- **K (Number of Neighbors):**
  - Determines how many neighbors are considered for making predictions.
  - Small K: Sensitive to noise, risk of overfitting.
  - Large K: Smoother predictions but may miss local patterns.
- **Distance Metric:**
  - Affects how neighbors are determined. For example, Euclidean distance is suitable for continuous features, while Hamming distance works well for categorical data.

<br>

## Advantages of KNN

1. **Simplicity:** Easy to understand and implement.
2. **Non-Parametric:** No assumption about the data distribution.
3. **Versatility:** Works for both classification and regression.

<br>

## Disadvantages of KNN

1. **Computational Cost:** As it involves calculating distances for all training data points, it can be slow with large datasets.
2. **Sensitivity to Irrelevant Features:** Performance can degrade if features are not properly scaled or irrelevant features dominate.
3. **Memory Usage:** Requires storing the entire training dataset.

<br>

## Example Workflow of KNN

1. **Dataset:** Suppose you have a dataset of fruits with features like weight and color intensity.
2. **New Data Point:** A fruit with unknown type.
3. **K = 3:** You choose to look at the 3 nearest fruits.
4. **Prediction:** If 2 of the nearest neighbors are apples and 1 is a pear, the new fruit is classified as an apple (majority rule).

<br>

## Conclusion

The K-Nearest Neighbors algorithm is an intuitive and flexible technique for both classification and regression tasks. However, it requires careful consideration of the value of K, distance metric, and feature scaling to achieve optimal performance.
