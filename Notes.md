
# "What is a decision tree?"

**Definition**: A decision tree is a machine learning approach that uses an inverted tree-like structure to model relationships between variables and predict outcomes.

**Structure**: It consists of decision nodes (questions) connected by branches (responses) leading to leaf nodes (outcomes).

**Applications**: Decision trees can be used for both classification (categorical outcomes) and regression (continuous outcomes) problem

# How is a classification tree built?

**Recursive Partitioning**: Classification trees are built using recursive partitioning, which splits data into smaller subsets to maximize the similarity (homogeneity) of items within each subset.

**Splitting Data**: The process involves scanning axes to determine the best split point that maximizes purity. For example, splitting loan data based on a loan amount of $40,000.

**Generalization**: After splitting, generalizations are made about future data based on the **dominant outcome** in each partition. This helps in creating decision nodes and branches in the classification tree.

**Further Partitioning**: The process can continue to create purer partitions by further splitting the data based on other variables, like annual income.

# "How do classification trees measure impurity?"

**Measures of Impurity**: Two common measures of impurity in classification trees are **entropy** and **Gini**. Entropy is used in the **C5.0 algorithm**, while Gini is used in the **CART algorithm**.

# Entropy

- Entropy quantifies the **level of randomness or disorder within a partition**. Lower entropy indicates more homogeneous partitions. The video explains how to calculate entropy using proportions of different outcomes.

$$
Entropy(S1) = \sum_{i=1}^C -P_i . \log_2(P_i)
$$

- Where S is the given data partition, C is the number of class levels, and $P_i$ refers to the proportion of the values in class level i

- **Information Gain**: The reduction in impurity (entropy or Gini) after a split is known as information gain. The algorithm chooses the split that results in the largest information gain.

## Split and combined Entropy

- When a data set is splitted, the **Entropy** is calculated for each split and then the weighted sumb of entropy is calculated.

$$ Entropy(S2) = \sum_{i=1}^n W_i.Entropy(P_i)$$

- The combined entropy is expected to be lower than the entrophy for the whole dataset. The reduction is called **Information gain** due to split.

$$ InfoGain(E) = Entropy(S1) - Entropy(S2) $$

- The higher the **InfoGain** the better the split

# Gini

- **Gini Impurity**: Gini measures **statistical dispersion and indicates how often a randomly chosen element would be incorrectly labeled**. Lower Gini values indicate purer partitions.
  
$$ Gini(S) = 1 - \sum_{i=1}^c P_i^2 $$

- Where S is the given data segment, c is the number of class levels, and $P_i$ refers to the proportion of the values in class level i.

# Regression tree : "How is a regression tree built?"

- **Recursive Partitioning**: Regression trees are built using recursive partitioning, which aims to create **child partitions with less variability than their parent partitions**.

- **Sum of Squared Residuals (SSR)**: The algorithm uses SSR to determine the best split. SSR measures the overall difference between the values in a partition and their mean.

- **Splitting Process**: The algorithm evaluates different splits and chooses the one that minimizes the SSR, thus reducing variability within the partitions.
  
$$ SSR = \sum_{i=1}^n (Y_i - \hat{Y})^2 $$

- where n is the number of items in the partition, $\hat{Y}$ is the mean of the items in the partition, and $Y_i$ is each item in the partition.

- Low SSR = less variation, closer to the mean.

- After splitting the data, SSR for each split is calculated and added later to represent total SSR for that split. The algorithm checks for each possible splits and the total SSRs, then choses the one with lowest SSR.

# Pruning

**Pruning** in decision trees is a technique used to manage the size of the tree to avoid overfitting

- **Pre-pruning**: Stops the tree growth early by setting criteria for splits, like the maximum number of features or nodes.

- **Post-pruning**: Allows the tree to grow fully and then reduces its size afterward, often using methods like **cost complexity pruning**.

- **Purpose**: Helps the tree generalize better to new data by preventing it from fitting the training data too perfectly.

# Tree Score

- The **"Tree score"** is a metric used in pruning decision trees to balance the **complexity** of the tree with its **performance**.

$$ Tree Score, T = SSR + \alpha|\hat{T}|$$

- The second term is tree complexity penalty. A penalty for the number of leaf nodes in the tree, influenced by a user-defined parameter called alpha. $\alpha$ is **complexity parameter** and $|\hat{T}|$ is the number of leaf/terminal nodes in tree T.

- **Higher alpha values favor simpler trees, while lower values favor more complex trees. The goal is to find the tree with the lowest tree score, which balances fit and complexity.**
- $\alpha$ is a hyperparameter and best value is found by hyperparameter tuning.
