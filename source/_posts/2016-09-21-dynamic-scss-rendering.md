# Dynamically Rendering SCSS in Rails



Recently at I came across a problem where I needed to dynamically include a stylesheet, or scss snippet depending on what kind of content I was showing. My first inclination was to use something like this:

``` ruby
# app/views/layouts.application.html.erb
...
<%= yield :head %>

# app/views/some_controller/some_view.html.erb
<% content_for :head do %>
  <%= stylesheet_link_tag '/path_to/stylesheet.css' %>
<% end %>
```



While this works just fine, however it doesn't play quite as nicely when you're using Turbolinks. While using Turbolinks, this implementation requires you to do a full page load every time you change the stylesheets included in the head. This isn't the end of the world, but wasn't quite the solution I was looking for.

After some more searching, I stumbled across the [SASS lang documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html) which included examples for rendering SCSS in rails.

With this knowledge, I was able to insert the computed CSS into my document, without the need to precompile, and without requiring a full page load.

In the end, my solution looked something like this.



``` ruby
# app/helpers/application.rb
def render_styles_for(stylesheet)
  path = Rails.root.join('app', 'assets', 'stylesheets', styleseet ])
# style: :compact, tells the Sass::Engine to render the SCSS in
# the minimum amount of space possible
css = Sass::Engine.new(File.open(path).read, syntax: :scss, style: :compressed)
  content_tag('style', css.render)
end

# app/views/some_controller/some_view.html.erb

<%= render_styles_for('new_styleshseet.scss') %>
<h1>Some Content</h1>
<p>And a little bit more content</p>
```

Now, you could even take this a bit further, and use it to render scss off of the web, or even from the database. All you need to do is pass some text to the `Sass::Engine.new` method, and it will output scss for you!