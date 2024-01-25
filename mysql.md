if you got the connection error in mysql workbench, try to create a new user and grant him with all privelegys. 

mysql> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;