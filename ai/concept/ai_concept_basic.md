# AI

## Machine Learning
- In general, the more options you give a learning algorithm to learn, the better it will perform.


## Machine Learning Algorithm
> Knowing Machine Learning Algorithms is important but what's more important is to know how to use them.

### 1. Supervised Learning
- **Practical Impact & Innovation**
    - Used the most in real-world applications.
    - Has seen the most rapid advancements and innovation.
- **Definition**
    > A method where the model learns from data that has both inputs (X) and outputs (Y).
    - `Input (X)` to `output (Y)`
        - Giving "right answers" from learning
        - The goal is to gather data, learn the trend (or relationship) between X and Y, and when you have X, produce Y.
        - `More high-quality data and a greater variety of relevant inputs generally improve the accuracy of predicting Y.`
- **Types**
    > Classification focuses on finding boundaries, whereas Regression focuses on identifying trends.
    - `Regression`
        - Used when the output Y is a continuous number.
        - Predicts a continuous number, meaning there are <u>***infinitely many possible outputs***</u>, based on existing data.
            - Example: Predicting house price from size, predicting height from age.
        - `Regression → identifying trends`
        
    - `Classification`
        - Used when the output Y is a category.
        - Predicts categories, meaning there are a <u>***limited number of possible outputs***</u>, based on existing data.
            - Example: Classifying emails as spam or not, classifying images as cat or dog, detecting cancers.
        - `Classification → finding boundaries`

### 2. Unsupervised Learning
- **Practical Impact & Innovation**
    - Used in various real-world applications such as customer segmentation, anomaly detection, and data exploration.
    - Has seen rapid advancements in clustering algorithms, dimensionality reduction, and representation learning.
- **Definition**
    > A method where the model learns from data that has **inputs (X) only**, without output labels (Y).
    - ***<u>Unsupervised learning is more suitable for situations where the input data is constantly changing.</u>***
    - Learns patterns, structures, or relationships within the data.
        - `The goal is to find hidden patterns, group similar data points, or reduce dimensions for better understanding.`
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
    - Learns from data that includes both inputs (X) and outputs (Y).
    - The model learns the relationship X → Y and can predict Y for new X.
    - Examples: Predicting house price from size, predicting height from age, classifying emails as spam or not.
- **Unsupervised Learning:**
    - Uses input data (X) only, without output labels (Y).
    - The model learns patterns, structures, clusters, or associations in the data.
    - Examples: Customer segmentation, dimensionality reduction (PCA), anomaly detection.
- **Key difference:**
    - `Supervised → requires labeled data (X + Y)`
    - `Unsupervised → works with unlabeled data (X only)`

