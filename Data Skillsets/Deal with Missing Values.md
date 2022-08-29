# Deal with missing value
```ad-important
**BIG IDEA:** We need to deal with missing values (delete or impute) in a way that we don't introduce bias to the data set, which means that **the treated data set (by deletion or imputation) still keep the same statistical properties as the raw data set.**
```
```ad-info
**Resources:**
- [A Guide to Handling Missing values in Python](https://www.kaggle.com/parulpandey/a-guide-to-handling-missing-values-in-python/notebook)
- [How to Handle Missing Data](https://towardsdatascience.com/how-to-handle-missing-data-8646b18db0d4)
- [Flexible Imputation of Missing Data - 2nd Edition](https://stefvanbuuren.name/fimd/)
```
![[#Proper methods for each reason of missingness]]
## Reason for missing values
Understanding why and how data is missing is important for choosing the right method to deal with missing data. There are three possible reasons ([ref](https://www.ncbi.nlm.nih.gov/books/NBK493614/) or [other ref](https://stefvanbuuren.name/fimd/sec-MCAR.html)):

![[Pasted image 20220302142908.png|600]]
1. Missing Completely at Random (MCAR)
	- The missing values of the variable(X) are independent of the other variables (observed or unobserved) or the variable (X) itself. In other words, **there is no particular reason for the missing value.**
	- In this case, the missing data only reduce the analyzable sample (consequently the statistical power), but do not introduce bias -> the data remain can be considered a simple random sample.
	- However, MCAR is generally regarded as unrealistic assumption.
2. Missing at Random (MAR)
	- The missing values are systematically related to the other observed features but not the unobserved features.
	- In this case, analyses of the remain data set (after exclude missing observations) may result a bias -> but we have method to reduce these biases.
3. Missing not at Random (MNAR)
	- The missing values of the variable are systematically related to the unobserved features (events or factors which are not measured by researcher) or the variable itself with unobserved missing value (e.g. obesity people are more unlikely to reveal their weight).
	- In this case, analyses of the remain data set (after exclude missing observations) may result a bias and this issue, different from MAR case, can't be addressed in the analysis.
	- For MNAR, the missing values are harder to handle as we need to find more data about the causes for the missingness (to turn it to MAC).
## Identify the reason for missing
- [ref](http://dept.stat.lsa.umich.edu/~jerrick/courses/stat701/notes/mi.html), look for "Determining which type of missingness"
```ad-caution
There is no statistical way to determine which categorical your data will fall
```
- To gain some insight (for making reasonable guess or assumption), we begin with MAR assumption and try to find the correlation between missing values of the variable and observed variables, their values or their missing point, itself included. 
	- *Method:* create new missing variables for variables have missing values (e.g. age_missing = 0 is the value of age is missing and = 1 is not) -> run a logistics model and see if any coef is significant.
- If that kind of correlation exists then missing data is MAR, else it can be MCAR as MNAR is hard to identify because it is related to unobserved variables (There is nothing in the data that can inform MNAR)
## Treating missing values
After identify the reason (or pattern) in missing values, there are two possible way to treat them: Deletion or Imputation ([ref](https://stefvanbuuren.name/fimd/sec-simplesolutions.html))
### Deletion
```ad-caution
Deletion is not really recommended as it is likely to result in loss of information from the data set -> We should delete the missing values if their propotion is very small
```
![[Pasted image 20220302161307.png|600]]
#### Listwise Deletion
```ad-definition
**Listwise Deletion** (or Dropping rows) will eliminates all observation with at least one missing values on the analysis variable
```
- *in Python:* using `df.dropna()`
- *Advantages:* 
	- Convenience 
	- If data is MCAR, listwise deletion produces unbiased estimates of means, variances and regression weights.
- *Disadvantages:*
	- Potential wasteful as it deletes a lot of observation
	- If data is not MCAR, listwise deletion can severely bias estimates of means, regression coefficients and correlations.
	- Listwise deletion can introduce inconsistencies in reporting as different analysis on the same data are often based on different subsamples (which have fewer variables the total number of variables in the data set)
#### Pairwise Deletion
- *Definition:* **Pairwise Deletion** is the method calculated the means and (co)variances on all observed data. In other words, only missing values (not rows) are left out.
	- The mean and variance of a variable is calculated based on all observed data (missing data excluded)
	- The correlation (or covariance) of variable X and Y is calculated based on all observations which have both X and Y non-missing.
- *in Python:* using normal `DataFrame` methods without modification
- *Advantages:*
	- Simple, using all available information
	- Under MCAR -> unbiased estimates
- *Disadvantages:*
	- If not MCAR -> estimates can be biased.
	- Ok for simple descriptive statistics but not so reliable to proceed the calculation for more complicated procedures or statistics.
#### Dropping Entire Column
- **Dropping entire column** is super rarely used as it needs to meet strict conditions:
	1. column contains a lot of missing values (rule of thumbs >80%?)
	2. the variable (column) is not significant important for the analysis.
- *in Python:* using `df.drop()`
### Imputation
- **Imputation** refers to replacing missing data with substituted values. There are several ways to impute values (figure below), which are used depend on the nature of the problem.
![[Pasted image 20220302171158.png|600]]
#### Imputing with a constant (univariate)
- A constant can be: mean ([example](https://stefvanbuuren.name/fimd/sec-simplesolutions.html), look for 1.3.3), median or mode.
- *in Python:* using `df.fillna()`
- Using imputing with a constant, mean for instant:
	- will underestimate (reduce) variance
	- will disturb relations btw variables
	- will bias any estimate
- *Imputation with a constant (e.g. mean) may be can only be used when a very small number of values are missing, but it should be avoided in general.*
#### Imputing using Time Series techniques
The imputing problem in Time Series can be treated in a particular way compared to other imputing problems, three basic techniques are:
- LOCF (Last observation carried forward) or `ffill`
- NOCB (Next (valid) observation carried backward) or `bfill`
- Linear Interpolation method
##### `ffill` and `bfill`
- *in Python:* using `df.fillna(method = 'ffill' or 'bfill'`
- *Advantages:* 
	- `ffill` and `bfill` method are convenient
	- they generate a complete dataset
- *Disadvantages:*
	- their outcome is dubious -> can generate bias even under MCAR
- These methods should only use when the missing values happen in very short time, as a quick fix.
##### Linear Interpolation
- **Linear interpolation** means to estimate a missing value by connecting dots a straight line in increasing order.
- *in Python:* using `df.interpolate()`
- Linear interpolation works well for a time series with some trend but not for seasonal data
#### Advanced imputing techniques
- Advanced imputing techniques use ML algorithms to impute the missing value. 
- These techniques are also multivariate as they also used other variables in the imputing process, different from above techniques which only use the missing data variable as input for imputing. 
- There are two main advanced imputing techniques: 
	- K-Nearest Neighbor (KNN) Imputation
	- **Multiple Imputation by Chained Equations (MICE)**
	- **Maximum Likelihood Imputation (MLI)** 
##### KNN Imputation
```ad-resources
[Brief introduction](https://towardsdatascience.com/the-use-of-knn-for-missing-values-cf33d935c637) or in [more details](https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-016-0318-z) with [example in Python](https://machinelearningmastery.com/knn-imputation-for-missing-values-in-machine-learning/)
```
- KNN imputation is based on the assumption that a missing point value can be approximated by the values of the points that are closest to it, based on other variables.
- *in Python:* using [`KNNImputer`](https://scikit-learn.org/stable/modules/impute.html#nearest-neighbors-imputation) from `sklearn.impute`
	- e.g. ![[Pasted image 20220311075305.png|450]]
- *Advantages:* #dig-deeper 
- *Disadvantages:* #dig-deeper 
##### Multiple Imputation by Chained Equations (MICE)
```ad-resources
[Brief introduction](https://stefvanbuuren.name/fimd/sec-nutshell.html) or in [a lot more details](https://stefvanbuuren.name/fimd/ch-mi.html)
```
```ad-info
May be better to learn ML before using MICE -> to better understand!
```
- Multiple Imputation is not accepted as the best general method to deal with incomplete data (which is considered MAR) in many field
- MICE's procedure 
	- There are three main steps in multiple imputation: imputation, analysis and pooling.
	- Schema: ![[Pasted image 20220310165839.png|500]]
	 1. Imputation Stage: create several complete versions of data by replacing the missing values by plausible data values (usually using regression).
		- The process can be broken down to four general steps ([sources](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3074241/)):
			- *Step 1:* A simple imputation, such as imputing the mean, is performed for every missing value in the dataset. These mean imputations can be thought of as “place holders.”
			- *Step 2:* The “place holder” mean imputations for one variable (“var”) are set back to missing.
			- *Step 3:* The observed values from the variable “var” in Step 2 are regressed on the other variables in the imputation model, which may or may not consist of all of the variables in the dataset. In other words, “var” is the dependent variable in a regression model (various regression models, e.g. linear regression, stochastic linear regression, logistic or poison regression... can work) and all the other variables are independent variables in the regression model.
			- *Step 4:* The missing values for “var” are then replaced with predictions (imputations) from the regression model. When “var” is subsequently used as an independent variable in the regression models for other variables, both the observed and these imputed values will be used.
			- *Step 5:* Steps 2–4 are then repeated for each variable that has missing data. The cycling through each of the variables constitutes one iteration or “cycle.” At the end of one cycle all of the missing values have been replaced with predictions from regressions that reflect the relationships observed in the data.
			- *Step 6:* Steps 2–4 are repeated for a number of cycles, with the imputations being updated at each cycle.
		- Also a clear explanation how the MICE work is provided in [this video](https://www.youtube.com/watch?v=WPiYOS3qK70) (begin at 7:21)
	2. Analysis Results: analyze and estimate the parameters of interest from each imputed dataset
	3. Pooled Results: pool the all parameter estimates into one estimate, and to estimate its variance.
- *in Python:* using [`IterativeImputer`](https://scikit-learn.org/stable/modules/impute.html#multivariate-feature-imputation) for `sklearn.impute`
	- e.g. ![[Pasted image 20220311080416.png|450]]
- *Advantages:*
	- Produce consistence and unbiased estimates on MAR (and of course MCAR) dataset, which means if it is done properly pooled estimates are unbiased and have the correct statistical properties (compared to the population)
- *Disadvantages:* 
	- Take a long time to be done on a big dataset, which has a lot of features and observations.
##### Maximum Likelihood Imputation (MLI)
```ad-resources
For [more details of MLI](https://www.kaggle.com/residentmario/simple-techniques-for-missing-data-imputation/notebook)
```
- **Maximum likelihood estimation** is a method that determines values for the parameters of a distribution of interest, in such the way that it maximizes the likelihood function of the given data for that distribution (A clear animated explanation can be found [here](https://www.youtube.com/watch?v=XepXtl9YKwc))
- Maximum likelihood is maximum likelihood estimation applied to missing data:
	1. Build a maximum likelihood estimator with *the complete records in the data set as your predictor variables* and *the variable containing missing values as your target*
	2. For each record containing missing data, draw its value using the parameterized distribution generated by the estimator.
- *In Python:* There is probably no off-the-shelf MLI in Python, but there is a way to build one using the principal procedure.
- *Advantages:*
	- Produce consistence and unbiased estimates on MAR (and of course MCAR) dataset, its performance is relatively equivalent to the MICE.
- *Disadvantages:*
	- The result of this method depends on the probability distribution of your estimator, which again depend on your choice (e.g. normal distribution, Bernoulli distribution, multimodal distribution...) -> there is no "standard" maximum likelihood estimator imputation technique.
### Proper methods for each reason of missingness
- If data is MCAR: 
	- Complete case analysis is valid
	- MICE and MLI is valid
- If data is MAR: only MICE and MLI will work (bonus: why [MLI > MICE](https://statisticalhorizons.com/wp-content/uploads/MissingDataByML.pdf) but when [MICE > MLI](https://missingdata.org/why-multiple-imputation-is-better-than-maximum-likelihood/))
- If data is MNAR: there two options
	- Option 1: *nothing* will work
	- Option 2: try to change MNAR to MAR, which called an "inclusive missing data strategy"
		- Try to measure the dummy missing variable with a ton "random" of variables ("auxiliary variables") if there still are other variables available
		- If there is some correlation somewhere btw dummy missing variable and auxiliary variables -> MNAR becomes MAR -> apply MICE methods (MLI is more tricky in this situation)
		- *Notice:* Unlike with regression, there is *no disadvantage* to including a ton of auxiliary variables to model missing data.