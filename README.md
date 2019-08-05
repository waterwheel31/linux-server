<h1> Linux Server Practice </h1>

This is a practice to launch a web app on a Linux server on a Cloud. 




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
<p> setting up was done in following steps
<p> - set up and launch Lightsail server on AWS webiste, also download a default secret key 
<p> - save the default secret key in local machine, in a folder like ~/.ssh/secretkey.pem
<p> - connect via ssh from terminal, with a command "ssh -i ~/.ssh/secretkey.pem ubuntu@54.93.241.240 -p 20" (20 is the default SSH port) 
<p> - 
<p> - update pakcage by running "sudo apt-get update" and "sudo apt-get upgrade", and "

<h2>References</h2>
<p> - XX
<p> - XX






  
