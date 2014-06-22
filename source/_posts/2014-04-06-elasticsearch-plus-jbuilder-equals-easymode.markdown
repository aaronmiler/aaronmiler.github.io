---
layout: post
title: "Elasticsearch + Jbuilder = Easymode"
date: 2014-04-06 17:16
comments: true
categories: [Elasticsearch,Ruby,Jbuilder]
---

After pondering how to deal with conditional logic in Elasticsearch queries. I finally realized that the query DSL for Elasticsearch is just structured JSON. Which is why Ruby didn't like when the syntax was messed up.
<!-- more -->
Jbuilder to the rescue!

Now with Jbuilder you can stick whatever you want in your queries. Conditional logic, loops, anything really.

Here is what we had before
``` ruby
client = Elasticsearch::Client.new host: "http://www.host.com"
client.search index: "index_name", body: {
  query: {
    term: {
      FIELD: "VALUE"
    }
  }
}
```

Here is what we can do now

``` ruby
require 'jbuilder'
client = Elasticsearch::Client.new host: "http://www.host.com"
query = Jbuilder.encode do |json|
  json.query do
    json.term do
      json.FIELD.do
        json.value "TERM"
      end
    end
  end
end
client.search index: "index_name", body: query
```

This allows you to do so much more. Like create methods that return a jbuilder object.

The biggest advantage I found from using Jbuilder, was it allowed me to DRY up all of my elastic search methods, and create conditional queries. While working with Jbuilder created it's own problems. It made working with the Elasticsearch DSL a lot easier
