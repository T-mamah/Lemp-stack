# MERN Stack on Ubuntu 20.04 

The MERN stack is an acronym for MongoDB, Express, React / Redux, and Node.js. The MERN stack is one of the most popular JavaScript stacks for building modern single-page web applications (SPA).

### Prerequisites
1. An Ubuntu VM (In this tutorial we're using an Ubuntu 22.04 on AWS EC2 instance.

This tutorial is broadly divided into 6 categories


1. Installing the Nginx web server
2. Installing MYSQL
3. Installing PHP
4. Confiquring Nginx to use PHP processor
5. Testing PHP with Nginx
6. Retrieving data from MYSQL database with PHP
   
   
   ## Installing the Nginx web Server

   To display web pages, we are going to implore Nginx, a high-performance web server

Update ubuntu

`$sudo apt update`

Upgrade ubuntu

`$sudo apt upgrade`

Install Nginx

`$sudo apt install -y nginx`

To verify that Nginx has been installed and is running as a service in Ubuntu run:

`$sudo systemctl status nginx`



If it is green and running, you have launched a web server in the clouds! Yay! :purple_heart:


To allow traffic from port 80, which is the default port for most web applications
>We need to edit inbound firewall rule and allow traffic on TCP port 80 on our EC2 instance. TCP port 22 is open by default.


Our server is running and we can access it from any IP Address 
and locally.

1. First, lets try to access it locally from our ubuntu shell by running:

`$curl http://localhost:80`

```html
{
Output:
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```

2. Secondly, lets test how our server responds to the request from the internet. run:


`http://<Public-Ip-Address>:80`


If you see the page above, then our webserver was successful installed and accessible through our firewall. Double Yay!!



## Installing MYSQL

Now that our web server is up and running, we need to install a *database management system <b>DBMS<b>*--MYSQL in this case.

`$sudo apt install -y mysql-server`

Login to the MYSQL console:

`$ sudo mysql`


```
Output:

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.31-0ubuntu0.22.04.1 (Ubuntu)

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>

```

It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script, you will set a password for the root user, using mysql_native_password as default authentication method.run:

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password>'`
   

Exit mysql shell with:

`exit`


Start the interactive script by running:

`$ sudo mysql_secure_installation`
   

This will ask if you want to configure the **Validate password plugin**
>Enabling this feature is something of a judgment call. 
Answer Y for yes, or anything else to continue without enabling.

Let's check if we are able to login to the MYSQL console:
   

`$ sudo mysql -p`


To exit
   

`exit`
   

>Notice that you need to provide a password to connect as the root user.
For increased security, it’s best to have dedicated user accounts with less expansive privileges set up for every database, especially if you plan on having multiple databases hosted on your server.


Our MySQL server is now installed and secured. Next, we will install PHP, the final component in the LEMP stack...Awesome
   


##  Installing PHP


We have Nginx installed to serve our content and MySQL to store and manage  our data. We need to install PHP to process code and generate dynamic content for our web server.

>While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration

We need to install **php-fpm**, which stands for *“PHP fastCGI process manager”*, and tell Nginx to pass PHP requests to this software. Additionally, we need **php-mysql**, a PHP module that allows PHP to communicate with MySQL-based databases. 

*Core PHP packages will automatically be installed as dependencies*

run:

`$sudo apt install php-fpm php-mysql`

PHP components have now been installed! Let's move to step 4


## Confiquring Nginx to use PHP processor








