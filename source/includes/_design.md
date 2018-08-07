# Architecture of edChain

TODO: Need to update this section
## Schema
Every edChain contributor needs to have edChain database schema setup at their end. 
It contains information about the structure of its content. For the most basic cases, you'll just rely on edChain's default core schema. But for advanced use cases, you can enforce rules about what the content of a edChain document can contain.

Schema that defines a Yale course video

> courses collection

```markdown
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

> lectures Array Object

```markdown
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

> courses collection

```markdown
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
* edChain API
* edChain videoScraper
* edChain android

<aside class="notice">
  
</aside>

## edChain API

> Folder Structure of the edChain API Project

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

Here we define the directories

* <strong>config:</strong>

* <strong>models:</strong>

* <strong>routes:</strong>

* <strong>tests:</strong>


## edChain VideoScraper



> Folder Structure of the edChain VideoScraper Project

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

## edChain android

> Folder Structure of the edChain android Project

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

