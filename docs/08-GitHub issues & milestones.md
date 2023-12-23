# GitHub Issues, MileStones y Colaboradores

Veremos como aplicar diferentes configuraciones a nuestro repositorio de GitHub, vamos desde configurar colaboradores como el uso de los issues.

Pensemos en un ```colaborador``` como alguien que va a tener acceso de lectura y escritura dentro del repositorio e incluso permisos de administración del mismo, no es lo mismo que un equipo de trabajo.

Un ```MileStone``` es algo importante que queremos que pase, un hito, es un tipo de MVP del proyecto que puede tener multiples issues que se deben corregir para cierta fecha.

Veamos un  ```issue``` como preguntas del repositorio, no solo para reportar realmente un error en el proyecto.

## URL's de apoyo

| Descripción | URL |
| ------------- | ------------- |
| GitHub - Propuestas | https://docs.github.com/es/issues/tracking-your-work-with-issues/about-issues |

## TIL

Los ```issues``` son usados comunmente para escribir alguna duda o pregunta respecto al proyecto, no solamente para reportar errores. En el apartado de issues, podemos ver también los pull request, esto es porque github registra en un mismo lugar pero con diferentes caracteristicas issues y pull request, por ello del filtrado que se coloca al inicio.

Los índices que se generan para estas dos tareas, normalmente no deberían de moverse, deben quedarse tal cual están.

Cuando cerramos un issue normalmente es cuando ya hubo un desarrollo en donde se atendió dicho issue.
Un issue no se elimina, siempre existen, solo se pueden cerrar.

Si se crea un issue por error, puede colocar un mensaje indicando eso para evitar confusiones. Una vez que se cierra el issue no se puede editar nuevamente.

Podemos generar templates para ciertos tipos de issues lo cual puede ayudar al momento de darlos de alta, sería en ```repositorio -> settings -> issues -> setup templates```. Veremos los template listos en la pantalla de issues.

Podemos generar etiquetas que nos ayudan a organizar nuestras issues. ```repositorio -> issues -> labels```.

Un ```Milestone``` es un agrupador de issues de un repositorio. Pueden usarse para dividir sprints.

Podemos agregar colaboradores a un repositorio y asignar ciertos privilegios a cada uno.
```repositorio -> settings -> manage access -> add people```

# Practica No. 1

Trabajamos en el repositorio ```11-avengers```.

Creamos issue para agregar a Nick Fury en los miembros.

```
git commit -am "Agregamos a Nick Fury"
git push
git lg
```

Cerramos el issue ligando el nuevo commit usando el id generado.

Esto funciona para GitHub.
Creamos un nuevo issue para quitar un personaje y guardamos el indice que se colocó.

```
git commit -am "Fixes #5: Hecho, se borro a Capitan Marvel"
git push
```

```Fixes #5``` hace referencia a un issue y el numero indica el indice del issue, hace que se cierre de forma automática.