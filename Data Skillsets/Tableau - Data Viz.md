- **Category:** note
- **Title:** Tableau - Data Viz
- **Created date:** 07/06/2022
- **Updated date:** 07/06/2022
- **Tag:** [[Data Visualization]]
- **Main refs:**
	- [SQL Belle channel](https://www.youtube.com/c/sqlbelle) Primary sources to learn Tableau with systematically and very informative tutorials
	- [Beyond "Show Me" | Custom charts and maps in Tableau](https://www.youtube.com/watch?v=KJnyggxzZwE)
	- [Zen Master: The "Tableau Twins" Take You Beyond Show Me](https://www.youtube.com/watch?v=myyakEnuqa8)
---
## Abstract
---
## Tasks
---
- [Example of BANs](https://www.youtube.com/watch?v=4Ntw_6RCbyE)
	- Results:
		- ![[Pasted image 20220608115413.png]]
	- Big Number + YoY Change + Sheet Name
## Filters
```ad-resources
[Tableau Filters - Comprehensive Tutorial](https://www.youtube.com/watch?v=DVTFvmoUnlE)
```
```ad-definition
Primary role of filter is to narrow down data.
```
- The hierarchy of Tableau filters:
	```ad-important
	Data that is already filtered from higher up filters will not be seen anymore by filters lower down in the hierarchy.
	```
	- ![[Pasted image 20220610083751.png|600]]
		- There also a hidden *Latest Date Filter* between *Data Source Filters* and *Context Filters* which we can find in Filter Field for Date type variables
- **Extract Filters:**
	- Where to find?
		- ![[Pasted image 20220610090630.png|400]]
- **Data Source Filters:**
	- Where to find?
		- In Tab Data Source in the top-right corner
		- ![[Pasted image 20220610092727.png|300]]
- **Action Filters:**
- **Tooltip Filters:**
- **Context Filters:**
## Group and Set
```ad-resources
[Tableau Groups vs Sets - Comparison and examples](https://www.youtube.com/watch?v=fqBFTdTxT1M)
```
- Group and Set
	- ![[Pasted image 20220609083711.png|500]]
### Sets
- By default, Set is about In/Out (Dimension's components in In/Out of the Set). But we can also show member in the sets by using drop down -> show members.
- Combined Set can only be create using "like-minded" Sets (which means that Sets created from the same Dimension)
- **Set is dynamic** which means the members of a Set can flexibly change based on how we structure (use Condition/Top) the Set -> Huge advantage compared to Group
	- ![[Pasted image 20220609093042.png|]]
- **Set can be used in operation (e.g. Calculated Field)**
#### Set Actions
```ad-resources
[Tableau Sets and Set Actions Comprehensive Tutorial](https://www.youtube.com/watch?v=tGO1D18hKv4)
```
```ad-definition
Set Actions means that when we do an action (hover, select, menu) we can add and remove members from a set interactively.
```
- Common Use Cases:
	- Dynamic Drilldown
	- Proportional Brushing
	- Market Basket Analysis
## Tableau Actions
```ad-resources
[Introduction to Tableau Actions - sqlbelle](https://www.youtube.com/watch?v=kjgp6dZdYuA)
```
- Actions allow to add interactivity to Worksheet or Dashboard
### Set Actions
## Dashboard in Tableau
- [The 13 Types of Displays That Are All (Unfortunately) Called Dashboards](https://www.youtube.com/watch?v=jWHsLAosIIg)
## Tableau's Trick and Tip
- Open the Drop Field (Aggregate) window: `right click + drag`
- Copy pill in canvas: `ctrl + left mouse drag`
- Create a text table: first, choose dimension -> `double click` on measures we want to include in
- Recap of the Sheet: `ctrl + e` (describe sheet)
- Don't want extract data every time: Save file as `.twbx` (packaged workbook)
- Refind Field Labels: Analysis -> Table Layout -> Show Field Labels for Rows/Columns
- Unpack `.twbx` file: add `.zip` after `.twbx` and unzip the file!
