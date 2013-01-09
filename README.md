backbone-event-channels
=======================

A simple **factory** for creating and referencing **namespaced Backbone event aggregators**, or **'channels'**, on the fly.

Motivation
==========
The [BackboneJS](http://backbonejs.org/) events system is a powerful tool, but often-times programmers have to resort to dependency injection and tight coupling to pass events through several layers of code, from one disparate object to another. In light of this problem, many have turned to **event aggregators** -- a centralized dispatcher every object can access. As of December 13th, this functionality is even built into Backbone 0.9.9 (the Backbone object itself acts as a global event aggregator). 

While a centralized aggregator works well, as programmers, we often try to avoid global cesspools. Thus, this project. With the `BackboneEventChannelFactory`, you now have the power to separate events into namespaced channels as you need them.

For further reading, see Derick Bailey's blog posts on event aggregators:
* [References, Routing, And The Event Aggregator...](http://lostechies.com/derickbailey/2011/07/19/references-routing-and-the-event-aggregator-coordinating-views-in-backbone-js/)
* [Revisiting The Backbone Event Aggregator...](http://lostechies.com/derickbailey/2012/04/03/revisiting-the-backbone-event-aggregator-lessons-learned/)

Installation
============
The `BackboneEventChannelFactory.js` file is designed to be used in a [RequireJS](http://requirejs.org/) environment.

If you're using RequireJS, just define `BackboneEventChannelFactory` as per usual.

If you're not using RequireJS, simply delete the `define([],function(){})` wrapper and associated `return BackboneEventChannelFactory` statement. You'll then have to ensure that `_` and `Backbone` are available in whatever scope you place the factory definition in.

Example
=======
**To create/get a channel**, you might do something like this:
```javascript
this.testChannel = BackboneEventChannelFactory.getChannel('testChannel');
```

Once done, you can **bind to events on your channel** as you would any other Backbone object:
```javascript
//(in Backbone 0.9.2)
this.testChannel.on('test', function(){ alert('woot');});` 
// or (in Backbone >0.9.9)
obj.listenTo(this.testChannel, 'test', function(){ alert('woot');});` 
```

If you find you need to **delete a channel**, you must **both** unregister it from the factory AND delete ALL local references:
```javascript
// delete local reference(s)
delete this.testChannel;
// unregister/delete factory's reference
BackboneEventChannelFactory.unregisterChannel('testChannel');
// Now the garbage collector is free to delete the actual object.
```
