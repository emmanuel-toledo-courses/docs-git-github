# Inicios en GitHub, Git Remote, Git Push & Git Pull

Veremos como podemos integrar y trabajar nuestros repositorios locales pero haciendo uso de ```GitHub```, cambiando de usar repositorios locales a un repositorio remoto.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| Portal GitHub | https://github.com/ |
| Iniciar sesión en GitHub desde Git, WINDOWS | https://docs.github.com/es/get-started/getting-started-with-git/caching-your-github-credentials-in-git#platform-windows |

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git push``` | Permite subir cambios a nuestro repositorio remoto, tales como ```GitHub``` |
| ```git remote add origin {url repositorio en github}``` | Agregamos un origen remoto a nuestro repositorio local, ```add``` es para agregar un nuevo repo remoto, ```origin``` el nombre que le damos al repo remoto, por estandar se acostumbra a poner ```origin``` pero puede ser otro diferente, ```{url github}``` es la dirección url de nuestro repositorio |
| ```git remove -v``` | Listar los repositorios remotos que se encuentran ligados al repositorio local |
| ```git push -u origin master``` | Cargamos una rama (con todos sus cambios) a nuestro repositorio remoto, requiere que hagamos un inicio de sesión |
| ```git branch -M main``` | Cambiar nombre de la rama en la que nos encontramos, usualmente usada para cambiar master por main |
| ```git push --tags``` | Cargamos los tags locales a nuestro repositorio en ```GitHub```, si un tag ya existe lo actualiza, si no, lo crea |
| ```git pull```, ```git pull origin main``` | Descargamos los cambios del repositorio desde ```GitHub``` hacia el repositorio local |
| ```git clone {url HTTPS del repositorio}``` | Clonamos el repositorio remoto en un repositorio local del equipo |

## TIL

```GitHub``` no es lo mismo que ```Git```, ```GitHub``` es una herramienta de administración de repositorios de forma remota. ```GitHub``` actualmente pertenece a ```Microsoft```. La version gratuita es demasiado completa, ya que podemos crear repositorios publicos (cualquier persona podrá ver nuestro repo) y repositorios privados.

Existen otras plataformas similares, tales como ```GitLab```, ```Bitbucket``` u otros.

También existen formas de generar un hosting de repositorios de git, usando herramientas tales como [Gitosis](https://wiki.archlinux.org/title/gitosis#:~:text=Gitosis%20is%20a%20tool%20which,system%20accounts%20on%20the%20server.).

```git push -u origin main```: ```origin``` es el nombre del repositorio (origen) remoto, podemos agregar más de un origen, usualmente se nombra ```origin``` al principal, pero puede ser diferente. ```main``` es el nombre de la rama que queremos cargar al repo remoto, ```-u``` es para indicar que en futuros ```push``` ya no sea necesario definir la rama, solo hacer un ```git push``` estando trabajando dentro de la rama que queremos cargar al repo remoto. Si queremos cargar un cambio de una rama de un origen diferente o especifico, usamos ```git push origin```, el nombre de la rama lo tomaria según la rama donde estemos trabajando.

# Practica No. 1

Vamos a trabajar con la practica ```09-heroes```, la cual es el contenido de ```assets -> 05 -> 09-heroes```.

Si sucediera un error en nuestra máquina podríamos perder todo el progreso, por eso podemos moverlo a GitHub. Creamos un repositorio en GitHub llamado 'docs-git-github-practice-liga-justicia' y que sea publico, una vez creado debemos de cargar nuestro repositorio local al repositorio en ```GitHub```.

Para iniciar un repositorio desde cero (no es nuestro caso).

```
echo "# docs-git-github-practice-liga-justicia" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/emmanuel-toledo/docs-git-github-practice-liga-justicia.git
git push -u origin main
```

Para cargar a ```GitHub``` repositorio local (es nuestro caso).

```
git remote add origin https://github.com/emmanuel-toledo/docs-git-github-practice-liga-justicia.git
git branch -M main
git push -u origin main
```

En ambos casos, si no tenemos iniciada nuestra sesión con ```GitHub``` dentro de ```Git```, nos solicitará un inicio de sesión.

```
git lg | git log

# Si vemos nuestro repositorio veremos el total de commits, ramas y tags entre otras cosas, pero no vemos los tags que estan localmente.

git tag

# Una vez cargados los tags, podemos descargarlos desde GitHub. 

git push --tags

# También se pueden generar un release basado en un tag, 
# donde podemos dar más información respecto a un tag en particular. Al crear un release podemos
# agregar archivos de apoyo, usualmente se adjuntan los proyectos compilados.
# Podemos crear un pre-release, que es algo similar al release, solo que indica que aún no esta completamente listo nuestro release.
# Una vez listo un pre-release o release podremos descargar los archivos de nuestro repo hasta ese punto del tiempo de vida del mismo.

# Podemos editar los archivos desde nuestro repositorio en GitHub (usualmente no se hace en rama main).
# Esto sería un escenario donde otro usuario hizo cambios en el repositorio y lo cargó a GitHub.
# Una vez hecho cambios debemos descargarlos.

git lg
git pull | git pull origin main
git lg

# En ocasiones al hacer un pull podremos ver un mensaje de warning que dice algo como lo siguiente:
# Pulling without specifying how to reconcile...
# El mensaje nos dice que debemos de indicar como queremos que nuestro repositorio interactue cuando hacemos
# un pull desde el repositorio remoto al local
# git config pull.rebase false # Solo hacer un merge 
# git config pull.rebase true # Hacer un rebase
# git config pull.ff only # Solo aplica los cambios si podemos hacer un Fast-Foward

# La que es común usar es la última. Agregamos la configuración global.
git config --global pull.ff only
git config --global -e

# Cargamos otro cambio desde GitHub y probamos.
git lg
git pull | git pull origin main

# Veremos que el HEAD -> main, y el origin/main estan al mismo nivel
git lg

# Eliminamos todo el repositorio 09-heroes, pero ahora podemos clonarlo por medio de HTTPS
git clone https://github.com/emmanuel-toledo/docs-git-github-practice-liga-justicia.git

# Descargo el repositorio en un folder llamado 'docs-git-github-practice-liga-justicia' que es el nombre del repositorio remoto en github, podemos cambiar el nombre de la carpeta al que teniamos antes.
# Los archivos que no vemos son los que colocamos en el archivo .gitignore

# Modificamos el README.md
git commit -am "README.md actualizado"

# El HEAD -> main se encuentra en un commit y el origin/main se encuentra en otro
git lg | git log

git push

# Editemos el README desde github en una linea especifica, del mismo modo lo hacemos en el repo local
git lg
git commit -am "README.md: Local actualizado"
git pull

# Veremos mensaje: fatal: Not possible to fast-forward, aborting.
# Esto porque configuramos el fast-fordward al hacer un pull (git config --global pull.ff only)
# No siempre pasara facilmente, podemos entrar a un rebase interactivo.

# Editamos para quitar (ff...)
git config --global e

# Configuración local del repo, no es global (--global)
git config pull.rebase true
git pull

# Resolvemos los conflictos manteniendo ambos cambios
# Vemos que estamos en interactive rebase in progress;
git status
git add .
git commit -m "README unificado con origin/main"
git s
git status

# Debemos de completar o continuar el rebase
git rebase --continue

# Veremos el mensaje: Successfully rebased and updated refs/heads/main.
git push

# Configuramos rebase global, cada que hagamos un pull con conflictos entraremos al rebase
git config --global pull.rebase true
git pull

# Modificamos ciudades.md, villanos.md y heroes.md en GitHub
# Tenemos 3 nuevos commmits que se encuentran remotamente
# Modificamos localmente ciudades.md y heroes.md en las mismas lineas que GitHub
git commit -am "Ciudades y héroes actualizados"
git push

# Veremos herrores debido a conflictos, para corregirlos debemos hacer un pull
git pull
# Encontramos conflictos en ciudades.md y heroes.md, los demás cambios pasaron correctamente
# Vamos a resolverlos los conflictos pendientes
# heroes.md: Accept current changes
# ciudades.md: Eliminamos punto 3 y aceptamos incomming changes
git status
git add .
git status
git commit -m "Unificado ciudades y heroes"
git status # Seguimos en rebase
git rebase --continue
git status # Salimos del rebase
git push
```
