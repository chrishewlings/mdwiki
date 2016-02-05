RVM
---

- *RVM* is a tool that can be installed that manages different installs of Ruby, like VirtualEnv for Python.

`rvm install $VERSION` - Installs a version of ruby for use with RVM. Will download binaries or compile from source as necessary
`rvm --default use 2.2` - Assigns version as the default instance of Ruby for all sessions. 
`rvm use 2.2` - Assigns version as the instance for this session. 

GEM
---

- *gem* is a tool to install and manage packages (like *Rails*)for usage in Ruby
`gem install $PACKAGE`

Heroku
------

- *Heroku* is a staging area of sorts -- it can integrate with your shell using a 'toolbelt' that allows you to deploy webapps quickly 


Rails
-----

- *Rails* is a framework for making webapps.
`rails new $app` will make a skeleton of a webapp 'bundle' named $app/ 
`rails s` will start a server instance in the current bundle

`rails generate scaffold $OBJECT $SUBOBJECT:$TYPE` - generates a 'scaffold' with name $OBJECT and $SUBOBJECT with $TYPE (string, integer)
`rake db:migrate` takes those 'scaffold' objects and converts them into a database form, accessible at the root dir/$OBJECTs

Deploy to Heroku
----------------

`git init` - to create a new repo for your webapp
`git add -A` - to add and commit all files
`heroku create` - to create a new app instance on heroku

Tip:
- For Heroku deployment, change:
````
gem 'sqlite3'
````
to 
````
group :development, :test do
	gem 'sqlite3'
end

group :production do
	gem 'pg'
	gem 'rails_12factor'
end
````
- This will use SQLite for development and testing environments but switch to PostgreSQL, which is more powerful. 

`bundle install --without production` - will prep a bundle without the `production` environment included.

- Set the root route to your $OBJECT(s):
	+ Edit $APPDIR/config/routes.rb and add `root '$OBJECT#index'

Finally, add, commit, push, and build with `rake`:
````
$ git add .
$ git commit -m "message"
$ git push heroku master
$ heroku run rake db:migrate
````

