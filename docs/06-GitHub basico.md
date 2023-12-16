# GitHub - Básico

Veremos a más detalle como funcionan los ```Markdown``` (md) como también el uso de los ```Pull Requests``` que tenemos en ```GitHub```.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| Documentación oficial | https://docs.github.com/es |
| Emojis en GitHub | https://www.webfx.com/tools/emoji-cheat-sheet/ |
| Ejercicios Markdown | https://www.markdowntutorial.com/ |
| Entendiendo el flujo de trabajo de GitHub | https://blog.mergify.com/understanding-the-github-pull-request-workflow/ |

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git fetch``` | Comando que nos ayuda a actualizar las referencias y commits que tenemos en el repositorio remoto sin modificar el contenido del repositorio local como si sucede con el comando git pull |

## TIL

```GitHub``` la mayor parte del tiempo usa el lenguaje ```Markdown``` para dar de alta diferentes interacciones con la plataforma.
- Issues
- Pull Requests
- Etc.

El nombre de la mascota de ```GitHub``` es ```Octocat```.

La opción ```Blame``` nos ayuda a ver quienes actualizaron que cosas en un archivo en particular dentro de ```GitHub```, su traducción es cumpable.

Cada ```commit``` se puede considerar de una forma como una rama, ```GitHub``` permite movernos a un punto del tiempo del repositorio según un ```commit```.

Los ```commits``` verificados son aquellos en los que ```GitHub``` detecta nuestra cuenta como propietaria de un ```commit``` en el repo.

También es posible borrar archivos desde ```GitHub```.

Al igual que al eliminar, podemos crear un nuevo archivo desde ```GitHub```.

Un ```Pull Requests``` es utilizado cuando queremos mover cambios de la ```rama2``` a la ```rama1```, realmente lleva a cabo el proceso del ```merge```, pero la idea principal del ```Pull Requests``` es poder llevar a cabo un analisis de todo el código que se va a mover de una rama a otra, además de que nos permite llevar a cabo autorizaciones, por medio de usuarios, que podrían autorizar o no el merge de las ramas.`

```GitHub``` nos permite agregar comentarios por cada commit e incluso por cada línea de código nueva de cada archivo. Estos comentarios los podemos ocultar si lo necesitamos, aunque no se verían más no se eliminar realmente.

# Practica No. 1

Hagamos cambios en el repositorio remoto, sabemos que podemos descargar cambios con el comando pull, pero si solo queremos actualizar referencias, es decir, la historia del repositorio como lo son los commit, podemos hacer lo siguiente.

```
git lg | git log

# Actualizamos la historia y referencias del repositorio local con lo que se encuentra en el repositorio remoto
git fetch

git lg | git log
```

# Practica No. 2

```
# Agregamos un correo electrónico de otra persona en el [user] email y un nombre diferente
git config --global -e

# Modificamos el repo
git commit -am "README actualizado"
git lg
git push
```

Veremos que otro usuario hizo dichos cambios, pero realmente no fue así, es una vulnerabilidad que tiene la plataforma que se presta a malas practicas, eso si, los commits no estarán verificados realmente, y esto puede ayudarnos a encontrar un cumpable de ciertos cambios.