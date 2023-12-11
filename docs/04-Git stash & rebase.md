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
| `````` | |
| `````` | |
| `````` | |

## TIL

El concetpo de ```Stash``` es demasiado sencillo, imaginemos que tenemos una app que se desplegó con ciertos cambios, nosotros seguimos trabajando en la app pero nuestro jefe nos pide desplegar nuevamente la versión anterior con un ajuste pequeño.

Si desplegamos el avance que tenemos, al no estar listo causaría problemas en la aplicación, pero el ```Stash``` nos permite colocar dichos cambios realizados, que no deberían desplegarse, en un tipo de bobeda, la cual los tendrá almacenados, de esa manera nosotros podemos volver a trabajar en la versión que se deplegó antes de la app y una vez resolvimos el problema, podemos sacar de la bobeda o del ```Stash``` dichos cambios para continuar con el nuevo desarrollo.

En ```git``` existe el concepto ```rebase```, imaginamos que tenemos la rama ```main``` y la rama ```cambios```, en esta última rama tenemos dos commits, pero al mismo tiempo se generaron dos commits en la rama ```main```, en ambas ramas tenemos dos commits en un mismo momento, pero necesitamos que los commits de la rama ```cambios``` existan despues de los commits de la rama ```main```. En estos casos el ```rebase``` es útil, ya que nos permite que mover a un área temporal una cantidad de commits y posteriormente recuperarlos en otro momento de la línea del tiempo del repositorio.

También existen los ```rebase``` interactivos, que no permiten trabajar de 4 diferentes manera con los commits:
1. Ordenar los commits
2. Corregir mensajes de los commits
3. Unir commits
4. Separar commits 


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

```
```