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

* [http-api-design](https://geemus.gitbooks.io/http-api-design/content/)
* TODO

## Codereview

* TODO

## Rails

### General

* Generate necessary [Bundler binstubs] for the project, such as `rake` and
  `rspec`, and add them to version control.
* use inline callbacks `after_create { SomeJob.perform_later(user_id) } `

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
* use timeouts for long running Postgres migrations
```ruby
def change
  reversible do |direction|
    direction.up   { execute("SET SESSION statement_timeout = 0;") }
    direction.down { execute("SET SESSION statement_timeout = 0;") }
  end
  ...
end
```

[fkey]: http://robots.thoughtbot.com/referential-integrity-with-foreign-keys

### Query

* use pluck and distinct for uniq single attribute `Location.order(:country).distinct.pluck(:country)`
* use class methods over scopes
```ruby
  def self.featured
    where(featured_athlete: true)
  end
```
*  for pessimistic locking use  [with_lock](https://github.com/rails/rails/blob/a913af96e0e46ca6637bca8f56282608628991eb/activerecord/lib/active_record/locking/pessimistic.rb#L61-L74)
* TODO  

### Routes

* limit resources with only `resources :guides, only: [:index, :show]`


## Ruby

* TODO 1
* TODO 2


## RSpec

* Write request specs for api's [request-spec](https://www.relishapp.com/rspec/rspec-rails/docs/request-specs/request-spec)
* Stub Env with `allow(Rails).to receive(:env).and_return(ActiveSupport::StringInquirer.new("production"))`
* use have_enqueued_job matcher for ActiveJob [have_enqueued_job](http://www.relishapp.com/rspec/rspec-rails/v/3-4/docs/matchers/have-enqueued-job-matcher)

## Postgres

* TODO 1
* TODO 2

## Writing 

* Use [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
