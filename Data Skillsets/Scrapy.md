# Scrapy
```ad-info
Scrapy is an application framework for crawling web sites and extracting structured data. [Scrapy official tutorial](https://docs.scrapy.org/en/latest/intro/tutorial.html)
```
- Scrapy automatically follows the rule in robots.txt (robots.txt file tells/recommends search engine crawlers which URLs the crawler can access on the site)
	- If don't want to follow the robots.txt rule: Go to setting.py -> change `ROBOTSTXT_OBEY` to `False`
- Create each specific class to scrap each page type.
## Scrapy project
```ad-important
A simple and common scrapy project will include the following step:
- Creating a new Scrapy project
- Writing a spider to crawl a site and extract data
- Exporting the scraped data using the command line 
- Making spider to recursively follow links
```
### Create a Scrapy project
- Choosing a directory to create the project (using command line)
- Create a Scrapy project syntax: `scrapy startproject <project_name>`
- The newly created scrapy project will contains:
	- ![[Pasted image 20220225084711.png|500]]
### Write a spider
- [ref](https://docs.scrapy.org/en/latest/topics/spiders.html)
```ad-info
Spiders are **classes** which define how a certain site(s) will be scraped, including how to crawl (i.e. follow links) and how to extract structured data from these pages (i.e. scraping items). 
```
```ad-caution
We need to run the *spider.py* file (`ctrl + f5` in VS code) before run the spider in command line.
```
#### scrapy.Spider
- `scrapy.Spider` is a simplest class of spider, from which other spider must inherit. It provides basic sending requests method and parsing response method ([more details](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy-spider)) but not any special functionality.
#### A scrapy cycle for spider
- Simple example (page 69):
	- ![[Pasted image 20220225090457.png|500]]
- *First:* We start by generating initial request to crawl the 1st URL and specify a [callback (call after) function](https://stackoverflow.com/questions/824234/what-is-a-callback-function) to be called to deal with the response downloaded from those requests.
	- using [`start_requests()`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.start_requests) method to generate request for the URLs in [`start_urls`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.start_urls) attributes
	- using [`parse()`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.parse) as default method (callback function), or specify a new callback function, to deal or parse the response of the above request
- *Second:* In the callback function, we parse the response or parse the page contents (using [Selectors](https://docs.scrapy.org/en/latest/topics/selectors.html#topics-selectors) or [[BeautifulSoup library]] or lxml) and generate [items](https://docs.scrapy.org/en/latest/topics/items.html) with the parsed data.
- *Finally:* the items returns from the spider will be persisted to a database (in some [Item Pipeline](https://docs.scrapy.org/en/latest/topics/item-pipeline.html)) or written to a file using [Feed exports](https://docs.scrapy.org/en/latest/topics/feed-exports.html) (to export in common file type such as JSON, CSV or XML)
#### CrawlSpider
- [CrawlSpider](https://docs.scrapy.org/en/latest/topics/spiders.html#crawlspider) is the most commonly used spider for crawling regular websites. It provides a convenient mechanism for following links (crawling) by **defining a sets of rules for the crawling links.**
- CrawlSpider inherits the simple `scrapy.Spider` class, but also has new attributes:
	- `rules`:  which is a list of [`Rule`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Rule) objects, defining the crawling rules for the spider.
		- if multiple rules match the same link, the first matched rule will be used.
		- `Rule` object has a mandatory argument which is a [`LinkExtractor`](https://docs.scrapy.org/en/latest/topics/link-extractors.html#topics-link-extractors) object, which is a class designed solely to recognize and return links in a HTML content based on a rules provided to it.
- Example (page 73-74)
### Export and Store data
#### Items in Scrapy
```ad-important
Reason to use Scrapy `Items`:
- Good code and storing structure organiztion for scraped data
- Can use `Items` to output scraped data to several file types (e.g. csv, json, xml)
```
- [Item classes](https://docs.scrapy.org/en/latest/topics/items.html) need to be defined in the *items.py* file of the project folder
- `<new_item>` class (e.g. Article) inherits from `scrapy.Item` class
	- ![[Pasted image 20220225110640.png|250]]
- Each page type, that we scrap, should have it own class in *items.py
- Output scraped data done by a scraper (e.g. *articleItems.py*) to a file:
	- e.g. ![[Pasted image 20220307090902.png|500]]
	- Each runs of scraper including writing the output to the corresponding file
#### Item Pipeline
- [Item pipeline](https://docs.scrapy.org/en/latest/topics/item-pipeline.html) is used to process the items which are scraped by the spider, typical uses are:
	- cleansing HTML data
	- validating scraped data (checking that the items contain certain fields)
	- checking for duplicates (then drop them)
	- storing the scraped item in a database
- To create a Item pipeline, there is 3 essential steps to follow:
	1. Make sure the callback function of scraper only do the extraction of data not the processing of data
	2. Replace the processing data code in the *pipelines.py* file
		- Change is made in the `process_item` method (in *pipelines.py*), which is the mandatory method for every pipeline class.
		- e.g. ![[Pasted image 20220307095726.png|500]]
	3. Activate an Item Pipeline by add a class to the `ITEM_PIPELINES` in *settings.py* and uncomment the concern lines
		- e.g. ![[Pasted image 20220307100221.png|400]]
		- the integer value (normally run from 0-1000 range) determine the order in which the Pipeline class run: items  go through lower -> higher.
### Logging with Scrapy
- Debug information generated by Scrapy can be useful but too verbose.
- Adjust the level of logging by adding a line to *settings.py*:
	- e.g. ![[Pasted image 20220307100625.png|150]]
	- A standard hierarchy of logging levels in Scrapy, from more verbose to less:
		1. INFO
		2. DEBUG
		3. WARNING
		4. ERROR
		5. CRITICAL
		- A level of logging will also include all the logging level after it (e.g. if logging is set to ERROR, only ERROR and CRITICAL will show up)
- Or adjusting the level of logging through the command line:
	- To output log in a separate logfile instead of terminal, define a logfile when running from the command line.
	- e.g. ![[Pasted image 20220307101358.png|500]]