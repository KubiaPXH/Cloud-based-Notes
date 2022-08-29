> Beautiful Soup official [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
## Definition
> Beautiful Soup is a Python library for pulling data out of HTML and XML files (cannot use it for JS files)
## `BeautifulSoup` object
```ad-info
official [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#beautifulsoup)
```
- The `BeautifulSoup` object represents the parsed document as whole, which means the content is transformed into a `BeautifulSoup` object
### A simple sample
- ![[Pasted image 20220204082241.png|700]]
- Here, we use `BeautifulSoup` object to create an instant `bs` with 2 main arguments:
	1. `html.read()` (only `html` work too): to get the HTML file open by `urllib.urlopen()`.
	2. the parser type (here: `html.parser`) used to parser the HTML file
		- There are two other popular parser which is:
			- `lxml`: better and somewhat faster than `html.parser` in parsing messy and malformed HTML code, but it is harder to use.
			- `html5lib`: even better in parsing HTML code than other two but harder to use and slower. 
- The instant `bs` received HTML content in the following structure
	- ![[Pasted image 20220204082039.png|700]]
	- So to get `h1`, we have many option: `bs.h1`, `bs.html.body.h1`, `bs.html.h1` or `bs.body.h1`.
- Good practice: Using generic functions (e.g. `getTitle()` )to get HTML and [[Web Scraping with Python#Handling exceptions and connection error|handle errors and exceptions]].
	- ![[Pasted image 20220204093226.png|500]]
### Most useful functions of `BeautifulSoup` object
- [`soup.find_all(tags, attrs, recursive, string, limit, **kwargs)`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find-all): method looks through a tag `name`'s descendants and retrieves *all* descendants that match [the filter](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#kinds-of-filters) -> return a list of results
	- `tags`: a `list` of string tag names
	- `attrs`: a `dict` of attributes and want-to-filter attributes' values
	- `recursive`: indicate how deep level tags we want to search. 
		- `True` (default): dig to deepest level tags
		- or `False`: look only at the top-level tags.
	- `string`: match based on the text content of the tags.
	- `limit`: number of items the function retrieves.
	- ` **kwargs`:  allows to select tags that contain a particular attribute or a set of attributes, kind of redundant but can be *useful by allowing to add an additional "and" filter to `attrs` argument.*
	- using with `.get_text()` function to get only the text in tag
- [`soup.find(tags, attrs, recursive, string, **kwargs)`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find):  find only one result that meets the filter -> return a result.
- [`soup.get_text()`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#get-text): return all the text in a document or beneath a tag
## Other useful objects
- `Tag` object's instance is retrieved individually a tag of `BeautifulSoup`'s instance or individually called `soup.find()` or `soup.find_all()`
- `ResultSet` object's instance is retrieved when it gets a list of tags by calling `soup.find_all()`
- `NavigableString` object: used to represent text within tags, rather than the tags themselves.
- `Comment` object: used to find HTML comments in comment tags, \<!--like this one-->
### `Tag` objects
- Often when web scrapping, we're not looking for the content of a tag but its attributes.
	- e.g. get URL of `a` tag from `href` attribute or get target image location of `img` tag from `src` attribute.
- Access direct on `tag` object's list of attributes (each attributes as a `dict`) using: `myTag.attrs`
## Navigating Trees
```ad-important
official [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-the-tree)
```
- **Use case:** Finding tag based on its location (not by tag name or attributes like `soup.find_all()`) 
```ad-info
Distinguish between *children* and *descendants*:
- *Descendants*: the tag can be at any level in the tree below a parent tag
- *Children*: the exact one tag below a parent tag (direct descendants)
```
- Going down: 
	- Accessing a descendant tag (first of its kind) using tag names:
		- Syntax: `soup.tag_name.sub_tag_name.another_sub_tag_name`
		- Example: `bs.body.h1` -> return the first `h1` tag which is a descendant of `body` tag
	- [`.contents`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#contents-and-children): return a tag's children in a list
	- [`.children`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#contents-and-children): used to iterate over a tag's children 
	- [`.descendants`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#descendants): used to iterate over all of a tag children, recursively: its direct children (level 1), the children of its direct children (level 2)... until no children left.
- Going sideways or to other siblings (working with tables) : 
	- [`.next_sibling` and `previous_sibling`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#next-sibling-and-previous-sibling): use to navigate the next and previous page element (only one element) that are on the same level of the parse tree
	- [`.next_siblings` and `previous_siblings`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#next-siblings-and-previous-siblings): iterate over a tag's siblings.
		- e.g. using `.next_siblings` to iterate to all the elements in a table (`tr` tag is title row?)
			- ![[Pasted image 20220204114411.png|700]]
- Going up: 
	- [`.parent`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#parent): access an element's parent
	- [`.parents`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#parents):  iterate over all of an element's parent (up to the root or document) 
- Get string:
	- [`.string`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#string): get string in a tag's children, if only one string contained in its children -> return a `NavigableString`
		- As it returns a `NavigableString` therefore `print(string)` is different from `print(repr(string)` or `print(str(string))`.
	- [`.strings`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#strings-and-stripped-strings): used to iterate over all string in a tag's children.
	- [`.stripped_strings()`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#strings-and-stripped-strings): used to iterate over all string a tag's children while stripping in all those strings.
- Nesting `BeautifulSoup` function in tag's navigating tree.
	- e.g. `bs.div.find_all('img')` will find all `img` tags which are descendant of the first `div` tag. 
	- e.g. `bs.find_all('div').children` will find all children of all the descendants `div` tag of `bs` instance (retrieved by `find_all('div')`)
- Regex