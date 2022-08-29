# Exploring Data Analysis
## Resources for EDA
- [x] https://r4ds.had.co.nz/exploratory-data-analysis.html
- [x] https://www.stat.cmu.edu/~hseltman/309/Book/chapter4.pdf
- [x] [Dramatically Improve Your Exploratory Data Analysis (EDA)](https://towardsdatascience.com/dramatically-improve-your-exploratory-data-analysis-eda-a2fc8c851124)
- [ ] Chap 1 of "Practical Statistics for Data Scientist"
## Purposes for EDA
- Goal of EDA is to develop understanding the important characteristics of your data (**especially your population of interest**), which are:
	- forming and checking of assumptions (Hypothesis driven approach)
	- detection mistakes, outliers and anomalies
	- better understand the variation of variables
	- better understand covariation (or relationships) among feature (explanatory variables) and outcome variable
	- determine if the data on hand is sufficient to answer a the question? 
		- if yes, EDA helps the preliminary selection of appropriate models. 
		- if no, EDA provides suggestions for further data collection
	- find in news opportunities in the data as EDA can give us surprised insights about data -> new information -> new opportunities.
### Hypothesis driven approach
```ad-definition
Hypothesis driven approach consists in establish hypothesis (educated guesses) about the varibles behaviors and their relationships, then focus on using data to prove (or disprove) them.
```
- *Advantages:*
	- Reduce effort -> increase speed: Limit amount of data used and number of tests to some hypothesis
	- Reduce risk: If you're right succeed fast, if you're wrong you fail fast
- *Disadvantages:*
	- Very objective -> risk of falling to blind spot: Your hypothesis are based one your knowledge which are limited -> reduce the chance of to get surprising insights.
## EDA process
- EDA is an iterative but **explorational** cycle:
	1. Generate questions about your data (**feel free to ask questions to your data**)
	2. Search for answers by visualizing, transforming and modelling your data
	3. Use what you learn to refine your questions and/or generate new questions
- Two useful types of questions (but not exhaustive):
	1. What type of variation occurs within my variables?
	2. What type of covariation occurs between my variables?
## EDA types
- EDA is general cross-classified in two ways: graphical or non-graphical and univariate or multivariate (usually bivariate)
	- ![[Pasted image 20220210172902.png|900]]
```ad-tip
It is almost always a good idea to perform univariate EDA on each of the components of a multivariate EDA before performing the multivariate EDA.
```
## Variation within a variable
- **Variation** is the tendency of the values of a variable to change for measurement to measurement.
- Best way to understand the pattern of variation of a variable is to **visualize the distribution of the variable's values.** 
- Normally we visualize distributions using *bar charts*, *histograms*, *density charts* and *boxplots* :
	- Further questions:
		- Fix our expectations? Why?
		- Not fix our expectations? Why?
		- New discoveries or unexpected things/patterns? Explanation?
		- Misleading? Anything is not right with the data?
	- Detection clusters -> in one variable using *histograms* or *density charts*
		- Describe the clusters? Explain the clusters? 
		- Misleading? Anything is not right with the data?
	- [[Deal with Outliers#Detecting potential outliers|Detection outliers]] -> using *boxplots*
		- Describe the outliers? Explain the outliers? 
		- Is the outliers affect the results of the analysis? (repeat your analysis with and without the outliers)
			- No -> remove outliers
			- Yes -> modification the weight of outliers or replace outliers with robust techniques(?)
### Univariate non-graphical EDA
- Data is usually the observations (measurements) of characteristics (attributes or variables) of (an) object(s). **These measurements can be seen as a "sample distribution" of the variable which in turn more or less represents the "population distribution" of the variable.**
```ad-important
Usual goal of univariate non-graphical EDA is:
- Better appreciate the "sample distribution"
- Some tentative conclusions about the "population distribution" based on "sample distribution"
- Outlier detection
```
#### Categorial data
- Interest characteristics of categorial data: **range of values** and **frequency of each value** -> Simple tabulation is the best univariate non-graphical EDA for categorial data.
- e.g. ![[Pasted image 20220221154841.png|500]]
#### Quantitative data
```ad-caution
**"Sample distribution" is not "population distribution"**, especially when sample is not randomly selected. And even for randomly selected samples, their "sample distribution" are different from each other -> The characteristic of our **randomly observed sample** are not inherently interesting, expect to the degree that they represent the population.
```
- Using **sample statistics** to investigate the characteristics of a sample distribution:
	> **Remember:** as (random) samples' distribution varies, therefore their sample statistics also vary (we have sample stats' distribution to represent it variation)
	- Center tendency: *mean*, *median* and *mode*
		- Definition: "Location" of a distribution has to do with typical or middle values
		- *Mean*: sum of all of the data values divided by the number of values
			- if we have n data labeled x1 -> xn: ![[Pasted image 20220221160747.png|120]]
		- *Median*: the middle value (the 50th percentile) after all values are put in an ordered list, if even number of values -> median = average of two middle values.
			- median is robust as its value is less affected by outliers or change in the data (compared to mean)
		- *Mode*: the most likely or frequently occuring value
		- Skewness and center tendency:
			- Mean < Median < Mode: Negatively skewed (Tail on the negative side)
			- Mode < Median < Mean: Positively skewed (Tail on the positive side)
			- ![[Pasted image 20220221162915.png|600]]
	- Spread: *variance*, *standard deviation* and *interquartile range*
		- Definition: Measurement of the spread (how far away from the center) of a distribution.
		- *Variance* of a sample is defined as the mean squared deviation (deviation = ![[Pasted image 20220221164325.png|80]]).
			- if we have n data labeled x1 -> xn: ![[Pasted image 20220221164204.png|150]]
			- why divide by (n-1)? because (n-1) denominator help the sample variance be come an unbiased estimator of the population variance ([proof](https://web.ma.utexas.edu/users/mks/M358KInstr/SampleSDPf.pdf)).
				- (n-1) is also the *degree of freedom* (df)
			- **Attention:** Distinguish between sample variance ![[Pasted image 20220221165847.png|20]] (vary from sample to sample) and population variance ![[Pasted image 20220221165917.png|20]] (single, fixed) 
		- *Standard deviation* (sd): is simply the square root of the variance.
			- In normally distributed data, approximately:
				- 68.3% of the values lie within 1 sd of the mean
				- 95.4% of the values lie within 2 sd of the mean
				- 99.7% of the values lie within 3 sd of the mean
		- *Interquartile range* (IQR):
			- *quartiles*: the quartiles of a sample (or a population) are the three values which divide the distribution or observed data into even fourths.
			- *interquartile range* (IQR) = third quartile (Q3) - first quartile (Q1) -> half of the "middle" values 
			- IQR is a more robust measure of spread than variance and sd.
			- For normally distributed data only, the IQR is ~ 4/3 times the sd.
	- Skewness & Kurtosis:
		- Skewness is a measure of asymmetry of probability distribution of a random variable around its mean.
			- ![[Pasted image 20220221162915.png|600]]
		- Kurtosis is a measure of "peakedness" (or flatness) relative to a Gaussian shape (or Normal distribution).
			- ![[Pasted image 20220221175006.png|600]]
		- How to calculate [skewness and kurtosis in Pandas](https://medium.com/@atanudan/kurtosis-skew-function-in-pandas-aa63d72e20de)
### Univariate graphical EDA
#### Histograms
- **Histogram** is a barplot in which each bar represents the frequency (count) or proportion (count/total count) of cases for a range of values (or a categorical variable) -> give us idea about the distribution of the variable.
	- *bin* is the range of data for each bar.
	- histogram can be used for spotting outliers
- Best practices:
	- Good idea to change try different bin sizes -> as bin sizes affect the shape of the histogram (especially for small samples)
		- e.g. ![[Pasted image 20220221181448.png|600]]
	- Also good idea to look at multiple samples from the same population -> how the distribution varies sample by sample
		- The distribution varies quite high for smaller sample size -> **beware of incorrect impression if working with small sample**
			- e.g. ![[Pasted image 20220221181548.png|600]]
```ad-important
Histogram is the only univariate graphical technique which makes sense for categorical data
```
#### Boxplots
- Boxplots are very good at representing information about the central tendency, symmetric, skew and outliers (attention to misleading about aspect such as [multimodality](https://en.wikipedia.org/wiki/Multimodal_distribution)). They are robust as they rely on robust statistics like median and IQRs.
- Components of a boxplot:
	- ![[Pasted image 20220222151256.png|400]] ![[Pasted image 20220222161525.png|400]]
	- *whisker*: the most extreme data point that is less than 1.5 IQRs beyond corresponding hinge.
	- *outliers*: any data value locates beyond its corresponding whisker.
	- *extreme outliers*: value locates more than 1.5 IQRs beyond its corresponding whisker (3.0 IQRs its corresponding hinge), extreme outliers are sometimes plotted differently than outliers.
```ad-caution
- Superimposed when plotting outliers.
- **A boxplot outlier is just a suggestion that the point may be a mistake**, but doesn't mean the point has problems by itself.
- Number of boxplot outliers depends strongly on the size of the sample.
```
- *fat tails* (positive kurtosis): is used to describe the situation where a histogram has a lot of values far from the mean relative to a Normal distribution.
	- ![[Pasted image 20220222162237.png|400]]
#### Quantile-normal plots (QN Plots or Normal QQ Plots)
- QN plot is used to see how well a particular sample follows a particular theoretical distribution.
```ad-caution
Do not confuse a QN plot with a simple scatter plot of two variables
```
- The more aligned the dots in QN plot to the diagonal (normal distribution) the more likely the sample is normally distributed.
	- e.g. ![[Pasted image 20220222175133.png|600]]
- For [clearly explained](https://www.youtube.com/watch?v=okjYjClSjOg) and [how to interpret a QQ plot](https://stats.stackexchange.com/questions/101274/how-to-interpret-a-qq-plot)
```ad-tip
Other (quite obvious) alternative to consider it to plot sample's density distribution and normal distribution in the same graph to compare!
```
- Important Question: **If the data (sample) doesn't fit normal distribution, which distribution does it fit?**
## Covariation between variables
- **Covariation** is the tendency for the values of two or more variables to vary together in a related way.
- Quick summary for revealing the relation between:
	- a categorical and a continuous variable, using a *multi-density chart* -> *boxplot*
	- two categorical variables (effect on a continuous variable?), using a *heatmap*
	- two continuous variables, using a *scatterplot*
### Multivariate non-graphical EDA
- Multivariate non-graphical EDA techniques show the relationship between two or more variables.
#### Cross-tabulation
- *Cross-tabulation* is **very useful** for categorical data, the filling can be count or percentage.
	- e.g. ![[Pasted image 20220224145531.png|400]]
#### Univariate statistics by category
- It can be useful to produce a variety of univariate statistics for the quantitative variable for each categorical variable -> to see if and how categories affect the distribution of quantitative variable.
#### Correlation and covariance matrices
- *Sample covariance* is a measure how much two variables "co-vary", how much (and in what direction) should we expect one variable to change when the other changes.
	- Formula:  ![[Pasted image 20220224150459.png|300]]
	- Sign of covariance:
		1. covariance > 0: if one measurement is above the mean, the other will probably also be above the mean
		2. covariance < 0: if one measurement is above the mean, the other will probably also be below the mean
		3. covariance = 0: two variables vary independently of each other
	- However, as covariances tend to be hard to interpret -> use *correlation* instead! 
- *Sample correlation* is equal to sample covariance divide by the product of the standard deviation of two variables
	- Formula: ![[Pasted image 20220224153756.png|200]]
	- Sample correlation is widely used as its value always varies between -1 and + 1 ([proof](https://sebastiansauer.github.io/why-abs-correlation-is-max-1/)), with:
		- correlation = - 1: "perfect" negative correlation (e.g. linear function with negative slope)
		- correlation = + 1: "perfect" positive correlation (e.g. linear function with positive slope)
		- correlation = 0: two variables are uncorrelated
- Most common non-graphical EDA technique is to calculate all the pairwise correlations and assemble them into a matrix (or correlation matrix heatmap).
	- e.g. ![[Pasted image 20220224154322.png|700]]
### Multivariate graphical EDA
#### Univariate graphs by category
- Side-by-side boxplots (or violinplots) are the best graphical EDA technique for examining:
	1. The relationship between a categorical variable and a quantitative variable.
	2. The distribution of the quantitative variable at each level (or range) of the categorical variable
	- e.g. ![[Pasted image 20220224155321.png|400]]
#### Scatterplots
- Scatterplot is a basic EDA technique using to investigate the relation between two quantitative variables (with outcome variable is almost always putted in y-axis)
	- e.g. ![[Pasted image 20220224155744.png|400]]
## From pattern to relationship
- **Patterns is clues for relationships**, if a systematic relationship exists between two variables it will appear as a pattern in the data.
- If patterns are spotted, we should consider:
	- Could this pattern comes from a relationship or coincidence?
	- If there is a potential relationship -> how can we describe it? how strong it is?
	- Might other variables affect the relationship?
	- Does that relationship persist when we look at subgroup of data?  
