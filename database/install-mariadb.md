# MariaDB 数据库安装 / 设置

## Windows

> MariaDB (mariadb-10.2.10-winx64.zip)

1. Unzip zip file to your_mariadb_directory/

2. Edit configuration file
	
    > your_mariadb_directory/my.ini (rename my-large.ini to my.ini )

  ```
  [client]
  # ------- add -----------
  default-character-set = utf8
  # ------------------

  [mysqld]
  port		= 3306
  socket		= /tmp/mysql.sock
  # ------- add -----------
  basedir = D:\dev\mariadb-10.2.10-winx64
  datadir = D:\dev\mariadb-10.2.10-winx64\data
  character-set-server = utf8
  # ------------------

  # ------- add -----------
  [WinMySQLAdmin]
  Server = D:\dev\mariadb-10.2.10-winx64\bin\mysqld.exe
  # ------------------
  ```

3. Install
	
    > cmd `your_mariadb_directory/bin`

  ```dos
  C:\>d:
  D:\>cd your_mariadb_directory/bin
  ```
  
  ```dos
  mysqld --install your_mariadb_service_name --defaults-file=your_mariadb_directory\my.ini

  (if your_mariadb_directory include spaces,use double quotation marks)
  
  
  uninstall:
  mysqld --remove your_mariadb_service_name
  ```

4. Start / stop MariaDB

  ```
  run > services.msc

  or:

  cmd
  net start your_mariadb_service_name
  net stop your_mariadb_service_name
  ```

5. Update MariaDB password

  > cmd `your_mariadb_directory/bin`
    
  ```dos
  mysql -u root -p
  ```
  ```sql
  update mysql.user set password = PASSWORD('your_new_password') where user='root';
  flush privileges;
  ```
	
6. Check configuration
  
  ```sql    
  MariaDB> show variables like 'char%';
  MariaDB> show variables like 'coll%';
  MariaDB> show engines\G
  ```
