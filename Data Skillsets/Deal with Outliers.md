# Deal with Outliers
```ad-resources
- [How to Deal with Outliers in Your Data](https://cxl.com/blog/outliers/)
- [Best-Practice Recommendations for Defining, Identifying, and Handling Outliers](http://www.hermanaguinis.com/ORMoutliers.pdf) (much more in details)
```
## What is an outlier
```ad-definition
**An outlier** is an observation that lies an abnormal distance from other values in a random sample from a population
```
### Origin of outliers
- There are two basic origins of outliers:
	1. they are errors (errors can occur in measurement, in data entry, or in sampling...)
	2. they are *genuine but extreme value*
### Impact of outliers
- Outliers can change the results of data analysis and statistical modeling, most common impacts:
	- They may cause significant change on the mean and standard deviation
	- They may increases the error variances and reduces the power of statistical tests
	- They may bias and/or influence estimates
	- They may also impact the basic assumption of regression as well as other statistical models
## Detecting "potential" outliers
To identify "potential" outliers, I normally prefer to use graphical methods giving their clear and intuitive properties. There are three common ways of doing:
- For detecting outliers in one variable:
	- Using [[Exploring Data Analysis#Boxplots|boxplot]]
		- e.g. ![[Pasted image 20220311113959.png|400]]
	- Using [[Exploring Data Analysis#Histograms|histogram]]
		- e.g. ![[Pasted image 20220311114107.png|500]]
- For detecting outliers in combined multiple variables:
	- Using [[Exploring Data Analysis#Scatterplots|scatterplot]]
		- e.g. ![[Pasted image 20220311114221.png|500]]
## Handling outliers
There is no straightforward way to handling outliers, but the best solution need to be tailored depend on the situation and data set. Therefore, **it is important to do a custom analysis with regard to outliers** before deciding how to handle them.
