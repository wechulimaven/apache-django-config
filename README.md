# apache-django-config

 chmod 400 ec2keypair.pem

 ssh -i "ec2keypair.pem" ubuntu@ec2-PUBLIC-IP-ADDRESS.compute-1.amazonaws.com



Django deployment to apache server

--------Changing file permission ownership---------------------
chmod 664 bd.sqlite3
sudo chown :www-data db.sqlite3
sudo chown :www-data project_folder
sudo chown :www-data main_project_folder
//chwon command changes user ownership of a file or directory

--------Changing in apache config file---------------------------
1. cd /etc/apache2/sites-available
2. sudo cp 000-default.conf 000-default.conf_backup

3. sudo vi 000-default.conf

COPY PASTE Changing only the directory paths into 000-default.conf

Alias /static /home/ubuntu/anpr/recognition/static
<Directory /home/ubuntu//anpr/recognition/static>
	Require all granted
</Directory>

<Directory /home/ubuntu/anpr/recognition/recognition>
	<Files wsgi.py>
		Require all granted
	</Files>
</Directory>
WSGIPassAuthorization On
WSGIDaemonProcess recognition python-path=/home/ubuntu/anpr/recognition/ python-home=/home/ubuntu/anpr/env
WSGIProcessGroup recognition
WSGIScriptAlias / /home/ubuntu/anpr/recognition/recognition/wsgi.py

</VirtualHost>

ENABLE APACHE VISIBALE SITE
4. sudo a2ensite 000-default.conf

INSTALL WSGI MOD IN APACHE
5. sudo apt-get install libapache2-mod-wsgi-py3
6. sudo a2enmod wsgi
7. sudo service apache2 restart

TO VIEW APACHE LOGS
8. cd /var/log/apache2/
