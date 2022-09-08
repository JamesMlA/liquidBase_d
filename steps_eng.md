### liquibase

#### requeriments

- liquibase https://www.liquibase.org/download
- clone this repository

## generating changelog

 copy the file named liquibase.properties to you data base path and opened

 change this parameters
```
# Enter the path for your changelog file.
changeLogFile=changelog.sql

#### Enter the Target database 'url' information  ####
liquibase.command.url=jdbc:postgresql://localhost:5432/prueba

# Enter the username for your Target database.
liquibase.command.username: postgres

# Enter the password for your Target database.
liquibase.command.password: secret

```

 open the terminal and run

 ```
 liquidbase generateChangelog
 ```

now you have the changes.sql copy and paste in the repository folder called changelogs

in this folder yo gona put all the changes that you make 

now open changelog.xml

here you gona se that im using the archives called example delete and crete put this 

```
<include file"changelogs/nombre del changelog"/>
```

now open a terminar and put

(WARNING this gona upload the changes to the database)

```
- liquidbase status 

- liquidbase update 

- liquidbase tag <coloca un nombre al tag es para el rollback>
```

despues de esto ve a revisar las base de datos apareceran dos tablas, si ya estan creadas no importa 
se llamaran:

databasechangelog
databasechangeloglock

estas bases de datos son para llevar el control por si alguien manda un cambio lo veras reflejado ahi 

### notas

cuando siempre procura agregar los rollbacks en los changelos el primero que generes no los tendra pero a los nuevos agregale todo lo que tienen los ejemplos 

despues de hacer un update has un liquidbase tag <nomrbe del tag> para que asi puedas volver con ese tag a la version anterior 

(pense en hacer un repositorio privado desde ya donde podamos tenes todo junto para que los changelogs que se vallan subiendo los puedan tener todos en sus maquinas)
(dime que piensas de la idea cualquier cosa estoy en slack)

#### commands

liquidbase status       [show the status]

liquidbase generateChangelog    [generate a changelog of the database alredy created]

liquidbase update   [make the changes to the database]

liquidbase tag "name of the version"        [give a tag for make rollbacks]

liquidbase rollback name of the tag     [rollback to the tag]

more command !(here)[https://docs.liquibase.com/commands/home.html]
