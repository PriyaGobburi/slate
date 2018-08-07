# Architecture of edChain

edChain architecture consists of user interface, 2 main modules and edChain database.

* <strong>edChain Android:</strong> User interaction with App takes place here. 

* <strong>edChain API:</strong> It provides meta data to the users and developers

* <strong>Curation Module:</strong> All videos are constructed, formatted and ordered here.

* <strong>Mongo DB:</strong> Database collects and stores the data.

![Architecture Icon](https://raw.githubusercontent.com/PriyaGobburi/slate/master/source/images/edChain_Architecture1.png)



## Schema


> Sample Course Structure

```
 {     
        "course_thumbnail": "http://i.ytimg.com/vi/-w0ylnzMwjc/hqdefault.jpg",
        "copyright_holder": "YouTube",
        "lectures": [
            {
                "lecture_title": "How Bitcoin and The Blockchain works | Chad Cascarilla",
                "lecture_thumbnail": "http://i.ytimg.com/vi/-w0ylnzMwjc/hqdefault.jpg",
                "lecture_hyperlink":  "https://youtu.be/nAn02VhQ0GM",
                "statistics": {
                    "runtime": 1907,
                    "views": 7769,
                    "keywords": [
                        "bitcoin",
                        "value",
                        "protocol",
                        "itBit",
                        "blockchain",
                        "fintech",
                        "$BTC",
                        "what is bitcoin",
                        "how does bitcoin work",
                        "what is blockchain",
                        "how does blockchain work",
                        "cryptocurrency",
                        "digital currency"
                    ],
                    "likes": 109,
                    "dislikes": 1,
                    "rating": 4.96363639832
                },
                "lecture_description": "String",
                "content_address": ""
            }
        ],
        "weight": 0.07231818199159999,
        "publication_date": "",
        "english_transcript": "",
        "instructor_name": "Real Vision",
        "content_address": "",
        "course_hyperlink": "https://www.youtube.com/watch?v=-w0ylnzMwjc",
        "ordinal_number": "",
        "subject_matter": "Bitcoins and Blockchain",
        "course_description": "String",
        "document_root": "",
        "course_title": "How Bitcoin and The Blockchain works | Chad Cascarilla"
    }
```

Every edChain contributor needs to have edChain database schema setup at their end. 
It contains information about the structure of its content. For the most basic cases, you'll just rely on edChain's default core schema. But for advanced use cases, you can enforce rules about what the content of a edChain document can contain.

Schema that defines a course video
courses is a collection
lectures Array Object
statistics Array Object

The id property
The id property serves as unique identifies for each object in the schema.
Ex: 
"id": "5b15997284c535f7c78b06cc"

# Project Structure

edChain consists of 3 main components

* edChain API
* edChain curation_module
* edChain android

<aside class="notice">
  Only the core project files and dirctories are shown under the project structure
</aside>

## edChain API

This API module consists of 5 main components.

* config: All configuration goes here.

* models: Describes the sturcture of internal components.

* routes: It acts like a middle tier.

* tests: Tests are added here

* app.js: It is entry point for API

> Structure of the edChain API Project

```markdown
edchain-api
      |
      |--+ config
      |
      |--+ models
      |
      |--+ routes
      |
      |--+ tests
      |
      |--- app.js
```
## edChain curation_module

edChain curation module consists of 2 main components.

* DatabaseBashScript : TODO

* edchain-videoScraper : TODO

> Structure of the edChain curation_module Project

```markdown
edchain-videoScraper
      |
      |--- DatabaseBashScript
      |     |
      |     |--+ CourseData
      |     |
      |     |--- mongoImportAll.sh
      |
      |--- edchain-videoScraper
      |     |
      |     |--- edChain_scraper.py
      |     |
      |     |--- curationWeightsAlgorithm.py
      |     |
      |     |--- curationConstants.py
      |     |
      |     |--- wsgi.py
```
## edChain Android application

edChain Android aplication module consists of one main components.

* source : TODO

> Structure of the edChain android Project

```markdown
edchain-android
      |
      |--+ src
            |
            |--+ config
            |
      	    |--+ Explore
      	    |
            |--+ Home
            |
            |--+ Stellar
            |
            |--+ styles
```
