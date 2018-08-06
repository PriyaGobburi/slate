# Architecture of edChain

TODO: Need to update this section
## Schema
Every edChain contributor needs to have edChain database schema setup at their end. 
It contains information about the structure of its content. For the most basic cases, you'll just rely on edChain's default core schema. But for advanced use cases, you can enforce rules about what the content of a edChain document can contain.

# Design

edChain consists of 3 main components
* edChain Android
* edChain API
* edChain Videoscraper

## edChain Android design


```
edchain-android
	|
	|\
	| \
	|  android
	|\
	| \
	|  assets
	|\
	| \
	|  gen
	|\
	| \
	|  ios
	|\
	| \
	|  node_modules
	|\
	| \ 
	|  src
	|	|
		|\
		| config
		|	|
		|	|\
		|	| agent.js
		|	|\
		|	| constants.js
		|	|\
		|	| routes.js
		|\
		| Explore
		|\
		| Home
		|\
		| Stellar
		|\
		| styles
```

![Design Text](https://raw.githubusercontent.com/PriyaGobburi/slate/master/source/images/edChain_AndroidDesign.jpg)

## edChain API design
![Design Text](https://raw.githubusercontent.com/PriyaGobburi/slate/master/source/images/edChain_API.jpg)

## edChain Videoscraper design
![Design Text](https://raw.githubusercontent.com/PriyaGobburi/slate/master/source/images/edChain_Video_Scraper.jpg)
