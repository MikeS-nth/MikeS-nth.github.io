---
layout: post
title: "How to Do a vLookup in Python"
feature-img: '../img/sample_feature_img_2.png'
---
If you are one of the many people who, like me, are coming to Python for data analysis after having spent a lot of time working with Microsoft Excel, you will at some point find yourself saying, "How do I do a vLookup in Python?"  (Or, if you're really like me, you'll throw in a few expletives.)

Despite many search results and stackoverflow questions to the same effect, I have not found a resource that gives a straightforward, practical explanation of how to do vLookup (or it's sexier alternative, index/match).  This post is my attempt to do that.

What is vLookup?  For those of you who may be unfamiliar, vLookup is an Excel formula that allows you to populate the cells in a given column based on a column-wise (vertical) match in another spreadsheet or table.  For example, let's say I had a table with Employee ID and Employee Name, and I also had a table with a log of keycard usage over time that included the Employee ID for that keycard, but not the name.  If I wanted to update the keycard log with the employee name, I would use vLookup to match the Employee ID in the keycard table with the Employee ID in the employees table, and populate a new column in the keycard table with the Employee name matched in the Employee table.  It's hugely helpful and very commonly used.

I will describe two methods to achieve the same result in Python, using the pandas library.  (I am sure there are other wasy to do it, but I find that these are good starting points.)

### Method 1:  `.map()` with a Dictionary
In this method, you can use the `.map()` method in pandas to fill a dataframe column based on matched values in a Python dictionary.

Sticking with the example above:

```python
# First, create a dictionary with employee IDs and names
# where the key is the ID and the value is the name.
employees = {
12345: "Jean-Luc",
98766: "Deanna",
29384: "Geordi"
}
```
Then, let's say I have a dataframe of keycard logs called `logs_df` that has a timestamp and EmployeeID, but no employee name.  It might look something like this:

|Time |EmployeeID |
|:---|:---|
|07:03:52  |98766 |
|09:23:02  |29384 |
|09:52:23  |98766 |
|10:01:33  |12345 |
|13:43:43  |29384 |

Notice that I have *more rows than employee names*.  This is unsurprising for a keycard log, but it also means I am comparing different-shaped data.

To accomplish the mapping with the dictionary, `.map()` is very useful:
```python
# Match the EmployeeID field to employee name and put
# the employee name in a new column called EmployeeName
logs_df['EmployeeName'] = logs_df.EmployeeID.map(employees)

```
The output will look like this:

|Time |EmployeeID |EmployeeName|
|:---|:---|:---|
|07:03:52  |98766 |Deanna |
|09:23:02  |29384 |Geordi |
|09:52:23  |98766 |Deanna |
|10:01:33  |12345 |Jean-Luc |
|13:43:43  |29384 |Geordi


### Method 2: `.merge()` with a Left Join
What if your lookup values are in another dataframe, rather than a dictinoary?  You could certainly create a dictionary form that dataframe, but it creates unnecessary extra work.  Instead, you can use the pandas `.merge()` method with a *left join* to accomplish your match.

Let's say my employee IDs were in a dataframe, called `employees_df` that looked like this:

|EmployeeID |EmployeeName |
|:---|:---|
|98766 |Deanna |
|29384 |Geordi |
|12345 |Jean-Luc |

In this case, I can populate `logs_df` with the employee names like this:

```python
# Using the pandas .merge() method with the how='left'
# argument:
logs_df = pd.merge(logs_df, employees_df, how='left',
        left_on='EmployeeID', right_on='EmployeeID')
```
And voila, we have our desired result:

|Time |EmployeeID |EmployeeName|
|:---|:---|:---|
|07:03:52  |98766 |Deanna |
|09:23:02  |29384 |Geordi |
|09:52:23  |98766 |Deanna |
|10:01:33  |12345 |Jean-Luc |
|13:43:43  |29384 |Geordi
