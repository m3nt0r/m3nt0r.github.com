---
layout: post
title: Hello GitHub Pages! - 
date: 2011-07-01
---

## Hello GitHub Pages!

This is just a test :)

Lorem ipsum dolor sit amet, consectetur **adipisicing** elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud *exercitation* ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 

Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation.

### ordered lists

1. listitem
2. listitem
3. listitem

### unordered lists

- listitem
- listitem
- listitem

### codeblock

    var spaces = 4;
    this.shouldBe = some(code);
    
### highlighted codeblock

Some Ruby...

{% highlight ruby %}
def File.binread(fname)
	open(fname, 'rb') {|f|
		return f.read
	}
end

class ConfigTable
	include Enumerable
	
	def initialize(rbconfig)
		@rbconfig = rbconfig
		@no_harm = false

{% endhighlight %}

Some CoffeeScript

{% highlight coffeescript %}
# Bind all of an object's methods to that object. Useful for ensuring that
# all callbacks defined on an object belong to it.
_.bindAll = (obj) ->
  funcs = if arguments.length > 1 then _.rest(arguments) else _.functions(obj)
  _.each funcs, (f) -> obj[f] = _.bind obj[f], obj
  obj


# Zip together multiple lists into a single array -- elements that share
# an index go together.
_.zip = ->
  length =  _.max _.pluck arguments, 'length'
  results = new Array length
  for i in [0...length]
    results[i] = _.pluck arguments, String i
  results


# If the browser doesn't supply us with **indexOf** (I'm looking at you, MSIE),
# we need this function. Return the position of the first occurrence of an
# item in an array, or -1 if the item is not included in the array.
_.indexOf = (array, item) ->
  return array.indexOf item if nativeIndexOf and array.indexOf is nativeIndexOf
  i = 0; l = array.length
  while l - i
    if array[i] is item then return i else i++
  -1
{% endhighlight %}


### inline code

This should be ```inline``` code

### blockquotes

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation

> "[...] ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor." - lorem

### links

a non-markdown link: http://github.com/blog 
this one is [a markdown link](http://github.com/blog) 
Email test: support@github.com

### github md?

c4149e7bac80fcd1295060125670e78d3f15bf2e 
issue #1
