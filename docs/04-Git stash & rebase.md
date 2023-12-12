# Git Stash y Git rebase - Para realizar cambios de emergencia

Tiene dos objetivo principales:
1. Stash: Veamoslo como una bobeda de archivos donde contendrá todos los cambios del último commit, es decir del HEAD. Es útil para cuando hay que desplegar cambios en nuestra app pero nosotros actualmente ya tenemos nuevas caracteristicas que no deberían de ser desplegadas aún.
2. Rebase: Permite unir o separar dos commits, se suele usar cuando no se han cargado cambios a un servidor ya que entre más grande el equipo, son más cambios y es más propenso a fallos.

Una recomendación es no cambiar la historia de un repositorio.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| Documentación oficial de ```git stash``` | https://git-scm.com/docs/git-stash |
| Documentación oficial de ```git rebase``` | https://git-scm.com/docs/git-rebase |

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git stash list``` | Listamos los stash que tenemos en el repositorio. El ```stash@{0}``` es el último stash añadido |
| ```git stash list --stat``` | Consultamos los stash con información del cambio de cada uno |
| ```git stash``` | Creamos un nuevo stash, los cambios que no estén dentro de un commit se quedan en el stash. Los stash también pueden generar conflictos al igual que ramas |
| ```git stash save "{nombre del stash}"``` | Agregamos un stash con nombre particular | 
| ```git stash pop``` | Recuperamos los cambios del último stash a la rama en la que estamos. Dicho último stash se elimina automaticamente, si tuvieramos más stashes, cambiaron de indice, el 1 se hizo 0, el 2 se hace 1, etc. |
| ```git stash clear``` | Borramos todos los stash del repositorio |
| ```git stash apply --index {índice}```, ```git stash apply --index 2``` | Restablecemos los cambios de un stash en una posición especifica según su indice, siendo 0 el último stash |
| ```git stash show {índice del stash}```, ```git stash show 1``` | Obtenemos la información de los cambios de un stash |
| ```git rebase master``` | Creamos un rebase con la rama master, este comando debe ejecutarse dentro de una rama que no sea la master ya que ahí es donde haremos el rebase (los commits de la rama dos hizo rebase con la rama master) |
| ```git rebase -i HEAD~{cantidad de commits}```, ```git rebase -i HEAD~4``` | Indicamos que queremos que los últimos 4 commits se consideren para entrar en un modo de rebase interactivo, dentro del mismo veremos opcioens que podemos realizar |
| ```git checkout -- README.md``` | Regresamos un archivo (en este caso README) a su estado original |

## TIL

El concetpo de ```Stash``` es demasiado sencillo, imaginemos que tenemos una app que se desplegó con ciertos cambios, nosotros seguimos trabajando en la app pero nuestro jefe nos pide desplegar nuevamente la versión anterior con un ajuste pequeño.

Si desplegamos el avance que tenemos, al no estar listo causaría problemas en la aplicación, pero el ```Stash``` nos permite colocar dichos cambios realizados, que no deberían desplegarse, en un tipo de bobeda, la cual los tendrá almacenados, de esa manera nosotros podemos volver a trabajar en la versión que se deplegó antes de la app y una vez resolvimos el problema, podemos sacar de la bobeda o del ```Stash``` dichos cambios para continuar con el nuevo desarrollo.

En ```git``` existe el concepto ```rebase```, imaginamos que tenemos la rama ```main``` y la rama ```cambios```, en esta última rama tenemos dos commits, pero al mismo tiempo se generaron dos commits en la rama ```main```, en ambas ramas tenemos dos commits en un mismo momento, pero necesitamos que los commits de la rama ```cambios``` existan despues de los commits de la rama ```main```. En estos casos el ```rebase``` es útil, ya que nos permite que mover a un área temporal una cantidad de commits y posteriormente recuperarlos en otro momento de la línea del tiempo del repositorio.

También existen los ```rebase``` interactivos, que no permiten trabajar de 4 diferentes manera con los commits:
1. Ordenar los commits
2. Corregir mensajes de los commits
3. Unir commits
4. Separar commits 

El uso del ```rebase``` interactivo debería usarse solo cuando nuestra historia del repo es local, si ya esta dentro del servidor externo se recomienda dejarlo así, ya que forma parte de toda la historia del repositorio.

# Practica No. 1

Vamos a trabajar con la practica ```07-demo-stash```, la cual es el contenido de ```assets -> 04 -> 07-demo-stash```.

```
git lg | git log

# Dentro de la rama master, modificamos misiones.md
# Stash no sería necesario si estamos trabajando en ramas.

# Sin hacer commit ni nada hacemos un stash (WIP on master: working in progress on master)
git stash

# Vemos en los logs el stash generado
git lg

# Todos los cambios que hemos hecho que no pertenecen a un commit estan guardados en el stash.
# Vemos que el archivo misiones.md ya no tiene los cambios que hicimos.

# Listamos los stash
git stash list

# Modificamos README.md
git commit -am "README updated"

# En este punto tenemos un stash y un commit
git lg | git log
git stash list

# Recuperamos el trabajo del último stash y se elimina de forma automática el stash
git stash pop
git stash list

# Ya no se encuentra el stash
git lg | git log

git commit -am "Misiones actualizadas"

# Ahora haremos lo mismo pero viendo conflictos al obtener los cambios del stash
# Modificamos el README.md
git stash

# Modificamos el README.md en las mismas lineas que el stash
git commit -am "README actualizado
git lg

# Recuperamos los cambios
git stash pop

# El stash digamos que es como una rama especial, debemos de ver un conflicto en el cual git no sabe que cambios deben persistir, aceptamos los cambios de venida
git commit -am "Conflictos en stash resueltos"

# Veremos que el stash aún sigue existiendo
git lg
git stash list

# Borramos todos los stash de git
git stash clear

# Modificamos villanos.md
git stash

# Modificamos villanos.md en las mismas lineas
git stash

# Modificamos villanos.md en las mismas lineas
git stash

# Veremos multiples stashs
git stash list

# Recuperamos el primer stash que hicimos
git stash apply --index 2

# Lo devolvemos al stash
git stash

# Veremos ahora 4 stashs, esto es porque no hicimos un drop del stash que antes recuperamos
git stash list

# Borramos stash de la posición 0 (índice 0)
git stash drop 0

# Consultamos un stash
git stash show 1

# Modificamos villanos.md y creamos stash con un nombre
git stash save "Agregamos a Loki en villanos"
git stash list --stat

git stash pop
git stash list

git commit -am "Agregamos a Loki en los villanos"
git stash clear
git stash list
```

# Practica No. 2

Vamos a trabajar con la practica ```08-demo-rebase```, la cual es el contenido de ```assets -> 04 -> 08-demo-rebase```.

## Rebase normal

Una alternativa a usar un merge y corregir conflictos.

```
# La rama 'rama-misiones-completadas' tiene dos commits pero no esta unida al master, y el master tiene 
# dos commits que deben de vivir dentro de la rama 'rama-misiones-completadas'
git branch
git checkout rama-misiones-completadas
git branch

# Nuestra rama 'rama-misiones-completadas' ya tiene los commits que tiene master
git rebase master
git lg | git log

git checkout master
git branch
git lg

# Se hace un merge en forma Fast-forward de rama-misiones-completadas a master
git merge rama-misiones-completadas
git lg
git branch -d rama-misiones-completadas
```

## Rebase interactivo - squash

```Squash``` nos permite fusionar dos o más commits en uno solo

```
# Modificamos misiones.md, quitamos punto 6 lo ponemos en misiones-completadas.md
git lg
git commit -am "Actualizamos misiones completadas"
git lg

# Los últimos dos commits es de lo mismo, no queremos tenerlo por separado sino en un solo commit
git rebase -i HEAD~4

# Presionamos 'a' para editar, y al último commit de arriba hacia abajo, le colocamos un squash (o solo s) en vez de pick, esto para indicar que tanto el último commit como el primero lo vamos a fusionar en uno solo, para guardar presionamos esc, dos puntos, wq (:wq)

# Si queremos fusionar 3 commits, debemos colocar squash en los últimos dos commits para que tome los últimos 3

---
pick 158ba9e Se agrego a la liga: Volcán Negro
pick 5d04ebf Agregamos el archivo de las misiones completadas
pick fb7d5b9 Actualizamos dos misiones completadas al momento
s    782c3e1 Actualizamos misiones completadas
---

# Nos muestra una pantalla para poder actualizar los mensajes del commit pero si no necesitamos no lo cambiamos, presionamos :wq! para salir

# Antes veiamos:
* f2cbeb9 - (2 seconds ago) Actualizamos misiones completadas - Emmanuel Toledo Castro (HEAD -> master)
* 93f9468 - (6 years ago) Actualizamos dos misiones completadas al momento - Strider
* 2449099 - (6 years ago) Agregamos el archivo de las misiones completadas - Strider

# Ahora vemos
* 87e91ba - (6 years ago) Actualizamos dos misiones completadas al momento - Strider (HEAD -> master)
* 2449099 - (6 years ago) Agregamos el archivo de las misiones completadas - Strider

# Los dos commits se fusionaron en uno solo
```

## Rebase interactivo - reword

Nos permite actualizar el nombre o mensaje del commit.

```
git lg

# Accedemos al rebase interactivo con los últimos 4 commits
git rebase -i HEAD~4

# Presionamos 'a' y en vez de pick ponemos 'reword' o 'r', luego esc, :wq
---
pick 300c014 Misiones nuevas agregadas
pick 158ba9e Se agrego a la liga: Volcán Negro
r 2449099 Agregamos el archivo de las misiones completadas
r 87e91ba Actualizamos dos misiones completadas al momento
---

# Nos mueve a la consola donde vemos los mensajes del primer commit.
---
Agregamos el archivo de las misiones completadas

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
...
---

# Ponemos algo como
---
Agregamos el archivo misiones-completadas.md

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    Strider <fernando.herrera85@gmail.com>
# Date:      Fri Jun 23 15:44:11 2017 -0600
#
...
---

# Presionamos esc, :wq!, veremos que nos pone una pantalla igual pero ahora apunta al otro commit al que le indicamos que ibamos a hacer un reword
git lg | git log
```

## Rebase interactivo - edit

Nos permite separar un commit en dos o incluso hacer modificaciones generales en el repositorio dentro del rebase y esto lo movemos al repo original (entiendase el rebase como un clon del repo).

```
# Modificamos README.md y misiones.md y villanos.md
# Tenemos tres cambios y queremos separar cada cambio en un commit diferente
git s

# Regresamos archivo README a su estado original
git checkout -- README.md

git commit -am "commits"
git lg

# Accedemos al modo rebase interactivo para separar un commit en dos
git rebase -i HEAD~3

# 'a' para editar, esc, :wq! para salir
---
pick f08864e Agregamos el archivo misiones-completadas.md
pick 448ea91 Misiones actualizadas
edit ba66e96 commits
---

# Debemos de continuar con el rebase, si vemos el estatus veremos el mensaje siguiente
# interactive rebase in progress; onto 158ba9e
# Indicando que estamos dentro del rebase interactivo
git status

# Eliminamos el último commit y lo bajamos del stage (es como estar en el punto del inicio de esta practica)
git reset HEAD^

# Damos seguimiento a villanos.md
git add villanos.md
git s
git commit -m "Agregamos a deadshot"

# Damos seguimiento a misiones.md
git commit -am "Misiones actualizadas"

# Seguimos en el rebase
git lg
git status

# Una vez listo todo vamos a hacer que el rebase continue, si tuvieramos un reword o algo más veriamos algo parecido a las practicas anteriores
git rebase --continue

# Ya no vemos commit con nombre 'commits'
git lg
```