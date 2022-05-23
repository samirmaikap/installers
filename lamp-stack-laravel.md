## Install Lamp Stack in a ec2 instance with Laravel

###### Step 1 : Update the instance

```
sudo apt update
```

###### Step 2 : Install apache

```
sudo apt install apache2
sudo ufw app info "Apache Full"
sudo ufw allow "Apache Full"
```

Check enter the server url to check if the site is working

###### Step 3 : Install MySql

```
sudo apt install mysql-server
sudo mysql

CREATE USER 'user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'user'@'localhost';
FLUSH PRIVILEGES;
```

If you need to ALTER the "root" password use the following command

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password>';
```

###### Step 3 : Install Php

```
sudo apt install php libapache2-mod-php php-mysql
sudo nano /etc/apache2/mods-enabled/dir.conf
```

It will look like this

```
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
```

Move the index.php to the first position

```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

Configure root directory

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

Make changes in 1 place

```
DocumentRoot /var/www/html
```

To 

```
DocumentRoot /var/www/html/public
```

Also add these lines after the **DocumentRoot** line

```
<Directory /var/www/html/public>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
</Directory>
```

Enable mod rewrite

```
sudo a2enmod rewrite
```

###### Step 4 : External Commands

Run these commands to install extra packages

```
sudo apt install curl
sudo apt intsall composer
sudo apt install git
sudo apt install php-fpm
sudo apt install php-cli
sudo apt install php-curl
sudo apt install php-xml
sudo apt install php-mbstring
```

###### Finally

Run this command to restart the apache

```
sudo systemctl restart apache2
```

Git pull your codes into the root directory which is **/var/www/html** run necessary Laravel command.
Check your site afterwards.
