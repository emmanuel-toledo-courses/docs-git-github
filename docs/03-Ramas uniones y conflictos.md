# Ramas, uniones, conflictos y tags

Por cada cambio que queramos hacer en nuestro repositorio, deberíamos de crear una rama para no afectar código que arruine la funcionalidad de la aplicación.

Podemos ver las ramas como una copia del proyecto en si que nace a partir de una rama que llamaremos rama principal, de esta se pueden crear N ramas y pasarian a ser ramas hijas.

Veremos como ```git``` nos ayuda al momento de resolver conflictos al momento de tratar de unir el contenido de una rama a otra.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| ```git branch``` | Consultar listado de ramas dentro del repo, la rama del color resaltado o con el * sería la rama en la que nos encontramos |
| ```git branch {nombre rama}```, ```git branch rama-villanos``` | Crear una nueva rama |
| ``` git checkout {nombre rama}```, ```git checkout rama-villanos``` | Movernos a una rama en particular |
| ```git checkout -b {nombre rama}```, ```git checkout -b rama-villanos``` | Crear y movernos automáticamente a una rama nueva |
| ```git merge {nombre rama}```, ```git merge rama-villanos``` | Hacemos un merge entre ramas, en la rama ```main``` hacemos merge con los cambios de la rama ```rama-villanos``` |
| ```git branch -d {nombre rama}```, ```git branch -d rama-villanos``` | Eliminar una rama |
| ```git branch -d {nombre rama} -f```, ```git branch -d rama-villanos -f``` | Eliminar una rama de manera forzada si es que existen cambios dentro de la misma a la cual no se le ah aplicado un merge con otra rama |
| ```git tag {nombre tag}```, ```git tag super-release``` | Establece un tag al último commit de nuestra rama |
| ```git tag``` | Consultar lista de tags |
| ```git tag -b {nombre tag}```, ```git tag -d super-release``` | Borramos un rag |
| ```git tag -a {nombre tag} -m "{mensaje}"```, ```git tag -a v1.0.0 -m "Versión 1.0.0 lista"``` | Creamos un tag en versión anotada para agregar un mensaje |
| ```git tag -a {nombre tag} {id de commit} -m "{mensaje}"```, ```git tag -a v0.1.0 64f7daf -m "Version Alpha de nuestra app"``` | Se crea un tag asociado a un commit en particular |
| ```git show {nombe tag}```, ```git show v0.1.0``` | Consultar los detalles de un tag especifico, tales como info en si del tag, el commit y los cambios que se hicieron asi como el autor |

## TIL

Una ```rama``` es una línea del tiempo de diferentes commits. Nos ayudan para agregar funcionalidades que puedan ser agregados a la rama principal. Cada rama es independiente, no choca una con la otra a menos que hagamos algo llamado ```merge```.

Un ```merge``` es la union de una rama con otra, por ejemplo unir cambios de ```dev``` a ```main```, pueden suceder tres escenarios:
1. Fast-foward: Una caracteristica natural de git que detecta que la rama principal no contiene los cambios de la rama con la que lo queremos unir, por ende los cambios de la rama ```dev``` a la rama ```main``` lo hace de forma transparente.
2. Uniones automáticas: Cuando existe en la rama ```main``` un cambio que la rama ```dev``` desconoce, pero los cambios de la rama ```dev``` no afectan ninguno de los cambios que ya tiene la rama ```main```, entonces une los cambios de forma automática y transparente.
3. Manual: Cuando existen cambios en la rama ```main``` pero la rama ```dev``` también realizó cambios en los mismos archivos de los cambios la rama ```main```, entonces git por si solo no podrá hacer el merge, ya que no sabrá que cambios deben de ser los que persistan, en estos casos un desarrollador debe de indicarle a git que cambios deben de prevalecer, quizas serán los de ```main```, los de ```dev``` o incluso ambos. A estos escenarios se les conoce como ```conflictos```.

Los ```tags``` o etiquetas no son más que una referencia a un commit específico. Son usualmente usados para marcar versiones o releases de nuestra aplicación.

# Practica No. 1

Vamos a trabajar con la practica ```06-demo```, la cual es el contenido de ```assets -> 03 -> demo-06.zip```.

```
## MERGE FAST-FOWARD:

git lg | git log

# Creamos archivo villanos.md
# Creamos una nueva rama para trabajar
git branch
git branch rama-villanos
git checkout rama-villanos
git branch
git lg | git log

# Al ver '(HEAD -> rama-villanos, master)' indica que la rama master y rama-villanos estan paradas en el mismo momento de la linea del tiempo del repo
git add .
git commit -m "Villanos.md: Agregado"

# Ahora veremos como la rama master y rama-villanos se encuentran en commits diferentes
git lg | git log

# Modificamos archivo villanos.md
git add .
git commit -m "Villanos.md: Flash reverso"
git lg | git log

# Si nos movemos entre las ramas veremos que el archivo villanos.md ya no existe incluso si lo vemos en el explorador de archivos
git checkout master
git branch

# Hacemos un merge o union entre ramas
git merge rama-villanos

# Veremos mensaje 'Fast-forward', lo que significa que todo paso de forma transparente
# Ambas ramas apuntan al último commit
git lg | git log

# Usualmente cuando dejamos de usar una rama se debería de eliminar
git branch -d rama-villanos

## MERGE UNION AUTOMÁTICA:

git checkout -b rama-villanos
git branch

# Modificamos archivo villanos.md
git commit -am "Agregamos a Doomsday"

# Modificamos archivo villanos.md
git commit -am "Agregamos a notas a villanos"
git lg | git log

git branch
git checkout master

# Borramos un heroe de heroe.md
git commit -am "Borramos a Daredevil"

# Veremos una difurcación entre los commits de la rama
git lg | git log

# Realizamos un merge (Merge made by the 'ort' strategy)
git merge rama-villanos

git lg
git branch -d rama-villanos

## MERGE CON CONFLICTOS:

# Un merge con conflictos suceden cuando en dos ramas se modifican una o más mismas lineas de código de un mismo archivo
git checkout -b rama-conflicto

# Modificamos punto 3 de archivo misiones.md
git branch
git commit -am "Misiones.md: Actualizada"
git lg

# Modificamos punto 3 y agregar punto 4 de archivo misiones.md
git checkout master
git commit -am "Misiones.md: Actualizada MASTER"

# En ambas ramas modificamos un mismo archivo y con eso una misma línea
# Realizamos un merge
git merge rama-conflicto

# Los archivos que no dan conflicto pasan de forma natural, pero los que no, debemos de ver las diferencias en Visual Studio Code, el icono que coloca es !, pasamos el punto 4 a la parte de la rama conflicto (si lo abren en bloc de notas verá lo mismo)
git commit -am "Union con rama conflicto"

# Se resolvio el conflicto que se tenía entre ramas
git branch
git branch -d rama-conflicto
```

# Practica No. 2

Vamos a trabajar con la practica ```06-demo```, la cual es el contenido de ```assets -> 03 -> demo-06.zip``` para ver el uso de ```tags```.

```
git lg
git tag super-release

# Veremos también el tag recién creado
git lg | git log
git tag
git tag -d super-release
git tag

# 1, cambios grandes o de gran escala de la aplicación
# 0, se añadieron ciertas funcionalidades a la aplicación pero no es de gran escala
# 0, se corrigio un error en la app
git tag -a v1.0.0 -m "Versión 1.0.0 lista"
git tag
git lg

# Copiamos el hash del commit (Villanos.md: Flash reverso)
git tag -a v0.1.0 64f7daf -m "Version Alpha de nuestra app"
git tag
git lg
git show v0.1.0

git tag
```
