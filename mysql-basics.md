# MySQL basics

## Common commands


Connect to the mysql server/daemon:
`mysql -uuser [-ppassword]`

(it's widely considered safer to omit the password part in the command and type the password afterwards - it prevents the shell history from keeping a trace of the pw:

`mysql -uuser
password:
mysql-shell>`)


- list all databases available to this user:
`show databases;`

- connect to a specific database:
`use <database_name>;`

- list all tables in the database:
`show tables;`

- show a specific table schema:
`desc <table_name>;`

- show a table's lines:
`select * from table_1;`

- leave (properly):
`quit;`
