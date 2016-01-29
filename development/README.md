# Development


## General

* [Keep the code simple].

### [Sandi's Rules](https://robots.thoughtbot.com/sandi-metz-rules-for-developers)

* Classes can be no longer than one hundred lines of code.
* Methods can be no longer than five lines of code.
* Pass no more than four parameters into a method. Hash options are parameters.
* Controllers can instantiate only one object. Therefore, views can only know about one instance variable and views should only send messages to that object (@object.collaborator.value is not allowed).


[Keep the code simple]: http://www.readability.com/~/ko2aqda2

## Codereview

* TODO

## Rails

### Background Jobs
* don't change a ActiveJob interface

### Migrations
* check if all indices are
* Set an empty string as the default constraint for non-required string and text fields 
```ruby
  create_table :users  do |t|
    ...
     t.string :name, null: false, default: ''
  end
```
## Ruby

* TODO 1
* TODO 2
