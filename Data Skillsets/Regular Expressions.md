## Regular Expressions:
> [Regex HOW TO](https://docs.python.org/3/howto/regex.html) in Python documentation
- **Practice regex:** 
	- [x] [regexone](https://regexone.com/) 
	- [ ] [hackerrank](https://www.hackerrank.com/domains/regex)
	- [ ] https://regexr.com/
### Definition: 
```ad-info
**Regular expressions** ("regex" or "regexp") are loosely really clever "wild card" expressions for richer matching and parsing strings.
```
- Regex used to identify *regular strings* (any string that can be generated by a series of linear rules), which means:
	1. strings which follow the regex rules -> `True`
	2. strings which don't follow the regex rules -> `False`
### Common metacharacters of regex 
```ad-info
[Metacharacters of regex in Python](https://realpython.com/regex-python/#metacharacters-that-match-a-single-character)
```
- Regex and its metacharacters can be a really powerful and flexible way to represent pattern in string.
	- e.g.1. ![[Pasted image 20211230100335.png|500]]
	- e.g.2. (more precise match with no white space) ![[Pasted image 20211230100942.png|500]]
### Regular expression library 
```ad-info
official documentation of [`re` library](https://docs.python.org/3/library/re.html)
```
#### Import: 
	- Syntax`import re`
#### Most useful functions of `re` library:
- [`re.search()`](https://docs.python.org/3/library/re.html#re.search): Scan through string looking for the first location where regex pattern produce a match -> return a Match object.
	- e.g.1. (same as `str.find()`) ![[Pasted image 20211230095910.png|500]]
	- e.g.2. (same as `str.startswith()`) ![[Pasted image 20211230100154.png|500]]
- `re.findall()`: to extract portions of a string that match your regular expression (same as a combination of `find` + slicing, e.g. `var[5:10]`) -> return a list of matched sub-strings.
	- e.g. ![[Pasted image 20211230101426.png|550]]
	- Warning: Greedy matching (default) -> means that the repeat characters (`*` and `+`) push outward in both directions to match the largest (greediest) possible string
		- e.g. ![[Pasted image 20211230101922.png|300]]
	- Non-greedy matching (optional) -> add `?` character after `*` or `+`
		- e.g. ![[Pasted image 20211230102122.png|300]]
	- Parenthesis () are not part of the match - but they indicate the boundary of the extraction
		- e.g. ![[Pasted image 20211230102746.png|500]]
- [`re.compile()`](https://docs.python.org/3/library/re.html#re.compile): compile a regular expression pattern into a regex object, which can be used for matching with `match()`, `search()` and other methods.
#### Most important objects of `re` library:
- [Match objects](https://docs.python.org/3/library/re.html#match-objects): have a boolean value of `True` if `match()` and `search()`identified a match but `None` when there is no match. We can simple test Match object is `True` or `None` using an if statement.
- [Regex objects](https://docs.python.org/3/library/re.html#regular-expression-objects): created by `re.complie()` and normally used as a regex pattern in `match()`, `search()` and other methods.
### Writing regex's best practices
1. break the *regular strings* to a smaller manageable parts
2. write regex for each part
3. combine them.
### Most common use regex templates
- Case 1: [Matching a scientific number](https://regexone.com/problem/matching_decimal_numbers) (with *positive and negative*; *significant digits*, *exponents*)
	- regex: `^-?\d+(,\d+)*(\.\d+)?(e\d+)?$`
- Case 2: [Matching phone numbers](https://regexone.com/problem/matching_phone_numbers?)
	- regex: `(\+?\d{0,2})?[\s-]?\(?(\d{3})\)?[\s-]?(\d{3})[\s-]?(\d{4})`
- Case 3: Matching emails
	- regex: `^([A-Za-z0-9\._-]+)(\+\w*)?@[A-Za-z0-9-\.]+\.[A-Z|a-z]{2,}\b`