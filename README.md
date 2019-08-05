<h1> Linux Server Practice </h1>

This is a practice to launch a web app on a Linux server on a Cloud. 
(the final project for Udacity Full Stack Web Developer Nanodegree) 



<h2>Used software/services </h2>
<p> - Flask for backend web application
<p> - PostgreSQL for the database 
<p> - sqlalchemy to access to the database
<p> - Google OAuth for thrid party authentification
<p> - Apache2 for webserver
<p> - Amazon AWS (Lightsail) for hosting


<h2>SSH login</h2> 
<p> - IP address and SSH port for the server:  54.93.241.240,  SSH port 2200     
<p> - To access, it is required to have the secret key, that are provided by me. Save the key in a file in your local computer (ex. ~/.ssh/secret.pem) 
<p> - To login, use your terminal to write following command =>  "ssh -i SECRETKEY_FILE_PATH grader@54.93.241.240 -p 2200"  (example of SECRETKEY_FILE_PATH is "~/.ssh/secret.pem) 
<p> - Sometimes the server is stopped to save the cost. In that case, please contact to me


<h2>Web acccess</h2>
<p> - URL of the web application:  <a href="http://54.93.241.240.xip.io">54.93.241.240.xip.io</a>   (using xip.io becaues Google AOuth does not allow number-only url) 
<p> - By accessing that address from your browser, you can see the website


<h2>Set up steps</h2>
<p> setting up was done roughly in following steps
<h3> Server launch </h3>
<p> - set up and launch Lightsail server on AWS webiste, also download a default secret key 
<p> - save the default secret key in local machine, in a folder like ~/.ssh/secretkey.pem
<p> - change the permission of the file  "chmod 700 ~/.ssh/secretkey.pem 
<p> - connect via ssh from terminal, with a command: "ssh -i ~/.ssh/secretkey.pem ubuntu@54.93.241.240 -p 20" (20 is the default SSH port) 
  
<h3> Adding a user </h3>
<p> - add another user, "grader", with following command: "sudo adduser grader" 
<p> - create a file "/etc/sudoers.d/grader" on SSH, and write "grader ALL=(ALL:ALL) ALL" 
<p> - create a key for the user by running following on local machine: "ssh-keygen -f ~/.ssh/grader.rsa", make its permission to 700
<p> - copy public key on SSH's /home/grader/.ssh/
  
<h3> Configureing firewall and profibiting root access </h3> 
<p> - sudo uwf allow 2200/tcp
<p> - sudo uwf allow 123/udp
<p> - sudo uwf deny 20/tcp
<p> - sudo uwf enable 
<p> - edit /etc/ssh/sshd_config,   change "PermitRootLogin" to "no" 

<h3> Package installing </h3> 
<p> - updating apt-get installer: "sudo apt-get update" and "sudo apt-get upgrade" on SSH
<p> - sudo apt-get install apache2   
<p> - sudo apt-get install libapache2-mod-wsgi python-dev
<p> - sudo apt-get install libpq-dev python-dev
<p> - sudo apt-get install postgresql postgresql-contrib
<p> - sudo apt-get install python3-pip 
<p> - sudo pip3 install virtualenv 
<p> - "sudo virtualenv venv", at "/var/www/html/"  and then "source venv/bin/activate" to create virtual environment 
<p> - installing Python packages with "pip3 install". The pakcages include: Flask, sqlalchemy, Google
  
<h3> App settings </h3> 
<p> - copy the all files and folders of the app on Lightsail, under /var/www/html/venv/
<p> - change the main python file's name to be "__init__.py"  
<p> - change wsgi file at /etc/apache2/sites-available/000-default.conf, to add following lines
<p> DocumentRoot /var/www/html/venv/fullstackcatalog/        
<p> WSGIScriptAlias / /var/www/html/venv/fullstackcatalog/project.wsgi   -> this redirects server's root to the web app
<p> - create "project.wsgi" under the app foler (/var/www/html/venv/fullstackcatalog/), and the contents are as following:

#!/usr/bin/python
import sys
import logging

logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/html/venv/")
sys.path.append("/var/wwww/html/venv/lib/python3.5/site-packages")
sys.path.append("/fullstackcatalog")

from fullstackcatalog import app as application
application.secret_key = (SECRET) 

<h3> Database settings </h3> 
<p> login PostgreSQL by run "sudo postgres", and then "psql"
<p> create data base by "CREATE USER ubuntu WITH PASSWORD (pass)" and "CREATE DATABASE catalog WITH OWNER ubuntu" 
<p> change the database setting in __init__.py and database_setup.py as  "engine = create_engine('postgresql://ubuntu:(pass)@catalog')"
<p> run "python3 set_database.py" to create tables 

<h3> Restart Apache server </h3>
<p> restart apache server by "sudo service apache2 restart", and access to 54.93.241.240.xip.io

<h2>References</h2>
<p> - this site helped a lot during the setting https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps  







  
