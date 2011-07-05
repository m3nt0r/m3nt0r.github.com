--- 
layout: post
title: Jailson! Access Control for CakePHP
tags: 
- acl
- auth
- CakePHP
- jailson
- plugin
- Projects
---

## Jailson! Access Control for CakePHP

I've written a access control plugin for CakePHP dubbed _Jailson_. It is completly transparent 
and auto-integrates with Auth (if present).

### Some examples from the README 

... because code says more than a thousand words.. =)

// simple in and out
{% highlight php %}
$this->User->lockAs('client'); // add user to client group
$this->User->release('client'); // remove user from client group
{% endhighlight %}

// related to another model
{% highlight php %}
$this->User->lockAs('admin_of', $this->Project);
{% endhighlight %}

// testing
{% highlight php %}$this->User->is('admin_of', $this->Project); // true
$this->User->isNot('admin_of', $this->Project); // false{% endhighlight %}

// array support
{% highlight php %}$this->User->lockAs(array('admin', 'member', 'reporter'), $this->Project);{% endhighlight %}

// and-testing
{% highlight php %}$this->User->is(array('member', 'reporter'), $this->Project); // true
$this->User->is(array('member', 'reporter', 'watcher'), $this->Project); // false
$this->User->is(array('member', 'reporter', 'admin'), $this->Project); // true{% endhighlight %}

// commit a test: save it to database.
{% highlight php %}$this->User->is('watcher_of', $this->Project, true); // where 'true' means: Create
$this->User->isNot('watcher_of', $this->Project, true); // where 'true' means: Delete{% endhighlight %}

// clear everything
{% highlight php %}$this->User->free(); // remove user from all groups{% endhighlight %}

That was the simple interface to setup roles.

### Syntax sugar

You might have noticed that i write "admin_of" instead of just "admin". This is just to make
the code more readable. Internally "admin_of" is translated to "admin" and also stored like that.

There are many other suffixes you can use like "admin_in" and so on. Use as you see fit.

### AuthComponent

The above was using the Behavior. Given that we attached it to our User model, which we 
also use for the AuthComponent, we can tell Auth to communicate with the Behavior to verify
if the current user is in a certain group.

Say i want 'add' and 'edit' action to be only available to Users who are logged in with 
an 'admin' account. The 'index' and 'view' action however may be requested by members too. 

Here's how you can set that up:

{% highlight php %}
public $components = array(
  'Jailson.AclAuth' => array(
    'deny' => array('*'), // if not in any group, reject
    'allow' => array( 
       'index' => array('member', 'admin'),
       'view' => array('member', 'admin')
       'add' => array('admin')
       'edit' => array('admin')
    )
  )
);
{% endhighlight %}

You can even do this on ```AppController``` level. The Allow/Deny rules will inherit if 
the actions match. For more information have a look at the README.

[http://github.com/m3nt0r/cakephp-jailson](http://github.com/m3nt0r/cakephp-jailson)

