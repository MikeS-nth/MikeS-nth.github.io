---
layout: post
title: "Stratifying the Target Variable for Multi-Linear Regression"
---
Sometimes when creating a multi-linear regression model, it's wise to stratify the `y` (target) variable when you split your training and testing data from the total sample (train/test/split).  Why would we do this?  If you have `y` data that is not normally distributed, you may have a situation where your random samples of your sample might not be sufficiently representative of the sample.  Meta!

In other words, you could have a situation where your training and/or testing sets (which are samples taken from your overall sample) look meaningfully different from the overall sample.  If that were the case, you run the risk of having a "garbage in, garbage out" situation, and your model may perform poorly.  

Stratifying is a common way to address this.  Essentially, stratifying is a way to ensure your ostensibly random sample is a representative sample.  

Usually, this comes into play for categorical variables.  In simple terms, the procedure is to sample in such a way that a representative selection from all categories are included in the training and testing sets.

To do this in Python using pandas and scikit-learn:

```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split

# Create training and testing samples from dataset df, with 30% allocated to the testing sample (as is customary):

X_train, X_test, y_train, y_test = train_test_split(df, y, test_size=0.3, stratify=y)

# The last argument `stratify` tells the function to stratify the target variable `y` so that the random sample is more representative of the full sample when `y`.
```

BUT--what do we do if your `y` is a continuous numerical variable, rather than a categorical variable?  Turns out that if we try the same syntax above, it throws an error.  This is because `train_test_split` doesn't know how to split up the sample unless you tell it what the "categories" are.

After a lot of time querying google, stackoverflow, and others more experienced than me, here's a solution I found.  The method is to trick Python into interpreting your continuous numerical `y` variable as a categorical variable instead.  How?  By creating bins, and passing your `y` variable into an ndarray containing those bins and the corresponding values.

In Python (with same libraries loaded as in the prior code snippet):

    # Create the bins.  My `y` variable has 506 observations, and I want 50 bins.
    bins = np.linspace(0, 506, 50)
    # Save your Y values in a new ndarray, broken down by the bins created above.
    y_binned = np.digitize(y, bins)
    # Pass y_binned to the stratify argument, and sklearn will handle the rest
    X_train, X_test, y_train, y_test = train_test_split(df, y, test_size=0.3, stratify=y_binned)

There you have it: stratification of a continuous numerical target value for multi-linear regression!
