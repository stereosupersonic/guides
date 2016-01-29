# Development

* [thoughtbot Best Practices](https://github.com/thoughtbot/guides/blob/master/best-practices/README.md)

## General

* [Keep the code simple].
* Limit collaborators of an object (entities an object depends on).
* Limit an object's dependencies (entities that depend on an object).
* Prefer composition over inheritance.
* Prefer small methods. Between one and five lines is best.
* Prefer small classes with a single, well-defined responsibility. When a class exceeds 100 lines, it may be doing too many things.
* [Tell, don't ask](http://robots.thoughtbot.com/post/27572137956/tell-dont-ask)
* 

### [Sandi's Rules](https://robots.thoughtbot.com/sandi-metz-rules-for-developers)

* Classes can be no longer than one hundred lines of code.
* Methods can be no longer than five lines of code.
* Pass no more than four parameters into a method. Hash options are parameters.
* Controllers can instantiate only one object. Therefore, views can only know about one instance variable and views should only send messages to that object (@object.collaborator.value is not allowed).


[Keep the code simple]: http://www.readability.com/~/ko2aqda2
## Design

### API
* [http-api-design](https://github.com/interagent/http-api-design)
* 
## Codereview

* TODO

## Rails

### General

* Generate necessary [Bundler binstubs] for the project, such as `rake` and
  `rspec`, and add them to version control.


[Bundler binstubs]: https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs

### Background Jobs
* don't change a ActiveJob interface

### Migrations
* [Add foreign key constraints][fkey] in migrations.
* check if all indices are
* Set an empty string as the default constraint for non-required string and text fields 
```ruby
  create_table :users  do |t|
    ...
     t.string :name, null: false, default: ''
  end
```

[fkey]: http://robots.thoughtbot.com/referential-integrity-with-foreign-keys

## Ruby

* TODO 1
* TODO 2


## RSpec

* Write request specs for api's [request-spec](https://www.relishapp.com/rspec/rspec-rails/docs/request-specs/request-spec)
* TODO 2

## Postgres

* TODO 1
* TODO 2
