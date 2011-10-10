Creating a Jekyll App on Heroku Cedar with custom Jekyll Buildpack (from GitHub)
===

Setup Jekyll
---

The first thing you have to do is install the jekyll gem.

    gem install jekyll

Clone the git repository
---

    git clone git@github.com:markpundsack/jekyll-heroku.git
    cd jekyll-heroku
    
Let's test it locally
---

    jekyll --server --auto

Open your browser and go to http://localhost:4000.

You should see "Hello World".

Deploying to Heroku
---

Install the Heroku gem

    gem install heroku

Create a Heroku app

    heroku create --stack cedar
    
Point Heroku to our custom buildpack

    heroku config:add BUILDPACK_URL="http://github.com/markpundsack/heroku-buildpack-jekyll.git"

Deploy!

    git push heroku master

Test it:

    heroku open

Creating a Jekyll App on Heroku Cedar (Manually)
=== 

Setup Jekyll
---

The first thing you have to do is install the jekyll gem.

    gem install jekyll

Create the site structure
---

Create the app directory

    mkdir jekyll-app

and create the following files:

    cd jekyll-app
    touch _config.yml
    touch index.html
    mkdir _posts
    mkdir _layouts
    touch _layouts/default.html

"Hello World" Jekyll
---

Let's create a Layout. Open _layouts/default.html and add:

    <html>
    <body>
      {{ content }}
    </body>
    </html>

Now we need an index page. Open index.html and add:

    ---
    layout: default
    title: Jekyll Example Site
    ---

    <h1>Hello World</h1>

Let's test it locally:

    jekyll --server --auto

Open your browser and go to http://localhost:4000

You should see "Hello World"

Deploying to Heroku
---

First, install the Heroku gem

    gem install heroku

Since Cedar will run Jekyll and generate the _site files automatically, they don't need to be checked into git
    
    echo _site >> .gitignore
    
Create a git repo and commit

    git init .
    git add .
    git commit

Create a Heroku app

    heroku create --stack cedar

Point Heroku to our custom buildpack

    heroku config:add BUILDPACK_URL="http://github.com/markpundsack/heroku-buildpack-jekyll.git"

Deploy!

    git push heroku master

Test it:

    heroku open
