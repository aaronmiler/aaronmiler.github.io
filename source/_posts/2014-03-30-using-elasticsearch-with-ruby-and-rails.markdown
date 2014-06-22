---
layout: post
title: "Using Elasticsearch with Ruby and Rails"
date: 2014-03-30 17:12
comments: true
categories: [Elasticsearch,Ruby,Rails]
---

At work I've been working on replacing our current product search (currently powered by a SaaS) with Elasticsearch. When I first started I set out to find what Ruby gem I should use on this project.

I found a couple of very impressive gems, such as [Search Kick](https://github.com/ankane/searchkick), but unfortunately Search Kick currently doesn't support Mongoid, so I kept looking.
<!-- more -->
After burning through a couple of other gems, all I'm left with now is the [Elasticsearch Ruby Gem](https://github.com/elasticsearch/elasticsearch-ruby)

Here are some tricks I used that I think made using the Elasticsearch gem easy.

Most methods are called against an Elasticsearch object. So in my model, I decided to store that object on initialization.

``` ruby
class Search
  attr_accessor :connection
  def initialize
    @connection = Elasticsearch::Client.new hosts: ["myhost1","myhost2" ], randomize_hosts: true
  end
end
```
The `randomized_hosts: true` allows you the load balance your Elasticsearch hosts

With the above code I can make queries in my model like so
``` ruby
def look_for(query)
self.connection.search index: "index_name", body: {
    query: {
      terms: {
        FIELD: [
          "VALUE1",
          "VALUE2"
         ]
      }
    },
    size: 25
  }
end
```
I found building queries in my ruby code to be quite annoying. Mainly because it took too long for me to get error messages from my Elasticsearch server and tests.

Then I found [Sense](https://chrome.google.com/webstore/detail/sense/doinijnbnggojdlcjifpdckfokbbfpbo). Sense is a chrome extension that allows you to build JSON based queries, that can be converted into the Ruby query DSL rather easily.

Here is the JSON query
``` javascript
"query": {
    "terms": {
       "FIELD": [
          "VALUE1",
          "VALUE2"
       ]
    }
}
```

You can see how it translates to the ruby DSL above. The feedback is quick, and it's a great way to test out your queries without doing a ton of modifications to your models.

One of the last roadblocks I ran into was dealing with Facets. I wanted to facet the products based on what Category they were in. Thing is, categories aren't always one word. By default Elasticsearch breaks up all of the words you want to facet. So a category like `Category Name` would come back with results something like this
```
"terms": [
            {
               "term": "Category",
               "count": 1
            },
            {
               "term": "Name",
               "count": 1
            },
]
```

What I wanted is this
```
"terms": [
            {
               "term": "Category Name",
               "count": 1
            }
]
```

To get there I found out I have to make sure anything I want to facet on (that will have more than 1 word) need to have their indexing set to `not_analyzed`. Now if you try to index something to an Elasticsearch index that doesn't exist, it will create it for you. But to get a column to be set as not_analyzed you need to create it yourself.

You can do it pretty easily like this
``` ruby
  def create_index
    self.connection.indices.create index: MYINDEXNAME,
      body: {
        mappings: {
          TYPE: {
            properties: {
              field: { type: 'string', index: 'not_analyzed'}
            }
          }
        }
      }
  end
```

My current roadblock is I can't put any sort of Ruby logic into the middle of the Elasticsearch query DSL, and I can't query for blank as it returns no results.

We'll see if something like that is possible, if not I may end up moving to another gem all together.

