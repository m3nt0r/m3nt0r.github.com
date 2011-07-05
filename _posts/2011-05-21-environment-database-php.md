--- 
layout: post
title: "QuickTip: Environment & Database.php"
tags: 
- bootstrap
- CakePHP
- config
- configuration
- database
- environment
- example
- Quicktips
---

## QuickTip: Environment & Database.php

In this post i am going to explain how to use the 
[Environment library from Rafael Bandeira](https://github.com/m3nt0r/cakephp-env-example/blob/master/vendors/environment.php) 
to automatically configure your Database connection based 
on the environment your app is running in.

Environment looks at the ```SERVER_NAME``` (or configurable conditions) and gives it a name and 
applies a defined set of core options. The method i am explaining uses this info to choose which 
database config to load, by adding some magic into ```Database::__construct```.

A good practice is to create a file in ```config``` with all your environment configs.

Before we begin, [download the environment php](https://github.com/m3nt0r/cakephp-env-example/blob/master/vendors/environment.php) 
and put it into your ```vendors``` folder.

### Setting up our environments.php

Create a file called ```config/environments.php```. In this example we want to create
three different environments: 

- development
- staging
- production

{% highlight php %}
// import the lib
App::import('Vendor', 'Environment');

// config
Environment::configure('development',
  array(
    'server' => 'localhost'     // if SERVER_NAME == 'localhost'
   ),
   array(
     'debug' => 2               // Configure::write('debug', 2)
   )
);

Environment::configure('staging',
  array(
    'server' => 'dev.myapp.com'
  ),
  array(
    'debug' => 1
  )
);

Environment::configure('production',
  true,
  array(
     'debug' => 0 
  )
);

// run
Environment::start();
{% endhighlight %}

### Let bootstrap know about it

To use this file when starting the app (visiting it in your browser) add it to the ```config/bootstrap.php```.

{% highlight php %}
config('environments');
{% endhighlight %}

### Adjusting the database.php

Now to the final part. The ```config/database.php```

{% highlight php %}
class DATABASE_CONFIG {

  // This is the default, generate by bake

  var $default = array(
    'driver' => 'mysql',
    'persistent' => false,
    'host' => 'localhost',
    'login' => 'root',
    'password' => '',
    'database' => 'test',
    'encoding' => 'utf8'
  );

  // Add properties for each of our environments

  var $development = array(
    'login' => 'dev',
    'password' => 'dev-pw',
    'database' => 'myapp_development',
  );

  var $staging = array(
    'login' => 'staging',
    'password' => 'staging-pw',
    'database' => 'myapp_staging',
  );

  var $production = array(
    'login' => 'live',
    'password' => 'live-pw',
    'database' => 'myapp_live',
  );

  // Then add a __construct to this class to run some code when cake loads it

  function __construct() {

    // once Environment has decided where we at, it will write the name into Configure.
    if ($environment = Configure::read('Environment.name')) {

      // now i am gonna test if theres a property of the same name
      if (isset($this->{$environment})) {

        // if so, i then merge any options into $default.
        $this->default = array_merge($this->default, $this->{$environment});
      }
    }

    // if everything above went smooth, $this->default now has the correct login info.
    // Since we are using $default i dont need to change anything else in my app.
  }
}
{% endhighlight %}

Pretty neat, eh? If you want to check it out i've create a 
[repo on GitHub](https://github.com/m3nt0r/cakephp-env-example) where you 
can download/fork a working CakePHP 1.3 example.

[https://github.com/m3nt0r/cakephp-env-example](https://github.com/m3nt0r/cakephp-env-example)

Enjoy!
