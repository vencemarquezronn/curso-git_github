¡Hola Mundo!

Estas son mis notas del curso de Git y GitHub de Plazti.

Estoy redactando las notas y aplicando en el archivo a medida que avanzo.

# Instalación

Se puede instalar git de diferentes maneras, pero mi preferencia es por línea de comandos.

## Windows

```powershell
winget install Git.Git
```
Con este comando, se instala git, git bash y una GUI para git.

## Unix

```bash
sudo apt install git # Distros basadas en Debian
sudo dnf install git # Distros basadas en Red Hat
brew install git # Mac [VERIFICAR SI FUNCIONA]
```
Con estos comandos se instala git en el sistema si aún no está instalado. Linux por lo general lo trae por defecto.
# Cambio de metadata del editor

Se pueden cambiar los valores por defecto del autor para trazabilidad de quién está haciendo los cambios.

```bash
git config --global user.name "Tu nombre" # Cambia el nombre del autor en Git
git config --global user.email "tu@email.com" # Cambia el correo electrónico del autor en Git.
```
En mi caso, utilizo la CLI de GitHub, por lo que esta configuración ya se hizo con la info de mi GitHub.
# Creación de un repositorio y primer commit

Una vez creada una carpeta y estando dentro de la carpeta, se puede crear un archivo, modificarlo, y ver quién hizo los cambios.

```bash
mkdir Example
cd Example
touch Archivo.md
code . #Se hacen cambios en VS Code

git init
git status # Muestra el estado de los archivos del repositorio, se agrega el archivo
git add . # Agrega todos los archivos del repositorio
git commit -m "Initial commit" # Hace el primer commit con un mensaje que afirma eso.
git log Archivo.md # Muestra la metadata de los cambios, autor y correo, fecha de modificación, commit y su mensaje, por cada commit hecho.
```

# Analizar los cambios de archivos en un repositorio Git

Se pueden ver los cambios en un archivo.

```bash
git show Archivo.md

# commit 4d39ff462dd9676c0542e8f3abeb55ab2d8de9de (HEAD -> master) <-- Cuál commit es
# Author: Ronald Vence Márquez <68980805+vencemarquezronn@users.noreply.github.com>  <-- quién hizo el cambio  
# Date:   Fri Mar 31 13:10:39 2023 -0500 <-- Cuándo se hizo el cambio

#     Agregada la primera clase, crear repositorio y commits <-- Qué se cambió (git commit -m "TEXT")

# diff --git a/Archivo.md b/Archivo.md
# index a6a75dd..fadce8f 100644
# --- a/Archivo.md <- Primera versión
# +++ b/Archivo.md <- Versión final
# @@ -1 +1,31 @@ <- Cuántos bytes cambiarion
# -¡Hola Mundo! <- El signo "-" al iniciar la línea, indica que se quitó esa línea
# +¡Hola mundo! <- El signo "+" al iniciar la línea, indica que se añadió esa línea
# \ No newline at end of file <- "Enter"
# ...
```

También se pueden ver las diferencias entre archivos.

```bash
git diff 4d39ff462dd9676c0542e8f3abeb55ab2d8de9de ed2c7cc86a08a4331ff56cccc0c04ef5229f7a2f # <Versión comparada> <versión a comparar>
# También compara la versión actual con la versión en staging con `git diff`

# -¡Hola Mundo!
# -
# -Estas son mis notas del curso de Git y GitHub de Plazti.
# -
# -Estoy redactando las notas y aplicando en el archivo a medida que avanzo.
# -
# -# Cambio de metadata del editor
# -
# -Se pueden cambiar los valores por defecto del autor para trazabilidad de quién está haciendo los cambios.
# -
# -```bash
# -git config --global user.name "Tu nombre" # Cambia el nombre del autor en Git
# -git config --global user.email "tu@email.com" # Cambia el correo electrónico del autor en Git.
# -```
# -
# -# Creación de un repositorio y primer commit
# -
# -Una vez creada una carpeta y estando dentro de la carpeta, se puede crear un archivo, modificarlo, y ver quién hizo los cambios.
# -
# -```bash
# -mkdir Example
# -cd Example
# -touch Archivo.txt
# -code . #Se hacen cambios en VS Code
# -
# -git init
# -git status # Muestra el estado de los archivos del repositorio, se agrega el archivo
# -git add . # Agrega todos los archivos del repositorio
# -git commit -m "Initial commit" # Hace el primer commit con un mensaje que afirma eso.
# -git log Archivo.txt # Muestra la metadata de los cambios, autor y correo, fecha de modificación, commit y su mensaje, por cada commit hecho.
# -```
# \ No newline at end of file
# +¡Hola Mundo!
# \ No newline at end of file

```

# Volver en el tiempo en el repositorio (`reset`y `checkout`)

Es posible volver en el tiempo a una versión anterior del repositorio. Se puede buscar una versión con `git log <FILE>`, buscar el commit al que se quiere y regresar a esa versón.

Hay dos tipos de commit, el "duro" y el "suave".

```bash
git reset <COMMIT> --hard # TODO vuelve a ese estado, es el más común
git reset <COMMIT> --soft # Todo vuelve a ese estado EXCEPTO lo que esté en staging
```

No obstante, estas formas son peligrosas ya que pueden hacer que se pierda progreso, por lo que es mejor hacer `git checkout`.

```bash
git checkout <COMMIT> <file.filetype> # Permite ver el estado de un archivo en un commit específico
git checkout master <file.filetype> # Permite volver al estado del último commit o stage de un archivo
```

# Ramificaciones de un repositorio

Se pueden trabajar cosas aparte de la rama principal "master" si se hacen ramificaciones.

```bash
git branch <branchname> # Se crea una nueva ramificación con otro nombre
git checkout <branchname> # Se cambia a la ramificación deseada
```
Esto nos permite ir avanzando por otras partes, guardar el progreso en diferentes ramas y cambiar entre ramas para notar cómo se ve el cambio.

# Otros comandos

```bash
git commit -am "Message" # git add + commit -m
```