# Architecture of edChain

TODO: Need to update this section
## Schema
Every edChain contributor needs to have edChain database schema setup at their end. 
It contains information about the structure of its content. For the most basic cases, you'll just rely on edChain's default core schema. But for advanced use cases, you can enforce rules about what the content of a edChain document can contain.

Schema that defines a Yale course video
courses collection
```json
{
  "_id": "ObjectId",
  "subject_matter":  "string"
  "instructor_name": "string"
  "publication_date": "string"
  "course_thumbnail": "string"
  "course_hyperlink": "https://youtu.be/nAn02VhQ0GM"
  "content_address": "string"
  "unique_identifier": "string"
  "course_title": "edChain Sample course"
  "course_description": "sample data"
  "copyright_holder": "YaleCourses"
  "lectures": Array
              {
                { "object": "string" },
                { "object": "string" },
                { "object": "string" }
             }
  "document_root": "string"
}
```
lectures Array Object
```json
{
  "lecture_title": "ObjectId",
  "english_transcript":  "string"
  "ordinal_number": "string"
  "lecture_hyperlink": "string"
  "lecture_description": "string"
  "statistics" : 
                {
                "views": "ObjectId",
                "likes":  "string"
                "runtime": "string"
                "dislikes": "string"
                "keywords": "string"
                "rating": "string"
                }
  "course_hyperlink": "https://youtu.be/nAn02VhQ0GM"
  "content_address": "string"
}
```
Schema that defines a MIT course video
```json
courses collection
{
  "_id": "ObjectId",
  "content_address": "string"
  "copyright_holder": "MIT"
  "course_title": "string"
  "deep_link": "https://youtu.be/nAn02VhQ0GM"
  "instructor_name": Array
              {
                { "object": "string" },
                { "object": "string" },
                { "object": "string" }
             }
  "publication_date": "string"
  "subject_matter": "string"
  "unique_identifier": "string"
}
```
The id property
The id property serves as unique identifies for each object in the schema.
Ex: 
"id": "5b15997284c535f7c78b06cc"

# Project Structure

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
