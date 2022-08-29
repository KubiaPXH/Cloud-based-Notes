## Definition
```ad-tip
[[Python#copy library|Deep copy]] dataset to keep the raw data intact, in case we need to reuse.
```
### Data Cleaning
```ad-tip
Put all train and test dataset to a list -> clean them together (using `for` loop through the list) 
```
#### Checklist for a good dataset
- [ ] Check data dimension (or shape)
	- Good ratio between feature and sample size (p >> n) #dig-deeper 
- [ ] Check column names
- [ ] Check for data type
	- using `df.dtype`
	- If not correct type -> change type using `df.astype()`
	- If possible to change current type to smaller types for optimization -> change type using `df.astype()`
	- Proper categorical data-types? (Nominal or Ordinal/Label encoding)
- [ ] Check missing values and bad values
	- Is there missing values and bad values? Any pattern?
	- How to [[Deal with Missing Values|deal with missing values]]
- [ ] Check outliers
	- Are there any outliers? using *boxplot*
	- Are they real outliers? using domain knowledge
	- Whether outliers affect outcomes? -> need to be treated or not?
	- If treatment, how to deal with outliers
- [ ] Check if need transformation (log, square root, cube)
- [ ] Check for optimal feature engineering
	- Create additional features from the existing data?
	- Which feature can be removed? Multi-collinearity?
##### [[Deal with Missing Values]]
##### [[Deal with Outliers]]
### Data Wrangling
- **Tools:** Better using Python `.py` in VS Code
- remember to use `lambda` with `df.apply` -> Optimal?
- shouldn't overwrite the raw data -> create new columns to keep new data points -> (maybe) delete redundant column at the end
### Feature Engineering
```ad-definition
**Feature engineering** is the process of selecting, manipulating and transforming raw data, with domain knowledge, into features that can be used in machine learning with the purpose to improve the quality of its results.
```
## Tools
For Data cleaning and wrangling in Python, especially in structured data, we use [[Pandas library]] and [[NumPy library]] to handle and transform raw data to useful and usable data.
