# Install-WordPress-on-Amazon-EC2-Ubuntu-20.04-Instance-or-Virtual-Machine
Install WordPress on Amazon EC2 Ubuntu 20.04 Instance or Virtual Machine

(1). Update Ubuntu System Repositories : Type the following command on the terminal and press enter key
     sudo apt update
	 
(2). To install the Apache web server type the following commands and press enter key

     sudo apt install apache2
     or
     sudo apt install apache2 -y

#Set UFW firewall to allows web traffic ( HTTP and HTTPS traffic)
(1). Check the list of the applications profiles that need access
    
    sudo ufw app list
	 
(2). We will use Apache Full profile for enabling different network activities
     
     sudo ufw allow 'Apache Full'
	 
(3). Check the status of traffic on port 80 and 443
     sudo ufw app info "Apache Full"
	
(4). Check apache2 service status
     
     sudo systemctl status apache2
	 
(5). Enter the public IP address in browser

#Install MySQL Server
(1). Type the following command and press enter key to install the MySQL server
     
     sudo apt-get install mysql-server
    or
     sudo apt-get install mysql-server -y
	
(2) To secure the MySQL server in Apache2 enter the following command and hit enter
     
     sudo mysql_secure_installation
	
#Create MySQL Dedicated Database and User:
(1). Type the following command and hit enter key in terminal to use SQL prompt
     
     sudo mysql -u root -p

(2). Create Database User
    Option 1 – Access to Localhost : We will use this option for this tutorial. Type the following command and hit enter key
         
	 CREATE USER 'user1'@'localhost' IDENTIFIED BY 'EnterPassword';
	 
    Option 2 – Grant access for any host : Type the following command and hit enter key
    
          CREATE USER 'user1'@'%' IDENTIFIED BY 'EnterPassword';
	  
    Option 3 – Access to any host and encrypted password : Type the following command and hit enter key
    
          CREATE USER 'user1'@'%' IDENTIFIED WITH caching_sha2_password BY 'Enter Password';

(3). Grant Permissions to the User
     Type the following command and press enter
     
        mysql> GRANT ALL PRIVILEGES ON *.* TO 'user1'@'localhost';
	
    To reload all privileges press enter
    
        mysql> FLUSH PRIVILEGES;
	
    To go to main terminal enter exit and press enter
    
        mysql>exit;
		
(4). Create MySQL Database
    Enter the following command and press to create new database. Refer the following image
    
	  sudo mysql -u root -p
	  CREATE DATABASE wordpressdb;
	  SHOW DATABASES;
	  exit;
	  
    To check the status of MyQL services enter the following commands and press enter
    
      systemctl status mysql.service
	  
	  
#Install PHP with some extensions
  Type the following command and press enter
  
    sudo apt install php php-mysql php-gd php-cli php-common
    sudo apt install php-

#Configure dir.conf file.

    sudo vi /etc/apache2/mods-enabled/dir.conf
	<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.php index.xhtml index.htm
    </IfModule>
	:wq!
	
#Restart Apache Web Server
   
    sudo service apache2 restart
   
#Install PhpMyAdmin on Amazon ec2 Ubuntu Instance
 1). Open your ssh terminal and type the following command and press enter key
 
     sudo apt install phpmyadmin
	 
(2). Press space bar to select Apache2 and press enter key

(3). Press tab once and hit enter

#Installing WordPress
(1). Type the following commands to install wget pakage and press enter key

    wget: This is a non-interactive command line tool and a software package for retrieving files using HTTP, HTTPS, FTP and FTPS protocols

    sudo apt install wget unzip -y

(2). Type the following command and press enter to download the WordPress

    sudo wget https://wordpress.org/latest.zip
	
(3). Type the following command to unzip the downloaded latest version of WordPress

      sudo unzip latest.zip
      

(4). Type the following command to copy all unzipped file to the html directory

      sudo cp -r wordpress/* /var/www/html/
	  
      cd /var/www/html
	  
	  ls
	  
(5). Make sure that the directory you are writing to allows for www-data to write to it. Enter the following command and press enter key

     sudo chown www-data:www-data -R /var/www/html/
     
 Info: sudo chown $USER:www-data /var/www/mysite

(6). Delete index.html in /var/www/html type the following command and press enter key
// to go to the path " /var/www/html " type  cd /var/www/html

    sudo rm -rf index.html
