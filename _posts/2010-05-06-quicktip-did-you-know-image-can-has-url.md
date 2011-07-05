--- 
layout: post
title: "QuickTip: Did you know? image() can has url!"
tags: 
- CakePHP
- html
- html-helper
- image
- Quicktips
- router
- url
- views
---

## QuickTip: Did you know? image() can has url!

How to save you alot of code on image links while still being able to use the 
full power of the cakephp router.

Most of you probably know the following piece of code from the ```default.ctp```:

{% highlight php %}
echo $html->link(
   $html->image('cake.power.gif', array(
       'alt'=> __("CakePHP...", true),
       'border'=>"0"
   )),
   'http://www.cakephp.org/',
   array('target' => '_blank'), null, false
);
{% endhighlight %}

This displays the small “CakePHP Power” badge with a link to the CakePHP website.

Much code for just a image surrounded with a link, eh?

The ```$html->image()``` method has a option called ‘url’ that basicly does the same thing. Only limitation is that you can’t pass attributes to the link tag. But it isn't always needed. If that's true in your case try the following.

The _same thing_, only without the clutter:

{% highlight php %}
echo $html->image('cake.power.gif', array(
   'url' => 'http://www.cakephp.org',
   'alt' => __('CakePHP...', true),
   'border' => 0
));
{% endhighlight %}

There you have it. Of course ```‘url’``` accepts arrays and everything else you would expect since it passes the value straight to ```Helper::url()```.

Enjoy!
