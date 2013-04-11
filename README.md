# Ember data Factories

For use instead of fixtures for testing with more realistic data ;)

## Define factories

```coffeescript
Ember.factory.create 'post', {
  name: 'Kris'
  age: ->
    20 + rand(20) + rand(20)
  email: ->
    "email#{rand(200)}@gmail.com"
}
```

Or like:

```coffeescript
Ember.factory.create('post').properties
  name: 'Kris'
  age: ->
    20 + rand(20) + rand(20)
  email: ->
    "email#{rand(200)}@gmail.com"
```

## Build a single model using factory for testing

`post = Ember.Factory.build('post')`

## Building multiple models

`posts = Ember.Factory.build('post', 2)`

## Experimental (under dev - untested)

Note that when you create multiple models, you will pass the index as an argument to any factory function, so you can fx change `email` to:

```coffeescript
Ember.factory.create('post').properties
  email: (n) ->
    "email#{n || 1}@gmail.com"
```

And it should create posts with `['email1@gmail.com', 'email2@gmail.com']

For global counting, use the `Ember.factory.counter('posts')`
Note that when the factory instantiates a model, it creates an `f` property pointing to the factory class, so you can use the factory class method from your model in case you have special factory methods there. You can also use f inside your usual factory methods:

```coffeescript
Ember.factory.create('post').properties
  email: (n) ->
    "email#{f.count('emails')}@gmail.com"
```
