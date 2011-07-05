--- 
layout: post
title: Eventful - Event Driven CakePHP Development
tags: 
- behavior
- CakePHP
- component
- eventful
- plugin
- Projects
---

## Eventful - Event Driven CakePHP Development

As promised i've created a repo for the event system i was working on.

It’s currently under heavy development, yet ready to use. I don’t think
the interface will change much from here on out. The installation is similar 
to the DebugKit. Put the “eventful” plugin into your plugins folder and add the Behavior or
Component to your app. This will include  all dependencies and the system is ready to use.

Only one thing is different from regular plugins. There is a seperate “events” folder 
which is an empty layout for the system and the place for your event listener classes.

### How to use it?

I’ve created a (messy) README which goes on about how to use it, but basicly the workflow is:

1. add the component (and/or behavior),
2. use the dispatch/dispatchEvent method in your actions/methods,
3. create or modify the event listener class and add a matching “on” method.
4. go nuts.

### Just codes plz

{% highlight php %}
// step 1
class UsersController extends AppController {
  var $components = array('Eventful.Event');
}
{% endhighlight %}

{% highlight php %}
// step 2
class UsersController extends AppController {
  var $components = array('Eventful.Event');

  function logout() {
	
	// your usual action code ...
    $this->Auth->logout();
	
    // ... send a event called "UserLogout"

    $this->Event->dispatch('UserLogout', array(
      'auth' =>; $this->Auth->user()
    ));
  }
}
{% endhighlight %}

{% highlight php %}
// step 3 in File: /app/events/controller/users_controller_events.php

class UsersControllerEvents extends AppControllerEvents {

  // do something on "UserLogout";
  function onUserLogout() {
    $this->log('User logged out...');
  }
}
{% endhighlight %}

### Calling all units!

Unlike the original implementation the current triggers all handlers of the same name. 
So if you have a "UserLogout" event fired from ```UsersController::logout()```
action the ```dispatchEvent()``` method will trigger all possible _candidates_ regardless 
in which listener class (f.e. UnrelatedControllerEvents) the event handler is defined. 

So in addition to the above. the following would be executed too:

{% highlight php %}
// example, note the differen class name
class MembersControllerEvents extends AppControllerEvents {

  // do something on "UserLogout"
  function onUserLogout($event) { // import $event data from call param
    if ($event->auth['isMember'])
        $this->log('Member '.$event->auth['name'].' logged out...');
  }
}
{% endhighlight %}

### Plugin Support

The System is also plugin aware. If you want to enrich your base  application with 
event handlers from plugins just copy the “events”  folder layout into the plugin 
directory and prefix the class filenames  with the plugin name. (just like app_controller).

{% highlight php %}
# /app/plugins/pizza/events/controller/pizza_users_controller_events.php
class PizzaUsersControllerEvents extends AppControllerEvents {
    // your event handlers
}
{% endhighlight %}

### Sold?

You can find it on github:
[http://github.com/m3nt0r/eventful-cakephp](http://github.com/m3nt0r/eventful-cakephp)

Enjoy! 


