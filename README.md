nprapps' Project Template
=========================

Copying the template
--------------------

```
git clone git@github.com:nprapps/app-template.git $NEW_PROJECT_NAME
cd $NEW_PROJECT_NAME
git remote rm origin
git remote add origin https://github.com/nprapps/$NEW_PROJECT_NAME.git
git push -u origin master
```

Configure the project
---------------------

* Update ``app_config.py`` with the name of the new project.

Install requirements
--------------------

Node.js is required for the JST compiler. If you don't already have it, get it like this:

```
brew install node
```

Then install the project requirements:

```
npm install less grunt grunt-contrib-less grunt-contrib-jst
mkvirtualenv $NEW_PROJECT_NAME
pip install -r requirements.txt
```

Generating index.html
---------------------

* Run ``fab make_index`` to generate a blank index page.
* <strong>Or</strong>, for a table, run ``fab make_table:data/example.csv`` to use the table template.
* Uncomment and update the ad code and Facebook tags at the top of ``www/index.html`` (or make yourself a ticket to do it later).

Running the project locally
---------------------------

```
workon $NEW_PROJECT_NAME
fab build_assets
cd www
python -m SimpleHTTPServer
```

Visit ``localhost:8000`` in your browser.

Working with static assets
--------------------------

The asset pipeline is now handled with [grunt](http://gruntjs.com). 

To compile LESS to CSS, compile javascript templates to JS and package assets with webassets:

```
workon $NEW_PROJECT_NAME
fab grunt
```

To automatically run these processes when you change files, simply run:

```
workon $NEW_PROJECT_NAME
fab watch
```

Deploying the project
---------------------

```
fab staging master deploy
```

Deploying to a server
---------------------

The current configuration is for running cron jobs only. Web server configuration is not yet included.

* In ``fabfile.py`` set ``env.deploy_to_servers`` to ``True``.
* Run ``fab staging master setup`` to configure the server.
* Run ``fab staging master deploy`` to deploy the app. 