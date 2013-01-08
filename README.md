backbone-event-channels
=======================

A simple factory for creating and referencing namespaced Backbone event aggregators, or 'channels', on the fly.

Installation
============
The BackboneEventChannelFactory.js file is designed to be used in a RequireJS environment.

If you're using RequireJS, just import BackboneEventChannelFactory as per usual.

If you're not using RequireJS, simply delete the `define([],function(){})` wrapper and associated `return BackboneEventChannelFactory` statement. You'll then have to ensure that `_` and `Backbone` are available in whatever scope you place the factory definition in.
