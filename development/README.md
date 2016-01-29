# Development


## General


* [Keep the code simple].

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
