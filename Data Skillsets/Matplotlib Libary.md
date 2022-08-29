## Matplotlib
```ad-resources
- [**official tutorials**](https://matplotlib.org/stable/tutorials/index.html)
- [**official Matplotlib cheatsheat**](https://matplotlib.org/cheatsheets/cheatsheets.pdf)
```
### Import Matplotlib
- Syntax: `import matplotlib.pyplot as plt`
- `%matplotlib inline`: ensure out plots are shown in Jupyter Notebook itself but not pop-up windows
### Part of a Figure
```ad-resources
[Part of a Figure](https://matplotlib.org/stable/tutorials/introductory/usage.html#parts-of-a-figure)
```
![[Pasted image 20220120104316.png|600]]
- **Figure**, is the **whole** figure, usually includes one or several **Axes** (or "graphs"). An **ax** (different from **axis**) includes two (or three if 3D) **axis** which ticks and tick labels and a region for plotting data.
- **Artist** is basically everything visible on the Figure such as *Text* objects, *Line2D* objects, *collections* objects... and even **Figures**, **Axes** and **Axis**. When Figure is rendered, all of the Artists are drawn to the **canvas**.
### Global API and OO API
```ad-important
In general, we should use OO API especially for complicated plots and functions (Global API or even [[Pandas library#Quick Plot in Pandas|Pandas plot]]) to draw simple plots 
```
```ad-tip
Add `;` after the last plot statement to avoiding the output (e.g. `[<matplotlib.lines.Line2D at 0x7ff70aa20760>]`) and display only the graph
```
#### Global API (or pyplot style)
- Matplotlib's default pyplot API has a global, MATLAB-type interface.
- **Problem:** In global API, we use directly the `plt` module to plot the graph(s) -> super hard to separate and post-rendered modify several graphs at the same time as the plot in to be done in a code-sequence order.
- **Solution:** Ok for using global API for simple plot, but for dealing with several graphs or complex plot -> OOP API instead as it gives us more flexibility and the ability to break the plot to smaller parts so easier to manage.
- Example:
	- ![[Pasted image 20220120105617.png|550]]
#### OO API (or Object-oriented style) 
- Explicitly create Figures  and Axes, and call methods on them => much better for plotting complicated plots compared to pyplot style
- Example:
	- ![[Pasted image 20220120110618.png|650]]
### Basic plots
#### Using OO API: 
- Syntax: `fig, *ax = plt.subplots()`
	- [`plt.subplots()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib-pyplot-subplots) (or `matplotlib.pyplot.subplots()`): create (return) a figure and a set of subplots (assigned to axes), with important arguments:
		- `nrows`: number of rows
		- `ncolumns`: number of columns
		- `figsize`: width and height of the figures in inches
		- `sharex`, `sharey`: controls the subplots will share x
		- `constrained_layout`: when active, set to `True`, will automatically adjusts subplots and decorations (e.g. legend and colorbars) so that they fit in the figure window while still preserving the logical layout. More about [Constrained Layout Guide](https://matplotlib.org/stable/tutorials/intermediate/constrainedlayout_guide.html#constrained-layout-guide).
	- `fig` and `*ax` (or `axs` used as list of `ax`) is the returned object `plt.subplots()` function.
	- example in the `plt.subplots()` link.
#### Common charts:
```ad-resources
[Python Graph Gallery](https://www.python-graph-gallery.com/) (with code) organized by sections
```
- **Line Chart:** Using [`ax.plot()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.plot.html#matplotlib.axes.Axes.plot) (or `Axes.plot`): plot y versus x as lines and/or markers -> return a **list** of Line2D
	- Syntax: `ax.plot(x, y, [fmt], *, data=<labelled_data>, **kwargs)`
		- `[fmt]`: a format string consists of a part for color, marker and line style. to see common use `fmt` see ref link.
			- `fmt = '[marker][line][color]'`
		- important properties:
			- `antialiased` or `aa`: assigned whether use antialiased rendering or not
			- `color` or `c`: assigned color
			- `data`: assigned input data from a labelled data.
			- `label`: assigned label which is displayed in the legend
			- `linestyle` or `ls` (including in `fmt`)
			- `markeredgecolor` or `mec`
			- `markeredgewidth` or `mew`
			- `markerfacecolor` or `mfc` (including in `fmt`)
			- `markersize` or `ms`
	- Plotting labelled data: all indexable object are supported (e.g. `dict`, `pandas.DataFrame` or `numpy.ndarray`)
		- e.g. ![[Pasted image 20220120120712.png|350]] 
	- Plotting multiples lines in one ax (or graph):
		- Most straight forward way is just to call `ax.plot()` multiple times.
			- e.g. ![[Pasted image 20220120120928.png|200]]
		- The other way is to specify multiple sets of \[x], y, `[fmt]` groups:
			- e.g. ![[Pasted image 20220120121231.png|300]]
- **Bar Chart:** Using [`ax.bar()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.bar.html#matplotlib.axes.Axes.bar): make a bar plot -> return BarContainer with all the bars (there is also bar horizontal, using [`ax.barh()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.barh.html)). 
	- Syntax: `ax.bar(x, height, width=0.8, bottom=None, *, align='center', data=None, **kwargs)`
		- `x`: x coordinates of the bars
		- `height`: the height(s) of the bars, corresponding to each x.
- **Scatter Chart:** Using [`ax.scatter()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.scatter.html#matplotlib-axes-axes-scatter): make a scatter plot of y vs. x with varying marker size and/or color. 
	- Syntax: `ax.scatter(x, y, s=None, c=None, marker=None,...)`
		- `x`, `y`: the data positions
		- `s`: the marker size in point\*\*2
		- `c`: the marker colors.
		- `marker`: the marker style.
#### Most Useful methods of Figures:
- [`fig = plt.figure(constrained_layout=True)`](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.figure.html#matplotlib.pyplot.figure): create a new figure, or activate an existing figure (with active constrained_layout)
- [`fig.suptitle`](https://matplotlib.org/stable/api/figure_api.html#matplotlib.figure.Figure.suptitle): add a center suptitle to the figure
#### Most Useful methods of Axes:
- [`ax.set()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set.html#matplotlib.axes.Axes.set): Set multiple *simple* properties at once, including `title`, `xlable`, `ylabel`, `xlim`, `ylim`...
- [`ax.set_title()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_title.html#matplotlib.axes.Axes.set_title): set title of the ax using an argument in string
- [`ax.set_xlabel()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xlabel.html#matplotlib.axes.Axes.set_xlabel): set xlabel using an argument in string
- [`ax.set_ylabel()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_ylabel.html#matplotlib.axes.Axes.set_ylabel): set ylabel using an argument in string
- [`ax.axis()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.axis.html#matplotlib.axes.Axes.axis): set and get properties axis (e.g. input as list \[xmin, xmax, ymin, ymax]).
	- [`ax.set_xlim()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xlim.html#matplotlib.axes.Axes.set_xlim): set limit for x-axis, xmin and xmax
	- [`ax.set_ylim()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_ylim.html#matplotlib.axes.Axes.set_ylim): set limit for y-axis, ymin and xmax
	- [`ax.set_xscale()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xscale.html#matplotlib-axes-axes-set-xscale): set the x-axis scale
	- [`ax.set_yscale()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_yscale.html#matplotlib-axes-axes-set-yscale): set the y-axis scale
	- [`ax.set_xticks`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xticks.html#matplotlib-axes-axes-set-xticks): set x-axis' tick locations and optionally label
		- [`ax.set_xticklabels`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xticklabels.html#matplotlib-axes-axes-set-xticklabels): set the xaxis' labels with list of string labels.
			- Rotation tick labels: [link](https://stackoverflow.com/questions/10998621/rotate-axis-text-in-python-matplotlib)
	- [`ax.set_yticks`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_yticks.html#matplotlib-axes-axes-set-yticks): set y-axis' tick locations and optionally label
	- More on [Tick locators](https://matplotlib.org/stable/gallery/ticks/tick-locators.html#tick-locators), [Tick formatters](https://matplotlib.org/stable/gallery/ticks/tick-formatters.html#tick-formatters) and [Date tick labels](https://matplotlib.org/stable/gallery/text_labels_and_annotations/date.html#date-tick-labels) (for Time-series data).
- [`ax.legend()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.legend.html#matplotlib.axes.Axes.legend): place a legend an the Axes ([Legend guide](https://matplotlib.org/stable/tutorials/intermediate/legend_guide.html))
- [`ax.text(x, y, s, fontdict=None, **kwargs)`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.text.html#matplotlib.axes.Axes.text): add text `s` to the Axes at the location x, y.
- [`ax.grid()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.grid.html#matplotlib.axes.Axes.grid): configure the grid lines
- [`ax.annotate()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.annotate.html#matplotlib.axes.Axes.annotate): annotate the point *xy* with *text* (and arrow using *arrowprops*)
#### Create the second axis:
- [example](https://matplotlib.org/stable/tutorials/introductory/usage.html#additional-axis-objects)
- [`ax.twinx()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.twinx.html#matplotlib-axes-axes-twinx): create a twin Axes (overlap the original Axes) sharing the same x-axis with the original Axes and an independent y-axis positioned opposite to the original one -> return **a new overlapped Axes**. same for `ax.twiny()`.
- [`ax.secondary_xaxis()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.secondary_xaxis.html#matplotlib-axes-axes-secondary-xaxis): add a second x-axis to this Axes (e.g. have a second scale) -> return **a new overlapped Axes**. same for `ax.secondary_yaxis()`
#### Arrange multiple Axes in a Figure: 
```ad-resources
[Arranging multiple axes in a figure](https://matplotlib.org/stable/tutorials/intermediate/arranging_axes.html#arranging-multiple-axes-in-a-figure)
```
- Using [`plt.subplots()` for a x b grid](https://matplotlib.org/stable/tutorials/intermediate/arranging_axes.html#basic-2x2-grid)
- Using [`plt.subplot_mosiac()` for Axes spanning rows or columns in a grid](https://matplotlib.org/stable/tutorials/intermediate/arranging_axes.html#axes-spanning-rows-or-columns-in-a-grid)
- To nest Axes layout (e.g. put two unrelated Figures together), using [`fig.subfigures()`](https://matplotlib.org/stable/tutorials/intermediate/arranging_axes.html#nested-axes-layouts)