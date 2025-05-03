# Flask Cheat Sheet

## Table of contents
Creating a Simple App
Structuring an Application with Blueprints
Creating Object-Based Configuration
Using the Jinja2 Template Engine
Creating Models with SQLAlchemy
Using Database Migrations
Creating a Login Manager
Connecting to a MySQL database

# create s Simple APP
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
	return 'Hello, World!'

if __name__ == '__main__':
	app.run()
# Structuring an Application with Blueprints
run.py
project/
	__init__.py
	config.py
	forms.py
	models.py
	admin/
		__init__.py
		routes.py
	main/
		__init__.py
		routes.py
	templates/
		index.html
	static/
		css/
			style.css
   # In run.py
   from project import app

if __name__=='__main__':
	app.run()
# In project/__init__.py
from flask import Flask
from project.main.routes import main
from project.admin.routes import admin

app = Flask(__name__)

app.register_blueprint(main, url_prefix='/')
app.register_blueprint(admin, url_prefix='/admin')
# In project/main/routes.py
from flask import Blueprint

main = Blueprint('main', __name__)

@main.route('/')
def index():
	return "Hello, World! This is the main page."
# In project/admin/routes.py:
from flask import Blueprint

admin = Blueprint('admin', __name__)

@main.route('/')
def index():
	return "Hello, World! This is the admin page."

 # creating Objects-Based Configuration
 class BaseConfig(object):
	SECRET_KEY = os.environ.get('SECRET_KEY') or 'abcdef123456'
	DEBUG = False
	TESTING = False

class DevelopmentConfig(BaseConfig):
	DEBUG = True
	TESTING = True

class TestingConfig
	DEBUG = False
	TESTING = True

 --- And then __init__.py include:
 from flask import Flask
from threechan import config

app = Flask(__name__)
app.config.from_object(config.DevelopmentConfig)
# Using the jinja2 Template Engine
-- Rendering a template from main/routes.py
from flask import Blueprint, render_template

@main.route('/')
def home():
	posts = [
		{
			"body": "Hello, this is a post",
			"timestamp": "This is a date and time",
		}
	]
	
	return render_template("home.html", posts=posts)


 
 
