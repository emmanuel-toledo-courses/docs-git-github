# Un poco más allá de los fundamentos de Git

Todos los recursos y proyectos estan dentro de ```assets -> 02```.

## TIL

Recordemos que los ```commit``` son un recuerdo del tiempo de vida del repositorio al cual podemos dirigirnos si lo requerimos.

Al ejecutar ```git log``` o ```git reflog``` y vemos ```(HEAD -> {rama})``` (por ejemplo: ```(HEAD -> main)```), esto indica en que rama nos encontramos en ese punto del tiempo.

El archivo ```.gitignore``` nos permite definir que archivos o directorios no queremos que git este dando seguimiento.

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git diff``` | Permite ver las modificaciones de los archivos del repositorio que no estan dentro del stage |
| ```git diff --staged``` | Permite ver las modificaciones de los archivos del repositorio que si se encuentran en el stage |
| ```git reset --soft HEAD^```, ```git reset --soft HEAD^2``` | Permite remover un commit y pasarlos a stage sin eliminar los cambios. HEAD es un puntero al último commit de la rama en que te encuentras, el número despues del ^ es el número de commits del último al primero que queremos seleccionar para dicho reset, si no colocamos nada indicamos que es el último (como un arreglo) |
| ```git config core.autocrlf true``` | Configurar salto de lineas con Git para evitar mensajes molestos (LF will be replaced by CRLF the next time Git touches it) |
| ```git reset --mixed {hash del commit}```, ```git reset --mixed df794ea```, ```git reset --mixed HEAD^``` | Es similar al --soft pero con la diferencia de que no deja los cambios en stage, sino que los quita de ahí. |
| ```git reset --hard df794ea``` | Destruimos y mantendremos todo el repositorio a como se encontraba en dicho commit |
| ```git reflog``` | Historia completa de la interacción del repositorio sin omitir nada, secuencia de movimientos en todo el repo |
| ```git mv {path origen} {path final}```, ```git mv destruir-mundo.md salvar-mundo.md``` | Movemos un archivo de un path a otro, puede usarse también para renombrar un archivo |
| `````` | |

# Practica No. 1

Vamos a crear una carpeta llamada ```03-instalaciones```.

```
git init

# Creamos archivo instalaciones.md y agregamos un texto

git add .
git commit -m "README file added"
git log

# Modificamos archivo instalaciones.md y vemos los cambio del mismo

git diff
git add .

# Ya no veremos las diferencias, el comando por si solo hará que veamos unicamente cambios que no se han agregado a un stage.
git diff

# Consultamos diferencias entre archivos que estan en el último commit y el stage
git diff --staged

# Usualmente se aprovecha el uso de VS Code para ver los cambios de forma más grafica

git commit -m "Updated instalations"

# Ya no deberemos ver diferencias
git diff
git diff --staged

# Modificamos el archivo README
git commit -am "Instalaciones actualiz"

git lg

# Actualizamos el mensaje del commit anterior
git commit --amend -m "Instalaciones actualizadas"
git lg
git commit --amend -m "Notas añadidas a las instalaciones"
git lg

# Modificamos el archivo README, ahora queremos que el commit anterior contenga el cambio que acabamos de hacer.
git reset --soft HEAD^
git status
git add .
git commit -m "Notas agregadas de nuevo a las instalaciones"
```

# Practica No. 4

Vamos a crear una carpeta llamada ```04-material-heroes```, su contenido será el de ```assets -> 02 -> Materia-Heroes.zip```.

```
git init
git status
git add README.md
git commit -m "README agregado"
git log
git add misiones.md
git commit -m "Agregamos misiones.md"
git log
git add heroes.md
git commit -m "Agregamos heroes.md"
git log
git add ciudades.md
git commit -m "Agregamos ciudades.md"
git log
git add .\historia\
git commit -m "Agregamos la carpeta historia"
git log

# Presionamos 'a' para modificar
# Presionamos 'esc', ':wq' para salir y guardar
git commit --amend
git log

# Modificamos heroes.md
git commit -am "Heroes.md: Agregamos a Linterna Verde"

# Modificamos heroes.md (has anterior al último commit)
git reset --soft f4425a5
git commit -am "Hearoes.md: Robin y Linterna Verde"

# Usamos el hash generado del commit "Agregamos ciudades.md"
git reset --mixed df794ea
# Ya no veremos los commits posteriores al de ciudades.md
git log

# Destruimos y mantendremos todo el repositorio a como se encontraba en dicho commit, veremos que no tenemos en heroes.md los herores que agregamos.
git reset --hard df794ea

# Tomamos hash de heroes
git reset --hard  37c5586

# Borramos carpeta historia

# Hacemos reset del commit anterior al de heroes, que sería misiones
git reset --hard HEAD^

# A pesar de que modifcamos nuestro repo podemos restaurar el historico de todo lo que ah ocurrido en orden historico
git reflog

# Usamos el hash del commit Heroes.md: Agregamos a Linterna Verde
git reset --hard 4a236a8

# Vemos que nuestro repo se restablece a como estaba a este commit
git reflog

# Usualmente esto no llega a suceder, pero es bueno saberlo para un escenario extraño que se pueda presentar.

# Creamos un archivo llamado destruir-mundo.md
git add destruir-mundo.md
git commit -m "Destruir mundo añadido"

# Renombramos un archivo usando comando de mover. Lo agrega al stage directamente
git mv destruir-mundo.md salvar-mundo.md
git status
git commit -m "Destruir mundo renombrado"
git log

# Podemos eliminar un archivo desde git pero lo deja en el stage
git rm salvar-mundo.md
git status

# Si hacemos un reset --hard veremos el archivo aún existente
git reset --hard | git checkout -- .

# Indicamos a git que dicho archivo debe quedarse eliminado
git rm salvar-mundo.md
git status
git commit -m "salvar-mundo: eliminado"

# Cambiamos nombre de superman.historia.md a superman.md por medio de Visual Studio
git status

# Para git es como si hubieramos eliminado superman.historia.md aunque solo lo renombramos
git add .

# Ahora veremos que git identificó el renombramiento del archivo
git status

git commit -m "Historia de superman renombrada"

# Nos movemos a salvar-mundo: elimnado
git reset --hard 6c5d1df

# Veremos que git comprende el renombramiento del archivo superman y no duplica el cambio anterior
git reflog

# Nos movemos al commit Historia de superman renombrada por medio de su hash
git reset --hard df0fed6

# Vamos a eliminar archivo batman.historia.md por medio de Visual Studio
git add .
git commit -m "Historia de batman eliminada"
```

Creamos carpeta ```node_modules``` y archivo ```server.log```. Agregamos archivo ```.gitignore``` en la raiz del proyecto.

```
# directorios que no queremos que tenga seguimiento (incluyendo contenido)
dist/
node_modules/

# archivo server.log
server.log

# todos los archivo con extensión .log
*.log
```

Volvemos a la consola de git.

```
git add .
git commit -m ".gittgnore agregado"
```

# Tarea

Realizar práctica de ```assets -> 02 -> Tarea.zip```, comandos de la actividad.

Seguimos los pasos del archivo index.html.

```
git init
git add README.md
git commit -m "Creación de README"

git add logs/hoy.log
git commit -m "Creamos el archivo hoy.log"

git add .gitignore
git commit -m "Agregado .gitignore"

# Borramos todo y solo dejamos README.md
git reflog
gir reset --hard | git checkout -- .
```