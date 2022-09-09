## liquibase

### requisitos

- liquibase https://www.liquibase.org/download
- clonar este repositorio

## generando el changelog

 copia el archivo llamado liquibase.properties a la ruta donde trabajas con la base de datos

abre el archivo y cambia la linea que tienes por esta  
```
# Enter the path for your changelog file.
changeLogFile=changelog.sql

```
en las siguientes lines coloca tu informacion
```
#### Enter the Target database 'url' information  ####
liquibase.command.url=jdbc:postgresql://localhost:5432/prueba

# Enter the username for your Target database.
liquibase.command.username: postgres

# Enter the password for your Target database.
liquibase.command.password: secret

```

ahora abre la terminal y coloca 

 ```
 liquidbase generateChangelog
 ```
### configurando el entorno 

ahora tienes el changelog con el estado actual de la base de datos. copialo y pegalo en el directorio de el repositorio llamado changelogs; tambien pudes crear la carpeta en tu directorio y pegar ahi el archivo generado

cada que vallas a agregar un nuevo cambio deberas guardarlo en esar carpeta  

si lo haces en una carpeta en tu directorio copia el archivo llamado changelog.xml de el repositorio y pegalo afuera de la carpeta changelogs como esta en el repositorio y abrelo

ahora si no, solo dejalo ahi y abrelo

ya abierto veras unas lineas de ejemplo donde llamo a los archivos del repositorio que estan dentro de la carpeta changelogs

borralas ya que solo son un ejemplo de como tienes que ir agregando cada cambio a futuro
ya borradas ahora agregaremos el changelog que generaste (esto no afectara en nada a la base de datos ya que detecta que ya tiene los cambios y solo lo ignorara)

pon esto donde estaban las lines que copiaste 
```
<include file"changelogs/nombre del changelog"/>
```

ahora abre la terminal en ese directorio y corre

(CUIDADO!!! esto subira los cambios directo a la base de datos asi que no lo hagas sin revisar antes todo ya que a este punto aun no has configurado los rollbacks)

```
- liquidbase status 

- liquidbase update 

- liquidbase tag <coloca un nombre al tag es para el rollback>
```

despues de esto ve a revisar las base de datos apareceran dos tablas, si ya estan creadas no importa 
se llamaran:

databasechangelog
databasechangeloglock

estas bases de datos son para llevar el control, si alguien manda un cambio lo veras reflejado ahi 

### notas

siempre procura agregar los rollbacks en los changelos el primero que generes no los tendra pero a los nuevos agregale todo lo que tienen los ejemplos 

despues de hacer un update has un liquidbase tag <nomrbe del tag> para que asi puedas volver con ese tag a la version anterior 

(seria mejor tener repositorio privado donde puedan tener todo junto para que los changelogs que se vallan subiendo los puedan tener todos en sus maquinas. dime que piensas de la idea para proponerla e implementarla si eso pasara, entonces mejor ya hago yo todo esto y solo les paso el link de ese repositorio privado para que suban sus changelogs y ver si todo va bien antes de que lo manden al servidor. cualquier cosa estoy en slack)

### commands

liquidbase status       [show the status]

liquidbase generateChangelog    [generate a changelog of the database alredy created]

liquidbase update   [make the changes to the database]

liquidbase tag "name of the version"        [give a tag for make rollbacks]

liquidbase rollback name of the tag     [rollback to the tag]

mas comandos https://docs.liquibase.com/commands/home.html
