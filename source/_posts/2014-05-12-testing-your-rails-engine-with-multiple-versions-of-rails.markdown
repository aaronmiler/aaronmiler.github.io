---
layout: post
title: "Testing your Rails Engine with Multiple Versions of Rails"
date: 2014-05-12 21:14
comments: true
categories: [Rails,Engine]
---

I've been building a rails engine over the past couple of weeks. As I near completion, I wanted to make sure that my engine was compatible with multiple versions of Rails.

The way that I found the easiest was outlined by Richard Schneeman (AKA [schneems](https://github.com/schneems)) in his blog post [Testing Against Multiple Rails Versions](http://www.schneems.com/post/50991826838/testing-against-multiple-rails-versions/)

<!-- more -->

His example was given for a gem, using Travis CI. Lucky for me, I was also using Travis to test my engine, and modifying his approach wasn't too crazy.

So, in order to test your Rails Engine against multiple versions of rails you will want to do the following.

First, in your `.travis.yml` file you'll want to put the following ENV variables
```yml
# .travs.yml
env:
  - "RAILS_VERSION=3.2.0"
  - "RAILS_VERSION=4.0.0"
  - "RAILS_VERSION=4.1.0"
```

You can see here I want to test against `Rails 3.2.0`, `Rails 4.0.0`, and `Rails 4.1.0`. You can put as many/any versions you want in that section.

Next, in your Gemfile put the following code

**NOTE**: Not your engine.gemspec file, in the Gemfile in the root directory of your rails Engine

```ruby
# Gemfile

rails_version = ENV["RAILS_VERSION"] || "default"

rails = case rails_version

when "master"
  {github: "rails/rails"}
when "default"
  ">= 3.2.0"
else
  "~> #{rails_version}"
end

gem "rails", rails
```

Lastly, make sure in your `.gitignore` file you add your `Gemfile.lock`. This will make sure that Travis rebuilds the gems for your engine every time it tests against a new environment variable.

After that you're all done, you'll see that the number of test runs on Travis go up pretty substantially. As you can see in the image below Travis is testing against 3 different versions of Ruby, and 3 different versions of Rails. My tests may take longer now, but it's nice to know

![Travis Tests](/images/travis_tests.png "Travis Tests")
