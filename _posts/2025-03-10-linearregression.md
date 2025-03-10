# **1. Introduction to Linear Regression**

Linear regression is a statistical method that models the relationship between a dependent variable \(y\) and an independent variable \(x\) using a linear equation:

$$
\hat{y} = b_0 + b_1 x
$$

Where:
- \(\hat{y}\) is the predicted value
- \(b_0\) is the intercept
- \(b_1\) is the slope of the line

The slope \(b_1\) can be calculated using:

$$
b_1 = \rho_{x,y} \frac{\sigma_y}{\sigma_x} = \frac{\sum(x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}
$$

And the intercept \(b_0\) is calculated as:

$$
b_0 = \bar{y} - b_1 \bar{x}
$$

Where:
- \(\rho_{x,y}\) is the Pearson correlation coefficient
- \(\sigma\) is the standard deviation

---

# **2. Linear Regression Evaluation**

### **Cost Function: Mean Squared Error (MSE)**

MSE is a common metric to evaluate linear regression models, and it is also used as the cost function to optimize:

$$
J(\beta) = \frac{1}{2m}\sum_{j=1}^m (y_j - \hat{y}_j)^2
$$

Where:
- \(m\) is the number of samples
- \(y_j\) is the actual value
- \(\hat{y}_j\) is the predicted value

The factor of 2 in the denominator makes the gradient calculation easier by canceling out during differentiation.

---

# **3. Gradient Descent**

Gradient descent is an optimization algorithm used to find the coefficients (\(\beta\)) that minimize the cost function:

1. Calculate the gradient at the current point.
2. Move in a step size proportional to the negative gradient.
3. Repeat until the minimum is reached.

In linear regression, this process helps find the \(\beta\) that minimizes the Mean Squared Error (MSE).

---

# **4. Model Evaluation Metrics**

1. **Mean Absolute Error (MAE)**
2. **Mean Squared Error (MSE)**
3. **Root Mean Squared Error (RMSE)**

These metrics help assess the accuracy of the linear regression model.

---

# **5. Residual Plots**

Residuals are the differences between actual and predicted values. They should be normally distributed because we assume the error term follows a normal distribution.

---

# **6. Example Code in Python**
Create linear regression model with optimal parameters using a grid search 

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import ElasticNet

df = pd.read_csv("../DATA/AMES_Final_DF.csv")
df.head()
X = df.drop('SalePrice', axis = 1)
y = df['SalePrice']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.1, random_state = 101)

# split the train and test dataset
scale = StandardScaler()
X_train_scaled = scale.fit_transform(X_train)
X_test_scaled = scale.transform(X_test)

# use Elastic net
base_elastic_net_model = ElasticNet()
param_grid = {'alpha': [0.1, 1.5, 10, 50, 100], 
			  'l1_ratio':[0.1, 0.5, 0.7, 0.95, 0.99, 1]}
grid_model = GridSearchCV(estimator=base_elastic_net_model,
							param_grid = param_grid,
							scoring = 'neg_mean_squared_error', 
							cv = 5, verbose = 0)
grid_model.fit(X_train_scaled, y_train)
grid_model.best_estimator_

# evaluation
y_pred = grid_model.predict(X_test_scaled)
mean_absolute_error(y_pred, y_test)
np.sqrt(mean_squared_error(y_pred, y_test))

```

