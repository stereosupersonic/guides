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
* TODO

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
* use inline callbacks `after_create { SomeJob.perform_later(user_id) } ` but better not use callbacks
* use `.none?` over `.blank?` it's straightforward
* use `model.invalid?` instead of `!model.valid?`
* use `users.many?` instead of `users.size > 1` use 
* use `User.find_each(batch_size: 100)` instead of `User.all.each`
* Use private instead of protected when defining controller methods.
* Name initializers for their gem name.
* Order ActiveRecord associations alphabetically by association type, then
  attribute name. 
```ruby
class SomeClass
  belongs_to :tree, class_name: Plant
  has_many :apples
  has_many :watermelons

  validates :name, presence: true, uniqueness: true
end
```
* Order ActiveRecord validations alphabetically by attribute name.
* Order ActiveRecord associations above ActiveRecord validations.
* Order controller contents: filters, public methods, private methods.
* Order i18n translations alphabetically by key name.
* Order model contents: constants, macros, public methods, private methods.

### views 
* Put application-wide partials in the [`app/views/application`] directory.
* Use `def self.method`, not the `scope :method` DSL.
* Use the default `render 'partial'` syntax over `render partial: 'partial'`.
* Use `link_to` for GET requests, and `button_to` for other HTTP verbs.

[Bundler binstubs]: https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs
### validations
* write validators app/validators/safe_for_work_validator.rb
* Use new-style `validates :name, presence: true` validations, and put all validations for a given column together.

### Background Jobs
* don't change a ActiveJob interface

### Migrations
#### foreign key
* [Add foreign key constraints][fkey] in migrations.
* * bin/rails generate migration CreateActions project:references
* use ` t.references :employee ` for setting an index
```ruby
class AssociatePostsWithUsers < ActiveRecord::Migration
  def change
    add_column :posts,
               :user_id,
               null: false,
               index: true
    add_foreign_key :posts,
                    :users
  end
end
```
#### global
* check if all necessary indices are set
* Name date columns with `_on` suffixes.
* Name datetime columns with `_at` suffixes.
* Name time columns (referring to a time of day with no date) with `_time`
  suffixes.
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
* use sql
```ruby
 def up
    connection.update(<<-SQL)
      UPDATE users SET admin = 'f'
    SQL
  end
```
* add uniq index for uniq validator [Blog Post](https://robots.thoughtbot.com/the-perils-of-uniqueness-validations)
```ruby
class CreateUsers < ActiveRecord::Migration
  create_table :users do |t|
    t.string :email

    t.timestamps null: false
  end

  add_index :users, :email, unique: true
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
* Avoid `member` and `collection` routes.
* limit resources with only `resources :guides, only: [:index, :show]`


## Ruby

* TODO 1
* TODO 2

## RSpec

* use instance_double for stubs [doc](https://www.relishapp.com/rspec/rspec-mocks/v/3-0/docs/verifying-doubles/using-an-instance-double) 
* Write request specs for api's [request-spec](https://www.relishapp.com/rspec/rspec-rails/docs/request-specs/request-spec)
* Stub Env with `allow(Rails).to receive(:env).and_return(ActiveSupport::StringInquirer.new("production"))`
* use have_enqueued_job matcher for ActiveJob [have_enqueued_job](http://www.relishapp.com/rspec/rspec-rails/v/3-4/docs/matchers/have-enqueued-job-matcher)
* TODO 2

## Postgres

* TODO 1
* TODO 2

## Writing 

* Use [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
