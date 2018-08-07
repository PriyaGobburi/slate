# Architecture of edChain

edChain architecture consists of user interface, 2 main modules and edChain database.
* edChain Android : User interaction with App takes place here. 
* edChain API : It provides meta data to the users and developers
* Curation Module : All videos are constructed, formatted and ordered here.
* Mongo DB : Database collects and stores the data.

![Architecture Icon](https://raw.githubusercontent.com/PriyaGobburi/slate/master/source/images/edChain_Architecture.jpg)



## Schema
Every edChain contributor needs to have edChain database schema setup at their end. 
It contains information about the structure of its content. For the most basic cases, you'll just rely on edChain's default core schema. But for advanced use cases, you can enforce rules about what the content of a edChain document can contain.

Schema that defines a course video
courses is a collection
lectures Array Object
statistics Array Object

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
The id property
The id property serves as unique identifies for each object in the schema.
Ex: 
"id": "5b15997284c535f7c78b06cc"

# Project Structure

edChain consists of 3 main components
* edChain API
* edChain videoScraper
* edChain android


## edChain API

> Folder Structure of the edChain API Project

```
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

Here we define the directories

* <strong>config: </strong>

* models:

* routes:

* tests:


## edChain VideoScraper

> Folder Structure of the edChain VideoScraper Project

```
edchain-videoScraper
      |
      |--+ DatabaseBashScript
      |
      |--+ edchain-videoScraper
```

## edChain android

> Folder Structure of the edChain android Project

```
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

