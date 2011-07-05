--- 
layout: post
title: Using Twig with CakePHP
tags: 
- CakePHP
- ctp
- gist
- html
- Kitchen
- snippets
- templates
- twig
- views
---

## Using Twig with CakePHP

Having fun with <a href="http://www.twig-project.org/" target="_blank">Twig</a> right now. 

For those who don’t know what Twig is:

- Twig is a template language.
- <a href="http://www.twig-project.org/" target="_blank">http://www.twig-project.org</a><!--more-->

I've create a View for CakePHP that uses it. Here's an example.

### The good old default.ctp in Twig

{% highlight html %}
{% raw %}
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html>
  <head>
	{{ html.charset() }}
	<title>{{ 'CakePHP: the rapid development php framework'|trans }}: {{ title_for_layout }}</title>
	{{ html.meta('icon') }}
	{{ html.css('cake.generic') }}
	{{ scripts_for_layout }}
  </head>
  <body>
	<div id="container">
		<div id="header"> 
			<h1>{{
				html.link('CakePHP: the rapid development php framework'|trans, 'http://cakephp.org')
			}}</h1>
		</div>
		<div id="content">
			{{ session.flash() }}{{ session.flash('auth') }}
			{{ content_for_layout }}
		</div>
		<div id="footer">
		{{
			html.image('cake.power.gif', [
				'alt': 'Powered by CakePHP'|trans,
				'url': 'http://cakephp.org'
			])
		}}
		</div>
	</div>
  </body>
</html>
{% endraw %}
{% endhighlight %}

More can be found at: [http://github.com/m3nt0r/cakephp-twig-view](http://github.com/m3nt0r/cakephp-twig-view)

_Note:_
The above was writting pre-Twig 1.x. There are some changes for associative array syntax in the latest version.
An updated version of this source is in the examples folder.
