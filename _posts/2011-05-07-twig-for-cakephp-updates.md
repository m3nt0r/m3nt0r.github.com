--- 
layout: post
title: "Twig for CakePHP: Updates"
tags: 
- CakePHP
- ctp
- github
- Projects
- twig
- views
---

## Twig for CakePHP: Updates

New features have been added to TwigView just recently. New filters, Better readme, 
Access to view object and experimental CakePHP 2.0-dev support.

### CakePHP 2.x Support

This one is experimental. Using changes made by BigClick in 
<a href="https://github.com/bigclick/cakephp-twig-view">his fork</a> i've remodeled the 
methods to act as proxy and detect if 2.x is being used. So this feature is completely 
transparent and the plugin will work in 1.2+, 1.3x and 2.0-dev without any changes required. 

At least in my quick tests it did ;) Enjoy.

### View Object

You can now access the view object within a template
    {% raw %} {{ _view.action }} {% endraw %}  //=> 'display'

### Two new filter sets

'basic' und 'number' and as the name suggest are shortcuts 
to the NumberHelper (me) and basic.php (Hiroshi Hoaki)

Display the debug (linenumber, pre+print_r) output
    {% raw %} {{ user|debug }} {% endraw %}

Display just the pre+print_r output
    {% raw %} {{ user|pr }} {% endraw %}

Display the value from a environment variable
    {% raw %} {{ 'HTTP_HOST'|env }} {% endraw %}

Convert byte integer to a humand readable size
    {% raw %} {{ '3535839525'|size }}    //=> 3.29 GB {% endraw %}

Formats a number with a level of precision.
    {% raw %} {{ '0.555'|p(2) }}    //=> 0.56 {% endraw %}

Display floating point value as currency value. USD, GBP and EUR only
    {% raw %}
     {{ '5999'|curr }}         // default, $5,999.00
     {{ '5999'|curr('GBP') }}  // £5,999.00
     {{ '5999'|curr('EUR') }}  // €5.999,00
    {% endraw %}

Formats a number into a percentage string.
    {% raw %} {{ '2.3'|pct }}    //=> 2.30% {% endraw %}

### Fancy Readme

I've added a decent readme with install and usage instructions.

[https://github.com/m3nt0r/cakephp-twig-view](https://github.com/m3nt0r/cakephp-twig-view)
