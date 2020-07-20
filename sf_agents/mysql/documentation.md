##### Plugin: MySQL 

##### Description: 

​        The MySQL plugin connects to MySQL server. It collects the databases statistics including server details, database details, and table details.

##### Configuration:

1. Check whether the server has been start on port 3306 by command:
   **service mysql status**
   If the server is not started, use the following command to start:
   **service mysql start** 

2. The plugin requires user to enable the performance schema. To check whether the performance schema is available, please use the below statement in shell:

   **Mysql --verbose --help**
   If output contains “--performance_schema” or related field, then it means performance schema is available on mysql server.

   If not, please use the following statement:
   **cmake . –DWITH_PERFSCHEMA_STORAGE_ENGINE=1**

   The performance schema is enabled in mysql by default. To check whether the performance schema is enabled, please use the following statement within mysql:

   **SHOW VARIABLES LIKE ‘performance_schema’;**

   If the value for variable ‘performance_schema’ is on, then it is enabled. 
   If not, please use the following statement in shell:
   **sudo mysqld --performance-schema-instrument='%=on'**
   See dev.mysql.com/doc/refman/5.6/en/performance-schema-quick-start.html for reference

   **Note:** Only mysql with version 5.5 and above support the performance schema

3. If the user want to get related data for specific database/table, the user needs to have privileges on that database/table. Use the following command in mysql to grant permission:
   **GRANT type_of_permisson ON database_name.table_name TO ‘username’@’localhost’;**
   See dev.mysql.com/doc/refman/5.6/en/grant.html for reference

##### Plugin Configuration:

​        Below is the plugin configuration, which is included in config.yaml under metric plugin section

```
 -   name: mysql

     enabled: true

     interval: 10

     config:

         port: “3306”

         host: “127.0.0.1”

         user: mysql

         password: mysql
```

 

**Note:** 

The host and port must be accessible and the user needs to have permission to read the information schema and performance schema