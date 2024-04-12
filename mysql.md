- ## Syntax
  mantra

```
mysql> CREATE DATABASE menagerie;
mysql> USE menagerie
```

- ## Tips

if you got the connection error in mysql workbench, try to create a new user and grant him with all privelegys.

mysql> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL PRIVILEGES ON _._ TO 'admin'@'localhost' WITH GRANT OPTION;

if u on windows and error steel exists try to start my sql command line client and write created user password
