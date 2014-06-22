---
layout: post
title: "Enabling hstore with a Rails Migration"
date: 2014-05-16 20:21
comments: true
categories: [PostgreSQL,Rails,Migration]
---

If you've used PostgreSQL before with hstore. I'm sure you've come across this while running your migrations.

```
PG::UndefinedObject: ERROR:  type "hstore" does not exist
```
<!-- more -->
Then you have to go into your database, enable hstore, but what if you rebuild the database? You run into that problem all over.

The easiest and most reliable solution I've found, is to create a migration that runs before all of your other migrations.

Just make sure the timestamp comes before all of the other files, and make the contents of the file look like this:

```ruby
# 200001010000_enable_hstore.tb
class EnableHstore < ActiveRecord::Migration
  def self.up
    execute 'CREATE EXTENSION hstore'
  end

  def self.down
    execute 'DROP EXTENSION hstore'
  end
end
```

Now, when you migrate your database, the first thing that happens is enabling hstore.
