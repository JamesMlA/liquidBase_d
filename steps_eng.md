### liquibase

#### requeriments

- liquibase https://www.liquibase.org/download
- clone this repository

## generating changelog

 copy the file named liquibase.properties to you data base path and opened

 open the file and change the line you have for this one  
```
# Enter the path for your changelog file.
changeLogFile=changelog.sql
```
in the following lines enter your information
```
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
### Setting up the environment 

now you have the changelog with the current state of the database. copy and paste it in the repository directory called changelogs; you can also create a folder in your directory and paste the generated file there.

every time you are going to add a new change you should save it in this folder.  

if you do it in a folder in your directory copy the file called changelog.xml from the repository and paste it outside the changelogs folder as it is in the repository and open it.

now if not, just leave it there and open it.

once opened you will see some example lines where I call the repository files that are inside the changelogs folder.

delete them as they are just an example of how you have to add each change in the future.
already deleted now we will add the changelog that you generated (this will not affect in anything to the database since it detects that it already has the changes and it will only ignore it)

put this where the lines you copied were 

```
<include file"changelogs/<changelog name>"/>
```
now open the terminal in that directory and run

(CAUTION!!! this will upload the changes directly to the database so don't do it without checking everything first as at this point you haven't configured the rollbacks yet)

```
- liquidbase status 

- liquidbase update 

- liquidbase tag <name of the tag>
```

after this go to check the database two tables will appear, if they are already created it does not matter 
they will be called:

databasechangelog
databasechangeloglock

these databases are to keep track, if someone sends a change you will see it reflected there.

### notes

always try to add the rollbacks in the changelogs the first one you generate will not have them but to the new ones add everything that the examples have. 

after doing an update make a liquidbase tag <tag name> so you can go back to the previous version with that tag. 

(it would be better to have a private repository where they can have everything together so that the changelogs that are uploaded can have them all on their machines. tell me what you think of the idea to propose and implement it if that happens, then better I do all this and just pass the link to that private repository to upload their changelogs and see if everything goes well before they send it to the server. anything else I'm in slack)

#### commands

liquidbase status       [show the status]

liquidbase generateChangelog    [generate a changelog of the database alredy created]

liquidbase update   [make the changes to the database]

liquidbase tag "name of the version"        [give a tag for make rollbacks]

liquidbase rollback name of the tag     [rollback to the tag]

more commands https://docs.liquibase.com/commands/home.html
