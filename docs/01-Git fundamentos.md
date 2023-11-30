# Git - Fundamentos

Todos los recursos y proyectos estan dentro de ```assets -> 01```.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| Git alias | https://gist.github.com/Klerith/0acf18bbece7923bcac55edb71b03c2b |

## TIL

Al trabajar en un repositorio de ```git``` es como tener una máquina del tiempo, en la cual podremos movernos hacia adelante y atras de los cambios realizados en dicho repositorio.

El termino proyecto en ```git``` no existe, más bien es un repositorio.
- Repositorio central: Proyecto que vive en un servidor externo y todo el equipo se conecta a el.
- Repositorio distribuido: Cada miembro del equipo tiene una copia del repositorio central.

¿Cómo funciona Git? Una línea del tiempo en la cual podemos movernos hacia adelante o atras con base a los ```commit``` realizados en un repositorio.

Cualquier comando que ejecutemos, si no nos muestra un mensaje, seguramente significa que se ejecuto el comando correctamente.

Se recomienda hacer la menor cantidad de modificaciones en la rama ```main```, usualmente solo tiene los cambios que se van a publicar cuando finaliza el proyecto.

El archivo ```README.md``` (md = markdown) nos permite colocar cierta información del repositorio en forma visual para el usuario final.

Todo lo que se trabaja en ```Git``` se recomienda trabajarlo en ingles ya que es un estandar pero sin problmea puede ser otro idioma.

```Git``` no da seguimiento a las carpetas que se encuentren sin archivos dentro de él. Se puede crear un archivo llamado ```.gitkeep``` dentro del folder para indicar a ```Git``` que a pesar de que no tenga archivos, queremos que ```Git``` lo administre.

## Glosario de palabras

| Palabra | Descripción |
| ------------- | ------------- |
| Commit | Screenshot (fotografía) de los cambios realizados en un repositorio de un proyecto |
| Branch / Rama | Lugar en el cual estamos trabajando, se pueden tener multiples ramas (copia del proyecto general). Todas las ramas dependen de una menos la main o master. |

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git --version``` | Obtener versión instalada de Git |
| ```git help``` | Listar las ayudas que da Git |
| ```git help {comando}```, ```git help commit``` | Abre el navegador con la información de ayuda del comando deseado |
| ```git config --global user.name "Emmanuel Toledo"``` | Configurar nuestro nombre en Git (hacer que nos reconozca) |
| ```git config --global user.email "emmanueltoledo1082@gmail.com"``` | Configurar nuestro correo electrónico en Git (hacer que nos reconozca), sirve para indicar quien realizó ciertos cambios en un repositorio, normalmente este correo electrónico es el configurado en GitHub, DevOps, etc. |
| ```git config --global -e``` | Vemos la configuración global realizada, podemos modificarlo directamente |
| ```git init``` | Comando que inicializa un repositorio, crea carpeta oculta llamada .git |
| ```git config --global init.defaultBranch {nombre}```, ```git config --global init.defaultBranch main``` | Hacemos que al iniciar un repositorio se cree automaticamente la rama main como la principal (anteriormente era master pero se ah ido cambiando por su significado) |
| ```git status``` | Da información sobre los commits y las ramas en donde nos encontramos además de que los archivos de color rojo son aquellos a los que Git no les da seguimiento, los de color verde son aquellos que tenemos preparados para hacer un commit, se le conoce como tenerlos en stage |
| ```git add {archivo} ```, ```git add index.html``` | Prepara un documento en stage para un commit |
| ```git add .``` | Prepara todos los documentos modificados en un stage |
| ```git reset {archivo}```, ```git reset index.html``` | Quita el archivo del stage |
| ```git commit -m "{mensaje del commit}"```, ```git commit -m "Primer commit"``` | Tomamos una fotografía de los cambios |
| ```git checkout -- .``` | Indicamos a Git que reconstruya el proyecto a como se encontraba el último commit |
| ```git branch``` | Vemos en que rama nos encontramos actualmente |
| ```git branch -m {nombre rama actual} {nuevo nombre}```, ```git branch -m master main``` | Comando para renombrar una rama en Git, no es algo que afecta a todos los repositorios, solo dentro del que nos encontramos |
| ```git commit -am "{mensaje del commit}"```, ```git commit -am "Readme actualizado"``` | Comando que realiza comando add y comando commit en uno mismo, pero solo funciona para archivos que ya previamente se tuvieron en un stage, si esta untracked no (sin haber hecho antes un git add .) |
| ```git log``` | Vemos el historial de los commits, el número que vemos es el id del commit, la rama donde se hizo, el autor y la fecha además del mensaje que se colocó, se veran del más reciente al más viejo |
| `````` | |
| `````` | |

### Practica No. 1

Todos los recursos y proyectos estan dentro de ```assets -> 01 -> 01-bases```.

```
git init
git status
git add index.html
git reset index.html
git add .
git commit -m "Primer commit"

# Ya no veremos archivos pendientes por darle seguimiento
git status

# Ajustemos algo en el código y hay que abrirlo
# Reconstruimos el proyecto al último commit
git checkout -- .

# Veremos rama master
git branch

# Cambiamos nombre de la rama
git branch -m master main

# Veremos rama main
git branch

# Hacemos que la rama principal sea main en vez de master
git config --global init.defaultBranch main

# Eliminamos carpeta .git (se destruye el repositorio) y volvemos a inicializar el repo, veremos rama main
git init
git add .
git commit -m "Primer commit"
git branch

# Consultamos la configuración global, veremos la configuración de la rama principal hecha antes
git config --global -e

```

Creamos un nuevo archivo llamado ```README.md``` con el siguiente contenido.

```
# Notas

Este es un repositorio de pruebas.
```

Continuamos con ```Git```.

```
git status
git add .
git reset README.md
git add .
git commit -m "README agregado"

# Eliminamos el archivo README
git checkout -- .

# Hacemos un cambio en el README
git commit -am "README actualizado"

# Consultamos el historico de los commits
git log
```

### Practica No. 2

Todos los recursos y proyectos estan dentro de ```assets -> 01 -> 02-bases```.

```
git init
git status

# Agregamos más de un documento al stage
git add .\index.html .\main.html
git reset .\index.html .\main.html

# Agregamos al stage todos los archivos de tipo .html (busca los archivos en el root)
git add *.html
git commit -m "Archivos HTML agergados"

# Agregamos todos los archivos JS dentro del forlder 'js'
git add js/*.js
git commit -m "Archivos JS agergados"

# Creamos un folder vacio llamado 'uploads', que nativamente lo ignora git, creamor archivo .gitkeep
git add uploads/*.gitkeep
git commit -m "Carpeta uploads agregada"

# Eliminamos la carpeta y podemos hacer lo siguiente para restaurarla
git checkout -- .e

# Indicamos a git que agregue todos los documentos dentro de una carpeta y los agregue al stage
git add css/
git commit -m "Estilos agregados"

git add .
git commit -m "Imagenes y fuentes agregadas"

git log
```

## Alias en Git

Podemos agregar banderas en los comandos de git

```
git status --short
```

Para crear un alias sería como lo siguiente.

```
git config --global alias.{nombre/comando del alias} "{comando que queremos ejecutar con el alias}"

git config --global alias.s "status --short"

# Podemos configurar el alias con el siguiente comando dentro del apartado [alias] (:wq para guardar, :q para cerrar sin guardar)
git config --global -e

# Ejecutamos alias s
git s

# Puede consultar la documentación oficial para ver los decoradores por comando
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"

# Ejecutamos alias lg
git lg

# Una alternativa de comando status
git config --global alias.s status -sb

# Ejecutamos alias s2
git s2
```
