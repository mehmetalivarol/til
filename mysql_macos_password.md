## Change root password on local Mac install of MySQL

1. Stop the mysqld server. ` 'System Prefrences' > MySQL > 'Stop MySQL Server'`
2. Start in safe mode: `sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables`
3. If no password exists: `update user set authentication_string=password('newpassword') where user='root'`;
3. If password exists: `UPDATE mysql.user SET Password=PASSWORD('vicki') WHERE User='root'`;

Password is in `mysql.user` schema. 
