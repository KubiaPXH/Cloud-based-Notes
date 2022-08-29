## Seaborn
> [**official tutorial**](https://seaborn.pydata.org/tutorial.html)

> [Seaborn Cheat Sheet - DataCamp](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Seaborn_Cheat_Sheet.pdf)
### Import Seaborn:
Syntax: `import seaborn as sns` (sns is the conventional alias of Seaborn)
### Plot functions:
#### The Structure of Plot functions:
- In Seaborn, all plot functions are classified in 3 big modules which are: relational (`sns.relplot()`), distributional (`sns.displot()`), categorical (`sns.catplot()`) (image below). However, they are still accessible at the very top level. 
	- ![[Pasted image 20220125100128.png|500]]
- There are two way to call a plot function in Seaborn:
	- First: Call directly the plot function (such as `sns.histplot()`)
		- e.g. ![[Pasted image 20220125100837.png|600]]
	- or Second: Call the parent function (such as `sns.displot()`) and specify argument `kind`
		- e.g. ![[Pasted image 20220125101621.png|650]]
		- if we don't specify the kind of plot, the default kinds are:
			-  `sns.relplot()`: *scatterplot*
			-  `sns.displot()`: *histplot*
			-  `sns.catplot()`: *stripplot*
#### Common Plots:
> [Python Graph Gallery](https://www.python-graph-gallery.com/) (with code) organized by sections
##### Relational Plots:
- **Scatter Plot:** Using [`sns.scatterplot()`](http://seaborn.pydata.org/generated/seaborn.scatterplot.html#seaborn.scatterplot): drawing a scatter plot between x and y can be shown for different subsets of data (semantic groups) using the `hue`, `size` and `style` (marker in matplotlib) -> return the matplotlib axes containing the plot. Important parameters (all args in Seaborn are keyword args):
	- `data`: input data structure (usually `DataFrame`)
	- `x`, `y`: variable specify position on the x and y axes (usually a column in a `DataFrame`)
	- `hue`: grouping variable that will produce points with different colors (usually get a input column, the entities or rows have the same value in that column have the same color)
	- `size`: grouping variable that will produce points with different sizes.
	- `style` (or marker): grouping variable that will produce points with different markers.
	- `legend`: specify how to draw legend. either *auto* (default), *brief*, *full* or False.
	- `palette`: choosing the colors to use when mapping the `hue` semantic. the string input values are passed to [`sns.color_palette()`](http://seaborn.pydata.org/generated/seaborn.color_palette.html#seaborn.color_palette). Attention in selecting color palettes to present data set, we want to represent them as *sequential*, *diverging* or *categorical* data ([more details](https://www.codecademy.com/article/seaborn-design-ii)).
- **Line plot:** Using [`sns.lineplot()`](http://seaborn.pydata.org/generated/seaborn.lineplot.html#seaborn.lineplot): drawing a scatter plot between x and y can be shown for different subsets of data (semantic groups) using the `hue`, `size` and `style` (marker in matplotlib). The default treatment of the `hue` and `size` as semantic group -> return the matplotlib axes containing the plot. Important parameters are more or less the same with `sns.scatterplot()`.
##### Distribution Plots:
- **Bar plot:** Using [`sns.barplot()`](https://seaborn.pydata.org/generated/seaborn.barplot.html#seaborn.barplot)
##### Categorical Plots:
##### Regression Plots:
##### Matrix Plots:
- **Heat plot:** Using [`sns.heatmap()`](https://seaborn.pydata.org/generated/seaborn.heatmap.html): Plot rectangular data as a heat map.
### OO Interface in Seaborn:
[**ref**](http://seaborn.pydata.org/tutorial/function_overview.html#axes-level-functions-make-self-contained-plots)

- To use OO Interface in Seaborn, the process is quite familiar with OO Interface in Matplotlib. The difference is just that instead of using *Axes* methods to plot (such as `ax.plot()`) we call directly the Seaborn plot functions (such as `sns.scatterplot()`) and then assign `ax` parameter of that function to a appropriate *Axes*.
	- e.g. ![[Pasted image 20220125112204.png|700]]
### Customizing with Matplotlib:
- As Seaborn is built on top of Matplotlib, sometimes we need to use Matplotlib functions to have some customizations that Seaborn can not do, such as: set layout, set title... to Figure ([[Matplotlib Libary#Most Useful methods of Figures|more details]]); set title, label, limit, scale, ticks, legend, text, annotate... to Axes([[Matplotlib Libary#Most Useful methods of Axes|more details]]).
	- e.g. ![[Pasted image 20220125113526.png|400]]
### Themes and colors for Plot:
#### Seaborn themes:
- We can set theme for a plot by set `context`, `style` and `palette` all in one go using `sns.set_theme()` functions:
	- [`sns.set_theme()`](https://seaborn.pydata.org/generated/seaborn.set_theme.html#seaborn.set_theme): set aspects of the visual theme for all Matplotlib and Seaborn plots. Important parameters:
		- `context`: scaling parameters, built-in scales are (in order of relative size): *paper*, *notebook* (default), *talk* and *poster* ([more details](https://www.codecademy.com/article/seaborn-design-i))
		- `style`: axes style parameters, built-in styles are: *darkgrid* (default), *whitegrid*, *dark*, *white* and *ticks* (or white with ticks) ([more details](https://www.codecademy.com/article/seaborn-design-i))
		- `palette`: color palette, built-in palettes are: *deep*, *muted*, *bright*, *pastel*, *dark* and *colorblind* ([more details](https://www.codecademy.com/article/seaborn-design-ii))
- Or we can set them one by one using specified functions as [`sns.set_context()`](https://seaborn.pydata.org/generated/seaborn.set_context.html#seaborn.set_context), [`sns.set_style()`](https://seaborn.pydata.org/generated/seaborn.set_style.html#seaborn.set_style) and [`sns.set_palette()`](https://seaborn.pydata.org/generated/seaborn.set_palette.html#seaborn.set_palette)
- [`sns.despine()`](https://seaborn.pydata.org/generated/seaborn.despine.html): take away spines in Axes, default top and right spines (this function must be called after called your plot)
#### Seaborn color palettes:
- Seaborn allows us to set custom color palettes by setting `palette` argument when calling a Seaborn plot functions. The simplest way to set the exact color we want it to create a `list` of color hex values.
	- Example:
		- Set pokemon type colors:
			- ![[Pasted image 20220125122104.png|350]]
		- Assign `palette` argument with the color `list`:
			- ![[Pasted image 20220125122336.png|500]]
		- Results:
			- ![[Pasted image 20220125122404.png|700]]
