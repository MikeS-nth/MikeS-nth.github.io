---
layout: post
title: "Pandas pd.read_csv: Understanding na_filter"
feature-img: '../img/sample_feature_img_3.png'
---

The pandas library for Python is extremely useful for formatting data, conducting exploratory data analysis, and preparing data for use in modeling and machine learning.

One of the most common formats of source data is the comma-separated value format, or .csv.  Spreadsheet programs like Microsoft Excel do a pretty good job of letting you work with .csv files natively without having to worry about things like data types.  To work with these files in Python, the pandas library offers a very useful function `pd.read_csv()` which not only parses the .csv into a dataframe, but also gives you more granular control to *how* it's parsed.

Full details on the arguments for `pd.read_csv` can be found in the documentation [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html).

I want to focus on one particular argument: `na_filter`, which defaults to `True` and controls how pandas parses null values in the .csv file.  Recently, I had been working on some projects where I had it set to `na_filter=False`, which led to unexpected errors in my code.  Debugging the issues led to a better understanding of `pd.read_csv` and especially the `na_filter`.

When you call `pd.read_csv` on a .csv file, the `na_filter` argument looks for values in the file and identifies any that are likely to be NaN, such as blank cells or various iterations of "NA" ("N/A", "NA", "NaN", etc. See the [documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html) for details).  For the corresponding value in the data frame, it places a NaN value.

This is obviously quite useful, and is the behavior we would typically want.

Why would we want to set it to `na_filter=False`?  One reason is that if we already know our data has no NAs and the file is very large, this method can be faster.  Another reason is that you may want to keep strings like "NA" based on your use case.  For example, if "NA" is used as shorthand for North America.

HOWEVER a word of caution:  If you use `na_filter=False` and there *are* NA values in your .csv file, they will appear as blank in your dataframe, but will be *invisible to null functions*.

For example:

```python
import pandas as pd
# Import the csv with na_filter off
df = pd.read_csv("my_file.csv", na_filter=False)
# Show the first two lines of the df
df.head(2)
>>> [col1, col2, col3
     1.5  ,     , foo
         ,  bar,    ]
# Looks like my df has null values.  Let's see how many:
df.isnull().sum()
>>> col1   0
    col2   0
    col3   0
```
Clearly, that is not correct and creates issues.  Being able to quickly identify and deal with null values is critical.  You can fix this with `df.col1.replace('', np.nan)`, but that's a hacky workaround.  Better to avoid it unless your really need to not filter NAs.

It also creates another problem with column data types:

```python
df.col1.dtype
>>> col1     object
```
What is happening here is that, despite col1 containing a float (and let's say for sake of argument that all non-NA values in the column are floats), pandas is treating it as an object.

This can really get in the way if you need to work with the entire column numerically.  Furthermore, calling `df.col1.astype(float, inplace=True)` does not work on the blank values, and you are still left with an object type column.

In contrast, if `na_filter=True`, col1's type would be float, not object, and I would be able to perform numerical transformations on the column despite the NaN values.

This is one of those things I discovered by accident as a result of debugging vexing errors on what seemed to be pretty simple code.  

My conclusion:  unless you have a very specific use case where you need to turn off `na_filter`, then keep the default value.
