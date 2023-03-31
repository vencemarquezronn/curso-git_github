¡Hola Mundo!

Estas son mis notas del curso de Git y GitHub de Plazti.

Estoy redactando las notas y aplicando en el archivo a medida que avanzo.

# Cambio de metadata del editor

Se pueden cambiar los valores por defecto del autor para trazabilidad de quién está haciendo los cambios.

```bash
git config --global user.name "Tu nombre" # Cambia el nombre del autor en Git
git config --global user.email "tu@email.com" # Cambia el correo electrónico del autor en Git.
```

# Creación de un repositorio y primer commit

Una vez creada una carpeta y estando dentro de la carpeta, se puede crear un archivo, modificarlo, y ver quién hizo los cambios.

```bash
mkdir Example
cd Example
touch Archivo.txt
code . #Se hacen cambios en VS Code

git init
git status # Muestra el estado de los archivos del repositorio, se agrega el archivo
git add . # Agrega todos los archivos del repositorio
git commit -m "Initial commit" # Hace el primer commit con un mensaje que afirma eso.
git log Archivo.txt # Muestra la metadata de los cambios, autor y correo, fecha de modificación, commit y su mensaje, por cada commit hecho.
```