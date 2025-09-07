# AI

## Machine Learning
- In general, the more options you give a learning algorithm to learn, the better it will perform.

## Index
1. [Machine Learning Algorithm](#machine-learning-algorithm)
    1. [Supervised Learning](#1-supervised-learning)
    2. [Unsupervised Learning](#2-unsupervised-learning)
    3. [Supervised Learning vs Unsupervised Learning](#comparison-supervised-learning-vs-unsupervised-learning)
2. [Regression Algorithms](#regression-algorithms)
    1. [Linear Regression](#1-linear-regression)
    2. [Polynomial Regression](#2-polynomial-regression)
3. [Evaluation Metric (Performance Metric)](#evaluation-metric-cost-function-for-linear-regression)
    1. [Hypothesis function](#1-hypothesis-function)
    2. [Cost Function (Squared Error Cost Function)](#2-cost-function-squared-error-cost-function)
    3. [Cost Function Intuition](#3-cost-function-intuition)

100. [Terminology](#terminology)


## Machine Learning Algorithm
> Knowing Machine Learning Algorithms is important but what's more important is to know how to use them.

### 1. Supervised Learning
- **Practical Impact & Innovation**
    - Used the most in real-world applications.
    - Has seen the most rapid advancements and innovation.
- **Definition**
    > A method where the model learns from data that has both inputs (x) and outputs (y).
    - `Input (x)` to `output (y)`
        - Giving "right answers" from learning
        - The goal is to gather data, learn the trend (or relationship) between x and y, and when you have x, produce y.
        - `More high-quality data and a greater variety of relevant inputs generally improve the accuracy of predicting y.`
- **Process**
    1. **Training Set**: Prepare data (features `x` and target `y`)
    2. **Learning Algorithm**: Choose an algorithm to train the model (e.g., Linear Regression, Decision Tree)
    3. **Function / Model**: Train the model to create a function (`h(x)` → y prediction)
    4. **Prediction**: Use the trained model to predict `y_pred` for new input `x`

    > Key point: Supervised Learning trains on data with **both inputs (x) and outputs (y)**.

    **Process Diagram:**

    ```markdown
    Training Set (x, y)
            │
            ▼
    Learning Algorithm
    (e.g., Linear Regression, Decision Tree)
            │
            ▼
    Function / Model (h(x) → y_pred)
            │
            ▼
    Prediction (y_pred for new x)
    ```
- **Types**
    > Classification focuses on finding boundaries, whereas Regression focuses on identifying trends.
    - `Regression`
        - Used when the output y is a continuous number.
        - Predicts a continuous number, meaning there are <u>***infinitely many possible outputs***</u>, based on existing data.
            - Example: Predicting house price from size, predicting height from age.
        - `Regression → identifying trends`
        - Type
            - [Linear Regression](#linear-regression)
            - [Polynomial Regression](#polynomial-regression)
        
    - `Classification`
        - Used when the output y is a category.
        - Predicts categories, meaning there are a <u>***limited number of possible outputs***</u>, based on existing data.
            - Example: Classifying emails as spam or not, classifying images as cat or dog, detecting cancers.
        - `Classification → finding boundaries`
        - Type
            - Logistic Regression
            - Decision Tree
            - Random Forest

### 2. Unsupervised Learning
- **Practical Impact & Innovation**
    - Used in various real-world applications such as customer segmentation, anomaly detection, and data exploration.
    - Has seen rapid advancements in clustering algorithms, dimensionality reduction, and representation learning.
- **Definition**
    > A method where the model learns from data that has **inputs (x) only**, without output labels (y).
    - ***<u>Unsupervised learning is more suitable for situations where the input data is constantly changing.</u>***
    - Learns patterns, structures, or relationships within the data.
        - `The goal is to find hidden patterns, group similar data points, or reduce dimensions for better understanding.`
- **Process**
    1. **Dataset**: Only input data exists (`x`)
    2. **Learning Algorithm**: Use clustering, dimensionality reduction, or other pattern-finding algorithms
    3. **Model / Structure**: Identify patterns, groups, or structure within the data
    4. **Insight / Application**: Assign clusters, extract features, detect anomalies, etc.

    > Key point: Unsupervised Learning finds **structure or patterns in the data without labeled outputs**.

    **Process Diagram:**

    ```markdown
    Dataset (x only)
            │
            ▼
    Learning Algorithm
    (e.g., K-Means, PCA)
            │
            ▼
    Model / Structure (patterns, clusters, structure)
            │
            ▼
    Insight / Application
    (cluster assignment, feature extraction, anomaly detection)
    ```
- **Types**
    > Focuses on discovering structure in the data rather than predicting specific outputs.
    - `Clustering`
        - Groups similar data points based on their features.
        - Finds groups, patterns, or structures in the data.
        - Example: Customer segmentation, grouping similar documents or images, grouping google news.
        - `Clustering → finding groups, patterns or structures`
        
    - `Dimensionality Reduction`
        - Reduces the number of input features in a dataset while preserving important information.
        - Example: PCA (Principal Component Analysis), t-SNE for visualization.
        - `Dimensionality Reduction → capturing key structure`
        
    - `Anomaly Detection`
        - Identifies unusual or rare data points in a dataset.
        - Example: Fraud detection, network intrusion detection.
        - `Anomaly Detection → finding outliers`

### *Comparison: Supervised Learning vs Unsupervised Learning*
- **Supervised Learning:**
    - Learns from data that includes both inputs (x) and outputs (y).
    - The model learns the relationship x → y and can predict y for new x.
    - Examples: Predicting house price from size, predicting height from age, classifying emails as spam or not.
- **Unsupervised Learning:**
    - Uses input data (x) only, without output labels (y).
    - The model learns patterns, structures, clusters, or associations in the data.
    - Examples: Customer segmentation, dimensionality reduction (PCA), anomaly detection.
- **Key difference:**
    - `Supervised → requires labeled data (x + y)`
    - `Unsupervised → works with unlabeled data (x only)`


---

## Regression Algorithms

### 1. Linear Regression
- **Definition**: A method to model the relationship between input variables (x) and a continuous output (y) using ***<u>a straight line</u>***.
- **Use cases**: House price prediction, salary prediction.
- **Types**
   1. **Single-variable Linear Regression (Simple Linear Regression / Univariate Linear Regression)**
        - **Input**: Only one input variable `x`
        - **Equation**: `y = wx + b`
        - **Example**: Predicting house price based on house size
    2. **Multi-variable Linear Regression (Multiple Linear Regression)**
        - **Input**: Multiple input variables (`x₁, x₂, …, xₙ`)
        - **Equation**: `y = w₁x₁ + w₂x₂ + … + wₙxₙ + b`
        - **Example**: Predicting house price based on house size, number of rooms, and location


### 2. Polynomial Regression
- **Definition**: An extension of linear regression where the relationship between x and y is modeled as an ***<u>nth-degree polynomial</u>***.
- **Use cases**: Growth curves, non-linear trends.
- **Equation**: y = w₀ + w₁x + w₂x² + … + wₙxⁿ


---

## Evaluation Metric (Cost Function for Linear Regression)

- **Definition**: A mathematical function that measures how well the model’s predictions match the actual values.
- **Why it matters**: It provides a target to minimize during training (optimization).

### 1. Hypothesis function

- Prediction formula:

  $$
  \hat{y}^{(i)} = f_{w, b}(x^{(i)}) = wx^{(i)} + b
  $$

### 2. Cost Function (Squared Error Cost Function)

> A function that measures how wrong the model is across the entire dataset.

- Predicted value: $\hat{y}$ (y-hat)

- Actual value: $y$

- Error: $\hat{y} - y$

- Cost Function: A single number that represents how wrong the model is across all training data.

- The most commonly used in Linear Regression: Squared Error Cost Function

- Formula:

  $$
  J(w, b) = \frac{1}{2m} \sum_{i=1}^{m} (\hat{y}^{(i)} - y^{(i)})^2
  $$

  $$
  J(w, b) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w, b}(x^{(i)}) - y^{(i)})^2
  $$

- **Explanation**:

  - $m$: number of training examples
  - $\hat{y}^{(i)}$: predicted value
  - $y^{(i)}$: actual value
  - Goal / Purpose: Find $w$ and $b$ such that $\hat{y}^{(i)}$ is as close as possible to $y^{(i)}$ for all training data. In other words, minimize $J(w, b)$ by adjusting $w$ and $b$ → so that predicted values are as close as possible to actual values.
  - $w$ and $b$ are parameters of the model, adjusted as the model learns from the data. They’re also referred to as “coefficients” or “weights”.

### 3. Cost Function Intuition
> When the cost is relatively small, close to zero, it means the model fits the data better than with other choices of $w$ and $b$. Since $J(w, b) \geq 0$, the minimum possible value of the cost function is 0, which occurs only when the predictions perfectly match the actual values.

- Normal:
    - Model: $f_{w,b}(x) = wx + b$
    - Parameters: $w, b$
    - Cost Function: $J(w, b) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w, b}(x^{(i)}) - y^{(i)})^2$
    - Goal: $\min_{w,b} J(w, b)$
- Simplified:
    - Model: $f_{w}(x) = wx$ (b = 0)
    - Parameters: $w$
    - Cost Function:
        - $J(w) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w}(x^{(i)}) - y^{(i)})^2$
        - $J(w) = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2$
    - Goal: $\min_{w} J(w)$

- Simplified Cost Function
    - $f_{w}(x)$ Graph
        - horizontal axis: $x$, vertical axis: $y$
        - for fixed $w$, function of $x$
    - $J(w)$ Graph
        - horizontal axis: $w$, vertical axis: $J(w)$
        - function of $w$ => parameter
    - Example (<u>The answer is right when $w = 1$ and $b = 0$.</u>)
        - $m = 3$, $w = 1$
            - $f_{w}(x) = \hat{y}$
                - $f_{1}(1) = 1$
                - $f_{1}(2) = 2$
                - $f_{1}(3) = 3$
            - $J(w)$
                - $J(1) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w}(x^{(i)}) - y^{(i)})^2 = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2 = \frac{1}{2 * 3}(0^2 + 0^2 + 0^2) = 0$

        - $m = 3$, $w = 0.5$
            - $f_{w}(x) = \hat{y}$
                - $f_{0.5}(1) = 0.5$
                - $f_{0.5}(2) = 1$
                - $f_{0.5}(3) = 1.5$
            - $J(w)$
                - $J(0.5) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w}(x^{(i)}) - y^{(i)})^2 = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2 = \frac{1}{2 * 3}((0.5-1)^2 + (1-2)^2 + (1.5-3)^2) \approx 0.58$

        - $m = 3$, $w = 0$
            - $f_{w}(x) = \hat{y}$
                - $f_{0}(1) = 0$
                - $f_{0}(2) = 0$
                - $f_{0}(3) = 0$
            - $J(w)$
                - $J(0) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w}(x^{(i)}) - y^{(i)})^2 = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2 = \frac{1}{2 * 3}((0-1)^2 + (0-2)^2 + (0-3)^2) \approx 2.3$
                
        - $m = 3$, $w = -0.5$
            - $f_{w}(x) = \hat{y}$
                - $f_{-0.5}(1) = -0.5$
                - $f_{-0.5}(2) = -1$
                - $f_{-0.5}(3) = -1.5$
            - $J(w)$
                - $J(-0.5) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w}(x^{(i)}) - y^{(i)})^2 = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2 = \frac{1}{2 * 3}((-0.5-1)^2 + (-1-2)^2 + (-1.5-3)^2) \approx 5.25$

        - Graphs looks like:
            - ![F_{w}(x) Graph](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/ai/concept/ai_cost_function_intuition_fwx_wx_graph.png)
            - ![F(w) Graph](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/ai/concept/ai_cost_function_intuition_fw_w_graph.png)
        - Choose $w$ to minimize $J(w)$ => $\min_{w}J(w)$ => $w = 1$
            - More general case: $\min_{w,b}J(w,b)$

---

## Terminology
- `Training set`: Dataset used to train the model
- `x`: Input variable / Input feature (can be a single value or a vector of features)
- `y`: Output variable / Target variable / Output Targets
- `m`: Number of training examples
- `(x, y)`: A single training example (e.g., (x=1, y=50))
- `(x^(i), y^(i))`: The i-th training example (e.g., (x^(1), y^(1)))
    - *Note: The superscript (i) is an index, not an exponent (x^(2) ≠ x²).*
- `f`: Function / Hypothesis / Model (maps input `x` to predicted output `ŷ`)
    - `f(x)` = function / model  
    - General notation for a function mapping input `x` to output.
    - `h(x)` = hypothesis  
    - Used in machine learning to represent the model we are training as a "prediction function".
        - **Compatibility Note:**  
            - `f(x)` and `h(x)` are almost interchangeable in Linear Regression.  
            - The difference is mostly notational: `h(x)` emphasizes that it is a hypothesis being learned, while `f(x)` emphasizes a general function.
- `f_{w,b}(x) = w x + b` (model function, simply `f(x) = w x + b` or `h(x) = w x + b`  
  (*all represent the same linear regression model*))
    - `f_{w,b}(x)` = explicit model with parameters
    - `f(x)` = general function
    - `h(x)` = hypothesis / model during training
    - In practice, `f(x)` ≈ `h(x)`; `f_{w,b}(x)` is just a concrete example with parameters.
- `ŷ (y_hat)`: Predicted output calculated by the model. The goal of training is to make `ŷ` as close as possible to `y`.
    - *Note: y vs ŷ (y-hat)*
        - `y` = Actual output / target variable / target value (ground truth), the true value we want to predict.
        - `ŷ` (y-hat) = Predicted output from the model (`f(x)` or `h(x)`)
        - Key point:
            - During training, `ŷ` may not equal `y`
            - Loss is calculated as the difference between `y` and `ŷ` to improve the model
            - During inference, `ŷ` is treated as the model's predicted result, which we use for decision-making
