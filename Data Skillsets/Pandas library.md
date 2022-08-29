- **Category:** note
- **Title:** Pandas library
- **Created date:**
- **Updated date:** 18/05/2022
- **Tag:** [[Data Analysis]] [[Data Visualization]]
- **Main refs:**
---
## Definition
```ad-definition
[`Pandas`](https://pandas.pydata.org/docs/index.html) is an open source, BSD-licensed library providing **high-performance, easy-to-use data structures and data analysis tools** for the [[Python]] programming language.
 ```
## Best practices in Pandas
- Consider the limitations and biases of your data when analyzing it
	- Imagine what will be the "best" (fictional) data which help you to answer the questions -> compared "best" data and the data we have
- Choose/Make indicators wisely to make your results understandable
- Check your work/your assumption as you go
- Watch out for small sample size
- Pay great attention to the data type
- As output of pandas operations are usually `DataFrame` or `Series` we can manipulate data directly on the output.
- Use `df.apply()` as the last option, prioritize built-in Pandas function
- **Minimally Sufficient Pandas**
	```ad-important
	**Goals:** 
	1. Sufficient (or minimum) amount of syntax learnt but (most) effective in all use cases:
		- Use simple and obvious way to complete a task
		- Use that way every single time
	2. Optimizing for highest speed and efficiency 
	```
	- Some guidelines for Minimally Sufficient Pandas:
		1. **Only use brackets (e.g. `df['name']`)** over dot (e.g. `df.name`) for selecting a column of data
		2. **Only use `df.rename()`** to rename columns or index
		3. **Only use `df.loc`  or `df.iloc`**  instead of `df.ix`
		4. **Only use `df.isna()`,`df.notna()`, `df.dropna()`, `df.fillna()`** instead of null method
		5. **Use operators (e.g. `+` or `>`) for most of the cases**, only use corresponding arithmetic and comparison methods (e.g. `df.add()`or `df.gt()` when there is no operators alternative.
		6. **Use the Pandas method (e.g. `df.sum()`)** over any built-in Python function with the same name (e.g. `sum(df)`) as Pandas methods are out-performed Python functions.
		7. **Using `df.pivot_table()`** over `df.groupby()` and `df.pivot()`
			- Flatten pivot table by using this code line ([link](https://stackoverflow.com/questions/39273441/flatten-pandas-pivot-table)):
				- ![[Pasted image 20220307140712.png|350]]
			- And use `df.reset_index()` to de-MultiIndexing
		8. **Using `df.groupby()` for quick sorting**
			- e.g. ![[Pasted image 20220308145724.png|600]]
		9. **Using `df.crosstab()` only to find relative frequency** (with `normalize` argument)
		10. **Using `df.melt()`** over `df.stack()` as it allows to rename columns and avoids MultiIndex
## Resources for Pandas
```ad-resources
- [A awesome collection of Resources for Pandas and related subjects](https://github.com/tommyod/awesome-pandas)
- [Pandas Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
```
- Intermediate Level:
	- [x] #task read and tn [Minimally Sufficient Pandas by Ted Petrou](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428) by Ted Petrou ⏫ ✅ 2022-03-07
	- [x] #task watch and tn [Data Science Best Practices with pandas (PyCon 2019) - YouTube](https://www.youtube.com/watch?v=dPwLlJkSHLo) by Data School 🔼 ✅ 2022-03-08
	- [ ] #task do [Pandas Exercises](https://github.com/guipsamora/pandas_exercises) 🔼
	- [Daniel Chen: Cleaning and Tidying Data in Pandas | PyData DC 2018 - YouTube](https://www.youtube.com/watch?v=iYie42M1ZyU) by Daniel Chen
- Advanced Level (search later in the awesome collection): 
	- [Effective Pandas: Patterns for Data Manipulation](https://www.amazon.com/Effective-Pandas-Patterns-Manipulation-Treading/dp/B09MYXXSFM) 🔽
		- [Effective Pandas](https://www.youtube.com/watch?v=zgbUk90aQ6A)  by Matt Harrison
	- Optimizing performance time:
		- [Optimizing Pandas Code for Speed and Efficiency](https://www.youtube.com/watch?v=HN5d490_KKk) by Sofia Heisler
		- [1000x faster data manipulation: vectorizing with Pandas and Numpy](https://www.youtube.com/watch?v=nxWginnBklU) by Nathan Cheever
## Data Structures in Pandas:
### Series:
[**ref**](https://pandas.pydata.org/docs/user_guide/dsintro.html#series)
```ad-info
[`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html) is a one-dimensional labeled array capable of holding any data type (integers, strings, floating point numbers, Python objects, etc.).
```
#### Basic syntax and attributes:
- Syntax: `s = pd.Series(data, index=index)`
	- `data` can be: Python `dict`, a NumPy `ndarray` or a scalar value
	- `index` is a list of axis labels (same as key in `dict`), index is \[0, ..., len(data) - 1] by default. A `Series` still have order (by `index`) within it, which is different from Python `dict`.
	- Different syntax to create a `Series`: input a `dict` as its argument
		- ![[Pasted image 20220115162116.png|350]]
- `s.name`: name attribute of a `Series`
- `s.dtype`: a `Series` has a specific data type (same as a `numpy.ndarray`)
- `s.values`: return values of `Series` as a `numpy.ndarray`
- `s.index`: return the `index` of a `Series`, we can assign it direct using a `list` on the right hand side of the statement.
#### Indexing:
- For `Series`, we do indexing using index (same as `dict`)
- `s.iloc[<number>]`: an attribute of `Series` to get the value of the `<number>` numeric positions.
	- e.g. ![[Pasted image 20220115163914.png|500]]
- Select multiple elements at once (the result is another `Series`):
	- e.g. ![[Pasted image 20220115164359.png|500]]
- Slicing in `Series`, the upper limit is also included (different in `list` where the upper limit is not included)
	- e.g. ![[Pasted image 20220115164901.png|500]]
- Boolean series indexing (or Boolean arrays indexing) is similar to NumPy
- **We can use indexing in assignment statement!**
#### Summary statistics (similar to NumPy):
- `s.mode()`: return the mode(s) of the `Series`
- `s.max()`: return the max value in a `Series`
- `s.idxmax()`: return index of the max value in `Series`
#### Arithmetic/logical operations (similar to NumPy):
#### Vectorized operations:
> `Series` can also be passed into most NumPy methods expecting an `ndarray`
- Key difference between `Series` and `ndarray` is that operation between `Series` automatically align the data based on label.
	- e.g. ![[Pasted image 20220115175645.png|200]]
	- In the result of above operation, only the values of aligned labels which exist in both `Series` are add to each other, other values of unaligned labels are marked as `NaN`.
#### Common functions in `Series`:
- [`df.astype(dtype)` or `s.astype()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html#pandas-dataframe-astype): cast a pandas object to a specified dtype.
- [`s.append()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.append.html#pandas.Series.append): concatenate two or more `Series`
- [`s.isin()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.isin.html): whether elements in `Series` are contained in *values*
- [`s.unique()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.unique.html#pandas.Series.unique): return unique values of `Series` object
- [`s.nunique()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.nunique.html#pandas.Series.nunique): return number of unique elements in the object
- [`s.eq()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.eq.html): return a boolean `Series` with value `True` for elements which both `Series` have and `False` for elements which exists in one `Series`.
#### Map() function in Pandas
```ad-resources
[A Visual Guide to Pandas map() function](https://blog.finxter.com/a-visual-guide-to-pandas-map-function/) (Pandas map multiple columns also possible)
```
### DataFrame:
```ad-definition
[**DataFrame**](https://pandas.pydata.org/docs/reference/frame.html) is a 2-dimensional labeled data structure with columns of potentially different types. DataFrame accepts many different kinds of input (1D or 2D `ndarray`, structured or record `ndarray`, `list`, `dict`, `Series` or another `DataFrame`)
```
#### Basic attributes and methods
- How to create a `DataFrame` -> see [link](https://pandas.pydata.org/docs/user_guide/dsintro.html#from-dict-of-series-or-dicts)
- `df.columns`: columns are fields of the data in the `DataFrame`, `columns` can optionally be passed. We can also think of columns is a `Series` and a `DataFrame` if a combination of several `Series`
- `df.index`: index of each entity or each row in the data table, `index` can optionally be passed and the default is \[0, len(df) - 1]
	- Count number of rows of the `DataFrame`: [several ways](https://stackoverflow.com/questions/15943769/how-do-i-get-the-row-count-of-a-pandas-dataframe), best way `len(df.index)`
	- `df.set_index()`: set `DataFrame` index using existing columns (add `inplace = True` in argument to modify the `DataFrame` in place and not create new object)
- `df.dtypes`: attribute give us the type of each `DataFrame` columns
	- `df.dtypes.value_counts()`: how many of each value types are used in this `DataFrame` 
- `df.shape`: return a tuple of shape (rows, columns) of `DataFrame`
- `df.T`: return a transposed `DataFrame`
- [`df.rename()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html?highlight=rename#pandas.DataFrame.rename): rename columns and indexes but the original `DataFrame` is still immutable
- **Subset Selection:** 
	- `df.head(n)`: return the first n (5 by default) rows in the `DataFrame`
	- `df.tail(n)`: return the last n (5 by default) rows in the `DataFrame`
	- `df.sample(n)`: return the random n (1 by default) rows in the `DataFrame`
- **DataFrame basic info/stats:**
	- `df.info()`: quick info abt the structure of the `DataFrame`
	- `df.describe()`: give a summary of stats for all numeric columns of the `DataFrame`
#### Indexing, Selection and Slicing
[**ref**](https://pandas.pydata.org/docs/user_guide/dsintro.html#indexing-selection)
##### Normal Selection
```ad-tip
**Recommended:** Always us `loc` and `iloc` to reduce ambiguity.
```
- Select column(s):
	- `df[col]`: select column -> return `Series`
	- `df[[col1,col2,...]]`: select col1 and col2... -> return `DataFrame`
	- `df.loc[:,col1:col2]`: select from col1 to col2 -> return `DataFrame`
- Select row(s):
	- By label:
		- `df.loc[label]`: select row by label (index) -> return `Series`
		- `df.loc[[label1,label2,...]]`: slice rows by index of label1 and label2... -> return `DataFrame` 
		- `df.loc[label1:label2]`: slice rows by index from label1 to label2 -> return `DataFrame`
	- By integer location:
		- `df.iloc[loc]`: select row by integer location -> return `Series`
		- `df.iloc[[loc1,loc2,...]`: select row by integer location of loc1 and loc2... -> return `Series`
		- `df.iloc[loc1:loc2]`: slice rows by integer location from loc1 to loc2-> return `DataFrame`
- Select a data point
	- `df.loc[label,col]`: select data point at row = label and column = col (substitute for `df.at()`) or `df[col][index]`
	- `df.iloc[label_loc,col_loc]`: select data point at row and column integer location (substitute for `df.iat()`) 
- Slicing a 2D `ndarray`
	- `df.loc[label1:label2,col1:col2]`: slicing a 2D `ndarray` from label1 to label2 and from col1 to col2
	- `df.iloc[label1_loc:label2_loc,col1_loc:col2_loc]`: slicing a 2D `ndarray` from label1_loc to label2_loc and from col1_loc to col2_loc
##### Conditional Selection (boolean arrays)
- `df[col_boolean_condition]`: select rows which fit the condition in the square brackets -> return `DataFrame`
- `df.loc[col_boolean_condition, 'col']`: select the columns (`col` or list of columns or range of columns) values or the rows which fit the condition in the square brackets -> return `DataFrame`
- `df.isin()`
- [`s.where(boolean_condition)`](https://pandas.pydata.org/docs/reference/api/pandas.Series.where.html): use for Series to select using boolean condition
	- e.g. ![[Pasted image 20220502110440.png|250]]
	- This function can also use to *replace values where condition False* (i.e. NaN cells)
#### Dropping (Select all except)
- [`df.drop([selected_col], axis=1)`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html): drop selected columns, axis = 1 points to columns.
	- [drop columns using columns' int location](https://stackoverflow.com/questions/20297317/python-dataframe-pandas-drop-column-using-int): `df.drop(df.columns[i], axis=1)`
- `df.drop([selected_label], axis=0)`: drop selected label, axis = 0 points to rows.
- `df = df[df['column_name'] != 'want_to_drop_value']`: drop rows have the column's value equal to want_to_drop_value
#### Modifying `DataFrame`
- Create new columns:
	- Syntax: `df.[<new_col>] = <new_Series>` -> Match all the matched index value and `NaN` for the unmatched index.
	- `<new_Series>` can be calculated by other columns of the `DataFrame` too.
	- e.g. ![[Pasted image 20220117103029.png|500]]
- Replacing values: 
	- [`df.replace(to_replace=?, value=?)`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.replace.html#pandas-dataframe-replace): replace values given in *to_replace* with *value*
	- For specific location value: select where to be replaced using `df.loc` or `df.iloc`-> assign new values
- Arithmetic operations: All the arithmetic operations in `DataFrame` is broadcasting just like `ndarray` in NumPy -> Attention to [[NumPy library#Broadcasting Operations|broadcasting condition]] in NumPy!
- [`df.rename()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html#pandas-dataframe-rename): alter axes labels or rows/ columns' name
- [`df.reset_index()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html#pandas-dataframe-reset-index): reset the index (no index at all) or a level of it.
- [Change order of a column](https://stackoverflow.com/posts/58776941/revisions) using `df.insert()`:
	- ![[Pasted image 20220530170829.png|300]]
- Change value of a set of lines' feature whose lines meet some conditions:
	- Option 1: `df.loc[condition(s), col_name] = value_to_modify` (conditions is based on lines' features, col_name is added to locate the cell)
		- ![[Pasted image 20220601151056.png|900]]
	- Option 2: Using [`np.where()`](https://numpy.org/doc/stable/reference/generated/numpy.where.html) to change the concern `Series`
		- ![[Pasted image 20220601151908.png]]
#### Iterate through all the rows in `DataFrame`
[Need to reread link](https://stackoverflow.com/questions/16476924/how-to-iterate-over-rows-in-a-dataframe-in-pandas)
#### Summary Statistics
- Summary statistics in `DataFrame` is more or less the same with `ndarray` in NumPy
#### Advanced Statistics
- [`df.corr()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html#pandas.DataFrame.corr): Compute pairwise correlation of columns -> return Correlation matrix.
#### Categorical Data in Pandas
[**ref**](https://pandas.pydata.org/docs/reference/api/pandas.Categorical.html)
#### Grouping in Pandas
- [`df.pivot_table()`](https://pandas.pydata.org/docs/reference/api/pandas.pivot_table.html): group `DataFrame` observations by unique values of a column to perform an aggregation.
	- There three components of a standard `df.pivot_table()`:
		1. *Grouping column:* Unique values form independent groups 
			- passed to the `index` and `columns` arguments (`columns` used for comparing among groups)
		2. *Aggregating column:* Column whose values will get aggregated
			- passed to the `values` argument
		3. *Aggregating function:* How the values will get aggregated (sum, min, max, mean, median...)
			- passed to the `aggfunc` argument
			- calculate different aggregations for each values -> using `dict`
				- e.g. ![[Pasted image 20220307141451.png|600]]
- [`df.grouby()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html#pandas-dataframe-groupby): Group `DataFrame` using a mapper or by a Series of columns
	- *Preferable syntax:* `df.groupby('grouping column').agg({'aggregating column': 'aggregating function'})`
		- e.g. ![[Pasted image 20220317114202.png|600]]
	- *Syntax for easy sorting*: `df.groupby('grouping column').['aggregating column']agg(['aggregating function 1','aggregating function 2',..]).sort_value('aggregating function').tail()`
		- e.g. ![[Pasted image 20220308145724.png|600]]
- `df.expanding()`
- `df.resample()`
- `df.rolling()`
#### Joining in Pandas
- [`df.merge()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html): merge `DataFrame`or named `Series` objects with a database-style join, same as JOIN in SQL (horizontal), or mapping using multiple conditions.
- [`pd.concat()`](https://pandas.pydata.org/docs/reference/api/pandas.concat.html#pandas.concat): append rows of other to the end of caller `DataFrame`, same as UNION in SQL (vertical)
#### Data Cleaning in Pandas
```ad-caution
The value of data also needs to be domain valid!
```
##### Clean missing (`NaN`) data
- **Checking missing data:**
	- `pd.isna()` (or `pd.isnull()`): we also have `df.isna()`, `s.isna()`, they return a boolean same-sized (as input) object 
		- count `NaN` values: `pd.isna(<df_or_s>).sum()` (not using here `count()` since `count()` also take count `False` value as 1)
	- `pd.notna()` (or `pd.notnull()`): we also have `df.notna()`, `s.notna()`
		- count not `NaN` values: `pd.notna(<df_or_s>).sum()`
- **Dropping missing data:**
	- [`df.dropna()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html?highlight=dropna#pandas.DataFrame.dropna) or `s.dropna()`: return a new object = input object which have already drops some `NaN` values
		- `axis`: determine if rows or columns contains missing values are removed. Default 0, drop rows or 1, drop columns.
		- `how`: Determine if removed row or column, when having at least one NA or all NA. Default 'any', drop if having any `NaN` or 'all', drop if all values are `NaN`
		- `thresh`: drop if the number of `NaN` values >= `thresh`
- **Filling missing data:**
	- [`df.fillna()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html?highlight=fillna#pandas.DataFrame.fillna) or `s.fillna()`: return a new object = input object whose `NaN` values are replaced by other value.
		- `value`: value used to fill the hole (can be scalar, `dict`, `Series` or `DataFrame` but not `list`)
		- `method`: default `None`, or 'ffill' - forward fill or 'bfill' - backward fill.
		- `axis`: default 0 - index or 1 - columns
		- `downcast`: fill `NaN` values using a `dict` as argument, the keys of `dict` match to columns and the values of `dict` match to value need to fill to `NaN`.
			- e.g. ![[Pasted image 20220117145131.png|350]]
	- [`df.interpolate()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.interpolate.html#pandas.DataFrame.interpolate): return a filled `DataFrame` using an interpolation methods
##### Clean not null data
- **Deal with abnormal data:**
	- `s.unique()`: return unique values of a `Series`
	- We can use assignment statement to replace abnormal values
	- or [`df.replace()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.replace.html?highlight=replace#pandas.DataFrame.replace): return a new `DataFrame` with replaced values
- **Deal with duplicates:**
	- [`df.duplicated()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html?highlight=duplicate#pandas-dataframe-duplicated): return boolean Series denoting duplicate rows in each columns, with arguments:
		- `subset`: only consider certain columns for identifying duplicates, default all columns (*which means the all values of 2 rows are exactly the same to consider them as duplicates*) or \<selected_columns>
		- `keep`: default 'first' - mark duplicates as `True` except the first occurrence, or 'last', or `False` - mark all duplicates as `True`
	- [`df.drop_duplicates()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html?highlight=drop_duplicates#pandas.DataFrame.drop_duplicates): return `DataFrame` with duplicate rows removed, main arguments are the same as `df.duplicated()`
- **Working with string columns:**
	```ad-info
	[Working with text in Pandas reference](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#working-with-text-data)
	```
	- `s.astype('string')`: assign the type of the series as string
	-  [`s.str.split()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.split.html?highlight=str): split a `Series` of strings around given delimiter.
	-  [`s.str.strip()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.strip.html?highlight=str%20strip#pandas.Series.str.strip)
	-  [`s.str.contains()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.contains.html?highlight=str%20contains#pandas.Series.str.contains): return boolean `Series` on whether an pattern or regex is contained with a string of the input `Series`
	-  [`s.str.replace()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace.html?highlight=str%20replace#pandas.Series.str.replace)
	- [`s.str.extract()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.extract.html): extract groups from the first match of [[Regular Expressions|regular expression]] *pat*
	- Unpack of stringtified Python objects:
		- using `import ast` library -> `ast.literal_eval()`
		- Example: 
			- first line is a stringtified list of dictionary
				- ![[Pasted image 20220308150413.png|600]]
			- using `ast.literal_eval()`
				- ![[Pasted image 20220308150511.png|300]]
```ad-recommendation
Thinking about using regex in `contains` and `replace` *only if needed*!
```
#### Quick Plot in Pandas
- [`df.plot()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.plot.html): real quick way to draw a plot using `DataFrame` data
	- `kind`: kind of plot to produce
		- 'line' : line plot (default)
    	- 'bar' : vertical bar plot
    	- 'barh' : horizontal bar plot
		- 'hist' : histogram
			- 
		- 'box' : boxplot
		- 'kde' : Kernel Density Estimation plot
		- 'density' : same as 'kde'
		- 'area' : area plot
		- 'pie' : pie plot
		- 'scatter' : scatter plot (DataFrame only)
		- 'hexbin' : hexbin plot (DataFrame only)
#### `df.apply()` and `lambda` function in Pandas #to-complete 
- [`df.apply(func, ...)`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html)  or `s.apply()`: apply a function along an axis of the ` DataFrame` or a `Series` -> [using in pair with *lambda* function](https://towardsdatascience.com/apply-and-lambda-usage-in-pandas-b13a1ea037f7).
	- `s.apply(func)`: send every values of the `Series` into the function
	- `df.apply(func, axis=1)`: send every row of the `DataFrame` into the function 
### Others:
- [`df.sort_values()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html): sort by the values along either axis
	- `by`: name or list of names to sort by.
	- `ascending`: default `True`, or `False`
- [`df.sort_index()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_index.html): sort object by index
- [`df.value_counts()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.value_counts.html): return counts of unique rows in DataFrame
	- `normalize`: return proportions (relative frequencies) rather than frequencies
- [`pd.concat()`](https://pandas.pydata.org/docs/reference/api/pandas.concat.html): concatenate Pandas object along a particular axis (horizontal or vertical)
	- `axis`: default 0, index or vertical; or 1, columns or horizontal.
- [`pd.melt()`](https://pandas.pydata.org/docs/reference/api/pandas.melt.html#pandas-melt): unpivot a `DataFrame` from [wide to long format](https://www.statology.org/long-vs-wide-data/) (or transform columns into rows )
- [`np.where()`](https://numpy.org/doc/stable/reference/generated/numpy.where.html): Ternary conditional operator for setting a value in `DataFrame`
	- ![[Pasted image 20220125151906.png|400]]
## I/O tools:
[**ref**](https://pandas.pydata.org/docs/user_guide/io.html?highlight=io#)
### CSV:
- [`pd.read_csv(<arguments>)`](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html#pandas.read_csv): read csv file, with arguments:
	- `filepath`: path to get the csv file, by default header = first line.
		- read from local computer directory: using `pd.read_csv(r'filepath')`
			- e.g. ![[Pasted image 20220118153409.png|600]]
	- `sep` or `delimiter`: delimiter to use, defaults to `,`
	- `delim_whitespace`: if delimiter is whitespace or not, defaults to `False`
	- `header`: select header for the `DataFrame`
	- `names`: assign columns' name as a list
	- `dtype`: set data type to columns
	- `index_col`: index_col is the column used as index of the `DataFrame`
	- `parse_dates`: default `False`, if `True` -> try parsing the index and other options (see documentation).
	- `na_values`: treat these values as `NaN` values
	- e.g. ![[Pasted image 20220117165809.png|330]]
- [`pd.to_csv()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html?highlight=to_csv#pandas.DataFrame.to_csv): write/save to csv file
### SQL Databases:
- [[Python#Retrieve data from Database using SQLite3|Old way to get data from SQL DB]]
- [Better way](https://towardsdatascience.com/sql-queries-in-python-51ef85b92c1e) to read DB: using `pd.read_sql()` method
	- Step 1: import `sqlachemy`
		- Syntax: `from sqlalchemy import create_engine` 
	- Step 2: create a SQL engine:
		- Syntax: `engine = create_engine(*args)`
		- the `(*args)`  is a string which indicates DB dialect (sqlite, MySQL, postgresql...) and connection arguments in form of a url.
			- ![[Pasted image 20220118101950.png|500]]
	- Step 3: query directly from the DB using [`pd.read_sql()`](https://pandas.pydata.org/docs/reference/api/pandas.read_sql.html) and import it to a `DataFrame`
		- Syntax: `df = pd.read_sql('SQL_query', engine)`
	- Step 4: close connection.
- Write DB: [`df.to_sql()`](https://pandas.pydata.org/pandas-docs/dev/reference/api/pandas.DataFrame.to_sql.html) method
	- Step 1: import `sqlalchemy` and create a SQL engine
	- Step 2: using `df.to_sql()`:
		- e.g. ![[Pasted image 20220118102821.png|400]]
		- `con`: input `sqlalchemy.engine` or `sqlite3.connection`
		- `if_exists` argument instructs how to behave if the DB already exists; 
			- default 'fail' -> raise a ValueError, 
			- or 'replace' -> drop replace old table by this new one, 
			- or 'append' -> inserting new values to existing table 
	- Bonus: Check if data is written correctly
		- Syntax: `engine.execute('SQL_query').fetchall()`
- [Create a Table in DB from Python](https://www.pythonsheets.com/notes/python-sqlalchemy.html#sqlalchemy-support-dbapi-pep249) and [more](https://www.pythonsheets.com/notes/python-sqlalchemy.html).
### JSON:
- `pd.read_json()`
- `pd.to_json()`
### Excel:
- Read excel file: using [`pd.read_excel()`](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html) method.
- Write to excel file: using [`pd.to_excel()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_excel.html) method.
	- Using [`pd.ExcelWriter()`](https://pandas.pydata.org/docs/reference/api/pandas.ExcelWriter.html#pandas.ExcelWriter) to write `DataFrame` objects in to specific excel sheets.
## Dealing with date:
### Convert data to datetime:
- [`pd.to_datetime()`](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html): convert argument to Pandas datetime.
- `pd.to_timedelta()`
### Get year and month from Pandas datetime:
[**ref**](https://stackoverflow.com/questions/25146121/extracting-just-month-and-year-separately-from-pandas-datetime-column)
- If `df['date']`  is datetime type and is not index column:
	- Get year: `df['year'] = df['date'].dt.year`
	- Get month: `df['month'] = df['date'].dt.month`
	- `df['date'].dt.week`
	- `df['date'].dt.dayofweek`
	- `df['date'].dt.dayofyear`
- If we have DatetimeIndex:
	- Get year: `df['year'] = pd.index.year`
	- Get month: `df['month'] = pd.index.month`