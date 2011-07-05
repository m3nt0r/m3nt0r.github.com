--- 
layout: post
title: Using Twig with CakePHP (cont.)
tags: 
- CakePHP
- ctp
- html
- Projects
- templates
- twig
- views
---

## Using Twig with CakePHP (cont.)

The TwigView got it’s own repository shortly after the initial _gist_. 

I am using the same <a href="http://github.com/m3nt0r/cakephp-twig-view">TwigView</a> for a few 
days now and i am not missing anything so far. Everything runs smoothly and i really enjoy 
working with Twig.

At first it was awkward.. How to write loops, etc. Had to refer to the  manual alot. But with all
new technology you just need some time to get  used to it. I wasn’t turned off cause views simply 
started to looked  alot nicer than they usually do. All the variable, method calling crap is out 
of the way. Helps alot when building nicely structured XHTML.

Custom helpers, loops, conditions and elements work. I am also using it for different output formats 
like JSON and even emails. For emails i was  really happy about a working ```{% raw %}{% trans %}{% endraw %}``` 
block implementation (everything in between is passed to i18n).

    {% raw %} 
    {% trans %}
    Hello {{ username }}!
    
    This is my mail body and i can translate it in X languages now.
    We love it ... {{ someotherVar }}
    {% endtrans %}
    {% endraw %}

_update_: doesn't work with variables anymore since 1.x... :-(

I think the most interesting aspect with custom view renderers is how you work with helpers. 
I decided to drop ```$this-&gt;``` for readability sake. I never had problems with collisions in 
my apps,  so why bother. You can access all helpers like you could pre-1.3.

    {% raw %}{{ time.nice(user.created) }}{% endraw %}

What you also can do is using the “helpers” that twig offers. There are some handy filters. 
Here’s a example with “date”

    {% raw %}{{ user.created|date("m/d/Y") }}{% endraw %}

My favorite is the “trans” filter. It will pass the value to ```__('', true)```. Such a time saver..

    {% raw %}
    {{
      form.input('message', {
        'label': 'Your message'| trans,
        'error': {
          'notempty': 'Please enter a message'| trans
        }
      })
    }}
    {% endraw %}

These are just some examples, but the format will stay. Here’s a final example using a custom 
helper and a cake array.

    {% raw %}
    {{
      gravatar.image(post.User.email, {
        'size': '30',
        'default': 'identicon'
      })
    }}
    {% endraw %}

As you can see, there is hardly anything you can’t do with the  current implementation. Well..
except for one thing: embeded PHP. But  who would want that with Twig, right?

### SQL Dump?

The original sql-dump element is 80% php code and that’s not very  “twig”. Logic like that 
should be either in a helper, controller or  model. But i don’t wanna discuss practices here. 
I guess for what it  does it works. You prolly could write the ```sql_dump.ctp``` in twig somehow.. 
i was too scared. ;) For the said sql-dump i **installed DebugKit** which renders the log just as good.

### About elements

What i forgot to mention was the ```element()``` command. I’ve implemented it as twig tag.

    {% raw %} {% element 'some/element' %}{% endraw %}

### Bottom Line

Twig is fun to write views with. There’s a TextMate bundle available and a good documentation 
over at <a href="http://twig-project.org/" target="_blank">twig-project.org</a>. Couple that 
with ZenCoding and writing views is so much faster =)

Extending is fun too! I’ve started to add some filters that route to  cakephp helpers. The first 
one was “timeAgoInWords”. Shortened down to ```user.created|ago```. Other possible candidates 
are the NumberHelper and most of the  TimeHelper…. well. sky’s the limit and nothing stops you 
from using the  default interface that i described above.

I think Twig and Cake is a powerful combination. And i haven’t even talked about Twigs own filter 
arsenal. You can <a href="http://github.com/m3nt0r/cakephp-twig-view">get the Plugin at GitHub</a>. 

Feel free to play around with it. See the “examples” directory for all default layouts.
