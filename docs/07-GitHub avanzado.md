# GitHub - Avanzado

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| Repositorio externo | https://github.com/Klerith/legion-del-mal |
| Repositorio externo | https://github.com/klerith/avengers |


## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git remote -v``` | Obtenemos listado de origenes que tenemos en nuestro repositorio local |
| ```git remote prune origin``` | Obtener listado de las ramas eliminadas remotamente y actualiza las referencias locales |

## TIL

Hemos visto como clonar repositorios con ```git pull```, si hubiera un repositorio en donde no somos los propietarios debemos de asegurarnos de ser colaboradores o miembros para accesar al repo.

Si no somos colaboradores de un repositorio podremos hacer un ```git pull```, pero será imposible hacer un ```git push```. Podemos realizar un ```fork```, que básicamente haría una clonación del repositorio al que queremos acceder pero ahora pertenecerá a nuestro usuario.
    - google/maps
Se hace un ```fork``` y terminamos teniendo el repositorio.
    - mi_usuario/maps
Una vez hecho alguna modificación, podemos solicitar un ```pull_request``` al repositorio ```google/maps``` y ellos le darán el seguimiento para agregar o no los cambios que realizamos.

Es común que en una empresa solo se tenga un repositorio remoto sin necesidad hacer un ```Fork``` por cada miembro del trabajo.
- Rama main:
    - Rama feature 1
    - Rama feature 2
    - ...
Usualmente se puede hacer un merge por consola desde la rama feature a la rama main, y posteriormente un push, o también se puede cargar la rama feature al server, hacer un pull request y una vez listo eliminar la rama feature que ya no se va a necesitar.

# Practica No. 1

Vamos a usar este [repositorio](https://github.com/Klerith/legion-del-mal). Podemos llevar a cabo un ```fork``` dentro para este repositorio.
- https://github.com/emmanuel-toledo/docs-git-github-practice-legion-del-mal

```
git clone https://github.com/emmanuel-toledo/docs-git-github-practice-legion-del-mal.git

# Renombramos por: 10-legion-del-mal
cd 10-legion-del-mal
git lg | git log
git commit -am "README.md: Updated"
git push

# Modificamos miembros
git commit -am "Borre espanta pajaron"

# Agregamos un aspirante
git add .
git commit -m "Solicitud de Emmanuel"
git push
```

Veremos un botón llamado ```Contribute``` en donde podremos comenzar el ```Pull Request``` de colaboración o contribución al repositorio principal. Si olvidamos hacer algo...

```
git commit -am "README con nombre Emmanuel"
git push
```

Podemos ver que los cambios que agreguemos entrarán automaticamente dentro del ```Pull Request```.
Podemos dar click en ```Create pull request```. Veremos que el ```Pull request``` se quedo en estado de autorización por el propietario real del repositorio.

Si fueramos el dueño del repositorio podremos aceptar o rechazar el ```Pull request```.

Vamos a la pantalla de ```Pull requests``` pendientes, seleccionamos el registro que se validaría, podemos dar clic en ```files changed``` para ver los cambios de los archivos, y dar clic el botón ```review changes```, seleccionamos la opción ```request changes``` si queremos que se modifique algo antes del merge.

Vamos a revertir un cambio en miembros.md, ya que no debimos haber eliminado al espanta pájaros.

```
# Obtenemos commit id previo a la eliminación del espanta pájaros
git lg

# Revertimos el commit solo al archivo miembros.md
git checkout 96035a3 miembros.md

git commit -am "Corregimos archivo de miembros"
git push
```

Una vez hecho los ajustes por lo que rechazaron el ```Pull Request```, podemos enviar comentarios diciendo el cambio.

El propietario del repositorio puede dar clic a ```Merge pull request```.

Con esto los cambios se llevaron a cabo desde el fork al repositorio principal.

# Practica No. 2

Trabajamos sobre ```10-legion-del-mal```.

Si queremos actualizar nuestro ```Fork``` con lo nuevo del reposiutorio principal, podemos usar el botón ```Sync fork```, en donde veremos los commits nuevos que existan.

```
git lg
git pull origin
git lg
```

Si queremos hacer esto mismo a traves de la consola sería un tanto diferente.

```
# Veremos el origin del repositorio
git remote -v

# Si solo queremos actualizar los cambios que vienen del server, podemos agregar un nuevo origin llamado upstream
git remote add upstream https://github.com/Klerith/legion-del-mal

git remove -v

# Tomará automaticamente el origin
git pull

# Bajamos cambios del repo con origen upstream
git pull upstream master

# Si estamos dentro de un rebase por algun conflicto podemos corregirlo
git status
git commit -am "Upstream actualizado"
git rebase --continue
git lg
git push
git lg
```

# Practica No. 3

Descargamos el zip del [repositorio](https://github.com/klerith/avengers) y llamamos la carpeta ```11-avengers```. Creamos un repositorio en GitHub.

```
git init

# Agregamos archivo .gitignore
git add .
git commit -m "Initial commit"

git remote add origin https://github.com/emmanuel-toledo/docs-git-github-practice-avengers.git
git branch -M main
git push -u origin main

git tag -a 0.0.1 -m "Versión Alpha"
git tag
git push --tags

# Creamos archivo villanos.md
git checkout -b rama-villanos
git add .
git commit -m "Villanos.md agregado"
git lg

# Cargamos la rama al remoto
git push --set-upstream origin rama-villanos

# Veremos el mensaje en GitHub: rama-villanos had recent pushes 11 seconds ago
# Damos clic en compare & pull request
# Agreguemos un nuevo villano sin finalizar el pull request

git commit -am "Doctor herrera agregado"
git push

# Finalizamos el request con un merge commit
# Eliminamos la rama que estabamos usando desde GitHub

git checkout main
git pull
git branch
git branch -d rama-villanos

# Si existieran cambios en una rama que queremos eliminar que aún no se han unido, podemos ejecutar.
git branch -d rama-villanos -f

# Consultamos los cambios junto con la rama en la que nos encontramos
git status --short -b

# Configuramos el alias (comando) git s
git config --global -e
```

Creamos una nueva rama desde ```GitHub``` llamada rama-misiones y agregamos un archivo misiones.md.

```
# Obtenemos la rama nueva, pero no bajamos cambios del main
git pull | git pull --all

# Solo vemos las ramas locales donde estamos participando
git branch

# Consultamos todas las ramas
git branch --all
git checkout rama-misiones

# Modificamos misiones.md
git commit -am "Misiones actualizadas"
git push

# Hacemos pull request y eliminamos la rama desde GitHub
# La rama sigue viviendo localmente
git branch -a | git branch --all

# Eliminamos las ramas que se quedaron que no son necesarias
git checkout main
git pull
git branch -d rama-misiones
git branch -a 

# Vemos algo como lo siguiente:
# * main
#  remotes/origin/main
#   remotes/origin/rama-misiones
#   remotes/origin/rama-villanos

# Este comando hubiera eliminado la rama-misiones de forma local y remota, pero la remota se eliminó desde GitHub.
git push origin :rama-misiones
git push origin :rama-villanos

git branch -a

# Obtener listado de las ramas eliminadas remotamente y actualiza las referencias locales
git remote prune origin

# Ya no vemos rama-misiones y rama-villanos
git branch -a
```

# Practica No.3 

```
git checkout -b rama-kitkat

# Modificamos villanos.md
git commit -am "Updated villanos.md"
git push --set-upstream origin rama-kitkat
git tag 
git tag -a v1.0.0 -m "Ktkat v1.0.0 - Stable"
git push --tags

# Creamos un release llamado: 'Versión Kitkat 1.0.0 Latest'
# Ahora, podemos decir que nuestra rama principal es kitkat, y es la versión de la aplicación que el cliente quiere usar
# Eliminamos la rama kitkat desde GitHub
# El release tag aún perdura incluso cuando la rama se eliminó

# Podemos recuperarla se forma sencilla
git s
git push

# Eliminamos la rama kitkat desde GitHub
git branch -d rama-kitkat
git remote prune origin
git branch -a

# Vamos a recuperar una rama que por alguna razón ya no existe ni en el remoto ni localmente
git tag
git checkout v1.0.0
git branch
git lg

# No encontrmaos dentro de un tag, no un branch
git s
git checkout -b rama-kitkat
git s
git push --set-upstream origin rama-kitkat

# Eliminamos la rama desde local
git checkout main
git branch -d rama-kitkat
git push origin :rama-kitkat

# Podemos crear una rama basada en un tag, simplemente vamos desde GitHub al tag y posteriomente decimos que queremos movernos a una rama en particular y colocamos rama-kitkat, de esta manera nos indicará GitHub que va a generar una rama nueva llamada rama-kitkat basada en el release tag v1.0.0
```
