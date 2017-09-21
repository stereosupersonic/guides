Rails	
======

## Heroku

https://devcenter.heroku.com/articles/getting-started-with-rails5

## Start a new project

http://guides.rubyonrails.org/getting_started.html#creating-a-new-rails-project

https://medium.com/craft-academy/getting-started-with-rails-tests-continuous-integration-deployment-7b5bfec905a5

### update rails

```gem install rails ```

### create a new project with posgres

```rails new radio-logger --database=postgresql```

### Add useful gems

```
#haml
gem "haml-rails"

#boostrap
gem "bootstrap-sass"

group :development do
  gem "annotate",              require: false
  gem "guard",                 require: false
  gem "guard-livereload",      require: false
  gem "guard-rspec",           require: false
  gem "pry",                   require: false
  gem "pry-nav",               require: false
  gem "simplecov",             require: false
end

group :test, :development do  
  gem "rspec-rails"
end
```

```bundle install```

```bundle exec rails generate rspec:install```

### Rubocop

group :development do
  gem "rubocop", require: false
end

``` touch .rubocop.yml ```

add config to .rubocop.yml

enable git hook to check rubocop before push

 *.git/hooks/pre-push*
 
```
#!/bin/sh
echo "pre-push"

echo "Starting rubocop"
bundle exec rubocop

if [ $? -ne 0 ]; then
    echo ""
    echo ""
    echo "Rubocop failed; push aborted!"
    exit 1
fi

echo "All pre-push checks passed! Pushing to remote"
```

``` chmod +x .git/hooks/pre-push ```


### Database

cp -a config/database.yml config/database.sample.yml

add to .gitignore

```
config/database.yml
```

Rails
-------

* TODO 1
* TODO 2

Ruby
-------

* TODO 1
* TODO 2
