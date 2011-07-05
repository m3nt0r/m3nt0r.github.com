--- 
layout: post
title: "QuickTip: How to overwrite HtmlHelper tags"
tags: 
- CakePHP
- helper
- html
- html-helper
- html-tags
- Quicktips
- views
---

## QuickTip: How to overwrite HtmlHelper tags

In some cases you may find it desirable to overwrite the tag templates
used by the HtmlHelper. For example if you put all your assets onto a CDN
and don’t want to put the hostname in front of all paths (messy..).

With this small modification in the AppHelper class you can do that
in bootstrap using Configure, which also allows you to make the tags
conditional if you want.. In short: _flexibility_, wee!

{% highlight php %}
// The code:
class AppHelper extends Helper {
  function __construct() {
    if ($this->toString() == 'HtmlHelper') {
      $tags = Configure::read('HtmlHelper.tags');
      if (is_null($tags)) $tags = array();
         $this->tags = am($this->tags, $tags);
    }
  }
}
{% endhighlight %}

With this in place (file goes to app root and is called app_helper.php) you can 
now configure your tags whereever you like passing an array with ```sprintf``` 
templates, like so:

{% highlight php %}
Configure::write('HtmlHelper.tags', array(
  'image' => '<img src="http://cdn.domain.com%s" %s/>',
));
{% endhighlight %}

yay!

**Note**: is_null checks if Configure value is set. This way you are not 
forced to set a empty array to your bootstrap.

