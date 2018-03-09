i. Ip Address: 18.196.173.223
ii. SSH Port: 2200
iii. Complete url to Hosted Application: http://18.196.173.223.xip.io

Summary of Software Installed
1. update the package list
    sudo apt-get update
2. Get upgrade of packages
    sudo apt-get upgrade
3. `sudo apt install finger`
4. `sudo ufw default deny incoming`
5. `sudo ufw default allow outgoing`
5. `sudo ufw allow ssh`
5. `sudo ufw allow 2200/tcp`
6. `sudo ufw allow www`
7. `sudo ufw allow 80/tcp`
8. `sudo ufw allow ntp`
9. `sudo ufw allow 123/tcp`
10. `sudo ufw enable`
11. Create user grader
	`sudo adduser grader`
12. Check if grader exists
	`finger grader`
13. Give grader sudo access
	`sudo nano /etc/sudoers.d/grader`
	Add this to file
	`grader ALL=(ALL) NOPASSWD:ALL`

14. Install apache and mod_wsgi for python apps on apache
	`sudo apt-get install apache2`
	`sudo apt-get install libapache2-mod-wsgi`
15. Clone app into server
	`git clone https://github.com/AdeyinkaAdegbenro/Restaurant_Catalogue_App.git`
16. Install python pip and then install dependencies
	`sudo apt install python-pip`

17. create wsgi file and add the following
  	`cd Restaurant_Catalogue_App`
  	`touch myapp.wsgi`
  	Added this
  	`import sys
  	 sys.insert('/var/www/Restaurant_Catalogue_App')
  	 sys.insert('/var/www/Restaurant_Catalogue_App/myapp.wsgi')
  	 from final_project import app as application
  	 application.secret_key = 'you wont guess`
18. Edit the wsgi configuration
	`sudo nano /etc/apache2/sites-enabled/000-default.conf`
	Added this
	`<VirtualHost *:80>
    #ServerName www.example.com
    #ServerAlias example.com
    #ServerAdmin webmaster@example.com
    DocumentRoot /var/www/Restaurant_Catalogue_App
    WSGIScriptAlias /myapp /usr/local/www/wsgi-scripts/myapp.wsgi
    <Directory /var/www/Restaurant_Catalogue_App>
    Order allow,deny
    Allow from all
    </Directory>
	</VirtualHost>`
19. Install postgresql and configure
	`sudo apt-get install postgresql`
    `sudo -i -u postgres`
    `psql`
    create database and user catalog
    `create database restaurantmenu;`
    `create user catalog;`
    `alter user catalog with encrypted password 'catalogpassword';`
20. Disable root login on Ubuntu disable password login
  	`sudo nano /etc/ssh/sshd_config`
  	Edit PermitRootLogin to no
  	`PermitRootLogin no`
    Edit PassWordAuthentication
    `PassWordAuthentication no`
    `sudo service ssh restart`

21. Generate ssh key-pair 
    `ssh-keygen`
22. Install public key on server
    `mkdir .ssh`
    `touch .ssh/authorized_keys`
    `sudo nano .ssh/authorized_keys`
    Paste public key in it
23. Third party resource used during this project include
    https://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html
    https://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/
    https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e
