Django is a free and open source tool used to store data into a lightweight SQLite database file. It is a high level and flexible Python web framework. In this article, we will explain how you can make the installation and configuration of PostgreSQL in order to be able to use it with Django applications on Ubuntu.

Let’s start by introducing the PostgreSQL. In fact it is an open source object relational database system. It has been released since 15 years, during which it earned a strong reputation due to its reliability, data integrity and correctness. PostgreSQL could be used with all existing operating systems, such Linux, UNIX and windows. All the data types are existed with this tool such INTEGER, NUMERIC, BOOLEAN, CHAR, VARCHAR, DATE, and others. This tool also supports storage of binary large objects, including pictures, sounds and videos.

Before starting it is required to have a clean Ubuntu server instance with a non-root user set up which also must be configured using “sudo” privileges”.

Configure PostgreSQL With Django Application
Installing the needed components from Ubuntu repository:

We will start our tutorial by installing all the needed components from our Ubuntu repository. So we will need the “pip”, python package manager, the database software and the associated libraries to interact with them. We will use the following command to do this:

	sudo apt-get update
	sudo apt-get install python-pip python-dev libpq-dev postgresql postgresql-contrib
	Create Database and Database user:

There is an operating system named “postgres” which was created during the installation of the Postgres to correspond to the postgres PostgreSQL administrative user. So it is required to change into this user to be able to perform administrative tasks using:

	sudo su - postgres
The “peer authentification” is used automatically by Postgres with local connections. It means that if the user’s operating system username corresponds to a valid Postgres username, so the connection will be without authentication. Now you can log into the Postgres session by using the following command:

	psql
We will start by creating the Database for our project. So will give it the name: ”projectdata” as the given name with the installation of this tool on Centos 07 in our previous article. Of course you can make your own name:

	CREATE DATABASE projectdata;
It is important to finish each command at SQL with semicolon. Now we will create a database user which will be used to connect to and interact with the database, so you have to enter your password here:

	CREATE USER projectdatauser WITH PASSWORD ‘password’;
We will make some changes for the connection parameters using the following commands:

	ALTER ROLE projectdatauser SET client_encoding TO ‘utf8’;
	ALTER ROLE projectdatauser SET default_transaction-isolation TO ‘read committed’
	ALTER ROLE projectdatauser SET timezone TO ‘UTC’;
Now we will give our database user access rights to the database already created using the following command:

GRANT ALL PRIVILEGES ON DATABASE projectdata TO projectdatauser;
Then typing the following command to exit the SQL prompt:

	\q
And the last command in this section is used to exit the postgres user’s shell session.

	exit
Installation of Django:

Now we will start the installation of our Django and all its dependencies within Python virtual environment. To get the virtual environment package you have to use the following command:

	sudo pip install virtualenv
Then use the following command to have a directory for your Django project:

	mkdir ~/projectdata
	cd ~/projectdata
And to finish the creation of your virtual environment use the following command:

virtualenv projectdataenv
Using the previous command, you will have a local copy of python and pip into our made directory projectdataenv (you can call it with other name depending on the first name you made).

Now we will activate the virtual environment before starting the installation using the following command:

	source projectdataenv/bin/activate
You will remark that you are working now with your virtual environment after using this command. So now we can start the installation of the Django using the pip command. Type the following command to do that:

	pip install django psycopg2
The psycopg2 will be also installed since it will enable us to use our configured database.

Using the “projectdata” created directory, we can start our Django project using the following command:

	django-admin.py startproject projectdata .
Configuration of Django database settings:

Now we will configure our project in order to use the created database. We will open the main Django project settings file using the following command:

nano ~/projectdata/projectdata/settings.py
At the end of this file there is a “DATABASES” section which is configured to SQLite as a database.

. . .
	DATABASES = {
	   'default': {
	       'ENGINE': 'django.db.backends.sqlite3',
	       'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
	   }
	}
. . .
We will change this section that the PostgreSQL database will be used instead of SQLite.

We will do as below:

	. . .
	DATABASES = {
	   'default': {
	       'ENGINE': 'django.db.backends.postgresql_psycopg2',
	      'NAME': 'projectdata',
	       'USER': 'projectdatauser',
	       'PASSWORD': 'password',
	      'HOST': 'localhost',
	       'PORT': '',
	   }
	}
	. . .
Then save and close the file.

Test our project:

Now we will test our Django project starting by the migration of our data structures to our database using the following command:

	cd ~/projectdata
	python manage.py makemigrations
	python manage.py migrate
Then type the following command to create an administrative account while you will be asked to choose a username, an e-mail address and a password:

	python manage.py createsuperuser
Now we will start our Django project using the following command:

	python manage.py runserver 0.0.0.0:8000
Then visit your server’s domain name or IP address followed by :8000 to find default Django root page. (You can do this with any web browser).

	http://server_domain_or_IP:8000
Then add the “/admin” to the end of the URL, that you be in front of the login screen. So enter your username and password already created that you will be taken to the admin interface. You can stop the development server using the Ctrl+C on your terminal window.
