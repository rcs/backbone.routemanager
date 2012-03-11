backbone.routemanager
=====================

Created by Tim Branyen [@tbranyen](http://twitter.com/tbranyen)

Provides missing features to the Backbone.Router.

Depends on Underscore, Backbone and jQuery.  You can swap out the 
jQuery dependency completely with a custom configuration.

## Tutorials and Screencasts ##

## Download & Include ##

Development is fully commented source, Production is minified and stripped of
all comments except for license/credits.

* [Development](https://raw.github.com/tbranyen/backbone.routemanager/master/backbone.routemanager.js)
* [Production](https://raw.github.com/tbranyen/backbone.routemanager/master/dist/backbone.routemanager.min.js)

Include in your application *after* jQuery, Underscore, and Backbone have been included.

``` html
<script src="/js/jquery.js"></script>
<script src="/js/underscore.js"></script>
<script src="/js/backbone.js"></script>

<script src="/js/backbone.routemanager.js"></script>
```

## Usage ##

### Defining a RouteManager ###

A route manager is your **MasterRouter**, you will be able to define any number
of **SubRouters**, but you will always reference the manager in your navigates.

*Assuming you have an app namespace*

``` javascript
// A basic route manager, works just like a Backbone.Router (cause it is one)
var AppRouter = new Backbone.RouteManager({
  routes: {
    "": "index"
  },

  index: function() {
    window.alert("Navigated successfully");
  }
});

// Create a new instance of the app router
app.router = new AppRouter();

// Trigger the index route
app.router.navigate("", true);
```

## Named params object ##

All route callbacks get access to a special object on the Router called
`params` which maps directly to the variables and splats defined in the route.

``` javascript
// A basic route manager, works just like a Backbone.Router (cause it is one)
var AppRouter = new Backbone.RouteManager({
  routes: {
    ":id/*path": "index"
  },

  index: function(id, path) {
    // You can use the arbitrarily named args you define... or you can use the
    // params object on the router.
    window.alert(id == this.params.id);
    window.alert(path == this.params.path);
  }
});

// Create a new instance of the app router
app.router = new AppRouter();

// Trigger the index route
app.router.navigate("5/hi", true);
```

This is useful for a number of reasons including a special significance for
`before/after` filters that are defined later on.

## Nested Routers ##

So far we haven't seen anything special that we couldn't do already with a
normal `Backbone.Router`.  One of the major benefits of RouteManager is that
you can define nested Routers.  These are defined in the same way as normal
routes, except you pass a `Backbone.Router` class instead.

Nested Routers are just normal `Backbone.Router`'s.

For example:

``` javascript
var SubRouter = Backbone.Router.extend({
  routes: {
    "": "index"
  },

  index: function() {
    window.alert("SubRouter navigated successfully");
  }
});

var AppRouter = Backbone.RouteManager.extend({
  routes: {
    // Define a root level route
    "": "index",

    // Define a sub route
    "sub/": SubRouter
  },

  index: function() {
    window.alert("MasterRouter navigated successfully");
  }
});

// Create a new instance of the app router
app.router = new AppRouter();
```

### Before/After filters ###

To be written...
