# Un poco más allá de los fundamentos de Git

Todos los recursos y proyectos estan dentro de ```assets -> 02```.

## TIL

Recordemos que los ```commit``` son un recuerdo del tiempo de vida del repositorio al cual podemos dirigirnos si lo requerimos.

## Glosario de comandos

| Comando | Descripción |
| ------------- | ------------- |
| ```git diff``` | Permite ver las modificaciones de los archivos del repositorio que no estan dentro del stage |
| ```git diff --staged``` | Permite ver las modificaciones de los archivos del repositorio que si se encuentran en el stage |
| `````` | |
| `````` | |
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


```

