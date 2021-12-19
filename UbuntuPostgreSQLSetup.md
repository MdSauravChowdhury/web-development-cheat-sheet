<h1>Test</h1>

Step 1 — Installing PostgreSQL
	<ul>sudo apt update</ul>
	<ul>sudo apt install postgresql postgresql-contrib</ul>

Step 2 — Using PostgreSQL Roles and Databases
     Switching Over to the postgres Account
	 <ul>sudo -i -u postgres</ul>
	psql

     Exit out of the PostgreSQL prompt by typing:
	\q


Step 3 — Creating a New Role
	<ul>createuser --interactive</ul>
	sudo -u postgres createuser --interactive

Step 4 — Creating a New Database
	<ul>createdb dbName</ul>
	<ul>sudo -u postgres createdb sammy</ul>

Step 5 — Opening a Postgres Prompt with the New Role
	<ul>sudo adduser DBUser</ul>
	<ul>sudo -i -u DBUser</ul>
	<ul>or sudo -u sammy psql</ul>
	<ul>psql</ul>
	<ul>psql -d postgres</ul>

Step 6 — Creating and Deleting Tables
	<ul>Config Django Models Setting
	or Create Menule</ul>

	CREATE TABLE table_name (
	    column_name1 col_type (field_length) column_constraints,
	    column_name2 col_type (field_length),
	    column_name3 col_type (field_length)
	);

=======================Optional==================================

Step 7 — Adding, Querying, and Deleting Data in a Table
	<ul>INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2017-04-28');</ul>
	<ul>INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2018-08-16');</ul>

Step 8 — Adding and Deleting Columns from a Table
	<ul>ALTER TABLE playground ADD last_maint date;</ul>

Step 9 — Updating Data in a Table
	<ul>SELECT * FROM playground;</ul>
	<ul>UPDATE playground SET color = 'red' WHERE type = 'swing';</ul>



