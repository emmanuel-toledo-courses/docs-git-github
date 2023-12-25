# Wikis, Proyecyos y GitHub Pages

Estas secciones que veremos en GitHub es algo que muchas empresan pagan por pener, pero esta plataforma nos lo da de forma gratuita.

## TIL

```Wikis``` son usadas como una documentación de un repositorio de un proyecto, es como wikipedia. Para repositorios privados se requiere un pago para habilitar las Wikis desde las settings del repositorio, para repositorios públicos no es necesario.

Los ```Proyectos``` usados para darle seguimiento a las actividades de un equipo o persona. Se pueden tener tantos proyectos como se requieran. Pensemos que es como Asana o incluso algo similar a DevOps.

Los ```GitHub Pages``` son usados para desplegar páginas web dentro de los servidores de ```GitHub ```.

Trabajaremos sobre el repositorio de [avengers](https://github.com/emmanuel-toledo/docs-git-github-practice-avengers).

Puede ver configuración respecto a las ```Wikis``` dentro del apartado de configuración. Al final del día la wiki trabaja con Markdown (md).

Se pueden linkear páginas a partir de agregar un enlace en la página, además el sidebar nos permite colocar un menú lateral.

Podemos crear un proyecto en el apartado de ```Projects``` dentro de un repositorio, podemos crear labels para colocar categorías a las actividades y también crear issues a partir de las mismas así como asignarlas a un proyecto en particular y también a un usuario.

Las ```GitHub``` pages son host gratuitos de GitHub que nos permiten desplegar páginas web sencillas tanto para nuestro usuario como para una organización así como también para un repositorio. Permite colocar código HTML, CSS y JavaScript. No podemos cargar código Python, PHP y otros, pero si permite consumir web services de estos.

Para crear un GitHub pages debe de crear un repositorio nuevo y llamarlo ```{nombre de usuario}.github.io```.
- https://github.com/emmanuel-toledo/emmanuel-toledo.github.io
Vamos a settings y seleccionamos la opción pages donde podemos aplicar cierta configuración, así como también poder ver la ruta de la página.

Podemos hacer lo mismo para el repositorio de avengers por medio de la rama main o de una carpeta especifica. 

```
git checkout -b rama-web
mkdir docs
# Creamos proyecto HTML dentro.
git add .
git commit -m "Sitio web listo"
git checkout main
git merge rama-web
git pull
git push
```

Dentro de ```settings -> pages``` podemos seleccionar la rama main y el folder donde se aloja nuestro sitio web para desplegar la web. Se acostumbró a dejar el folder llamado docs como el encargado de almacenar el sitio web ah publicar. 

Veremos un sitio en una URL como la siguiente.
- https://emmanuel-toledo.github.io/docs-git-github-practice-avengers/

Ya cuenta con certificado HTTPS y no es necesario agregar ningún otro tipo de configuración.

Podemos ver los ```Insights``` de un repositorio, lo cual nos mostrará los movimientos que existen desde nuestro repositorio, tales como.
1. Tags.
2. Pull requests.
3. Issues.
4. Etc.

Un ejemplo sería ver lo siguiente.
- https://github.com/facebook/react/pulse