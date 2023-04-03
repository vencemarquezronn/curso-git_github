¡Hola Mundo!

Estas son mis notas del curso de Git y GitHub de Plazti. El código en Línea de Comandos aparece en Bash sólo por estética. Los comandos deben ser introducidos línea por línea y los comandos de Windows se declaran o se dejan como notas para correr en powershell.

Estoy redactando las notas y aplicando en el archivo a medida que avanzo.
# Instalación
Se puede instalar git de diferentes maneras, pero mi preferencia es por línea de comandos.
## Windows

```bash
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
touch Archivo.md # En Windows: ni Archivo.md
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
git diff 4d39ff462dd9676c0542e8f3abeb55ab2d8de9de ed2c7cc86a08a4331ff56cccc0c04ef5229f7a2f # <Commit comparado> <Commit a comparar>
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
git checkout <COMMIT> <Archivo> # Permite ver el estado de un archivo en un commit específico
git checkout master <Archivo> # Permite volver al estado del último commit o stage de un archivo
```

# Ramificaciones de un repositorio

Se pueden trabajar cosas aparte de la rama principal "master" si se hacen ramificaciones.

```bash
git branch <Nombre de ramificación> # Se crea una nueva ramificación con otro nombre
git checkout <Nombre de ramificación> # Se cambia a la ramificación deseada
```
Esto nos permite ir avanzando por otras partes, guardar el progreso en diferentes ramas y cambiar entre ramas para notar cómo se ve el cambio. Para fusionar dos ramificaciones se hace un `git merge` desde la rama master.

```bash
git checkout master
git merge <Ramificación a combinar>
```
En caso de haber conflictos, el editor de texto probablemente tiene una forma de arreglarlo.
# Gestión de llaves públicas y privadas
Si se va a colaborar en plataformas como GitHub y GitLab, es necesario crear llaves pública y privada. Esta llave está encriptada y la razón es para proteger el repositorio de ser hackeado o secuestrado. Por mi parte, al usar  GitHub CLI, la configuración ya se ha realizado sin necesidad de que yo intervenga, pero estos son los pasos en caso de que no sea así.

Cualquier sistema operativo puede generar estas llaves:
```bash
ssh-keygen -t rsa -b 4096 -C "tu@email.com" # De esta forma se genera una llave pública y privada para el email que se está utilizando en Git y GitHub/GitLab para registrar el trabajo.
```
Al final, el SO generará una llave pública y una privada, por lo general en el directorio raíz del usuario $HOME:
```bash 
C:\Users\YourUser\.ssh\ {id_rsa, id_rsa.pub} # Así se veria el directorio en Windows
/home/YourUser/.ssh {id_rsa, id_rsa.pub} # Así se vería en Linux y Mac
```
Pero la forma en la que se revisan que las llaves existan y estén funcionando varía del SO:
## Windows y Linux
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
# No se registra la llave pública, sino la privada. JAMÁS SE COMPARTE LA PRIVADA, SINO LA PÚBLICA.
```
## Mac
```bash
eval "$(ssh-agent -s)"
# > Agent pid NUM
cd ~/.ssh
vim config
# Introducir lo siguiente:
# Host *
#     AddKeysToAgent yes
#     UseKeychain yes
#     IdentityFile ~/.ssh/id_rsa
cd ~
ssh-add -K ~/.ssh/id_rsa
```
# GitHub
Por propósitos del curso, se vincula el espacio en GitHub con el repositorio creado en local por medio de las claves creadas anteriormente. Para esto, se agrega en GitHub\Settings\SSH and GPG authentication la clave pública que se generó.

Para agregar el contenido del repositorio a GitHub se debe primero crear el repo en GitHub y después vinvular el repo local con el remoto, para hacer el primer push.

```bash 
git remote add origin https://github.com/tunombredeusuario/elrepocreado.git
# Está agregando en el repositorio local un origen remoto en la URL especificada (esta no existe, es para ser genéricos)
git branch -m main # Se cambia el nombre de la rama de master a main, debido a un cambio de GitHub
git pull origin main --allow-unrelated-histories
# Actualiza el contenido local con el contenido en remoto resolviendo los conflictos en el historial al hacer el merge (git pull = git fetch && git merge)
git push origin main
# Se envía al origen la rama main que se viene trabajando, pero en GitHub 
```
## Manejando etiquetas y versiones
Con las etiquetas y versiones se pueden manejar diferentes puntos en el tiempo que implementan diferentes cosas. Se puede manejar las versiones de el proyecto que se esté manejando.
```bash
git tag -a <Nombre> -m <Mensaje> # Ej.: git tag -a v0.1 -m "La versión alpha 0.1 de estas notas.
git commit -am <Un mensaje> # Se guardan los cambios
git pull origin main # Se traen los cambios que estén en el origen
git push origin main # Se envían los cambios al origen
```
De haber una equivocación, podemos eliminar un tag:
```bash 
git tag # Ver los tags
git tag -d <Etiqueta a eliminar> # Elimina el tag en nuestro entorno local
git push origin :refs/tags/<Tag a eliminar> # Elimina el tag en el origen
```
## Manejando ramificaciones en origen
Una cosa es hacer ramificaciones en el entorno local, pero esos cambios también se deberían ver reflejados en el origen.
```bash
git checkout <Ramificación> # Nos ubicamos en la ramificación
git push origin <Ramificación> # Se manda la ramificación al origen
```
## Colaborando con otros programadores (flujo de trabajo real en git)
Para permitir a otras personas para colaborar en el proyecto, debo agregarlos.

GitHub\Repositorio\Settings\Collaborators >> Se incluye el correo o username del colaborador y así se le enviará un correo para que acepte la invitación y, una vez que acepte, podrá colaborar con el resto de personas, de la forma que hemos definido.
### Combinando ramificaciones de desarrollo a main
Al desarrollar en diferentes ramificaciones por separado diferentes elementos del proyecto, los cambios no se ven reflejados en la rama principal.

Primero se actualizan los cambios en las ramificaciones que se estén trabajando.
```bash
git pull origin <Ramificacion>
```
Segundo, se ubica en la rama principal y se hace el merge con la ramificación a combinar
```bash
git checkout main
git merge <Ramificación a combinar con "main">
```
Si existen conflictos, se solucionan de la misma forma que se había hecho antes y se mandan a origen.

```bash
git pull origin main # Se actualiza la rama
git push origin main # Se envían los cambios a origen
```
## Pull requests
Ahora bien, no todos los cambios deberían verse reflejados en el entorno de producción sino sólo aquellos que sean definitivos, por lo que se utiliza una característica de GitHub llamada pull request.

Al iniciar una nueva ramificación y publicar cambios allí, se puede enviar una Pull Request que es, básicamente, la inicialización de una conversación sobre un cambio que se haya hecho en la ramificación para su revisión, transformación, aprobación y combinación con la rama principal. Una vez pasado por este proceso, es posible eliminar la ramificación pero se sugiere que sea sólo temporal.

Para reflejar el cambio de la eliminación de la rama en el entorno local en que se haya creado, simplemente se actualiza la rama principal.

```bash
git checkout main
git pull origin master
```
## Uso de forks
GitHub permite hacer un fork o una copia del proyecto original para que pueda trabajar en él sin tener que estar en el proyecto (debe estar en público). Se le da al botón `fork` en GitHub y hago un `git clone` en mi disco duro para poder trabajarlo de forma local. Una vez hecho, se hace commit y se envía al origen, pero esto no afecta al proyecto original. Para poder incorporar esos cambios en el proyecto original se hace un pull request y se maneja igual desde el lado de el equipo que maneja el proyecto original/principal.
### Actualizar cambios en origen principal al origen del fork/local
Se puede actualizar el fork con el original con un pull request desde GitHub, pero también es posible hacerlo desde Git en consola.

Para eso, se agrega el origen principal a las fuentes del repo local, se traen esos cambios y se envían a mi origen del fork.
```bash
git remote add upstream <URL del repo original del proyecto>
# Se agrega la fuente del proyecto original . "upstream" es opcional, es una forma de distinguir localmente el repo que trabajo del repo de donde hice el fork.
git pull upstream main
# Se trae los cambios del proyecto original a mi fork
git commit -am "Fusión del repo original a mi fork"
git push origin main
# Se envían las actualizaciones a mi fork
```
# Ignorar archivos con .gitignore
Hay archivos que quizá no se deberían sincronizar con el repositorio en línea, puede ser por preferencias personales (binarios), pero muy a menudo es por cuestiones de seguridad (ids, claves, llaves, entre otras). Para eso, se crea en el directorio raíz del repositorio un archivo `.gitignore`, donde se listan archivos específicos, directorios, conjunto de archivos. Así, se obvian los archivos y directorios indeseados dentro del proyecto.

```bash
*.jpg # Ignora todos los archivos de jpg
directorio # Ignora un directorio
archivo # Ignora un archivo
# Los SO no suelen distinguir entre archivos y directorios a menos que tengan una extensión.
```
# Usando README.md
Es buena práctica tener un archivo README.md que describe el proyecto y cómo funciona. Existe una variedad de editores. VS Code también puede editarlo, pero sólo como un archivo de texto, por lo que también es buena práctica aprender sintaxis de Markdown.
# Otros comandos
```bash
git commit -am "Message" # git add + commit -m
git log --all --graph --decorate --oneline # Permite ver el progreso del proyecto con laas ramificaciones, commit, merges y demás.
git show-ref --tags # Muestra a qué commit se asocia un tag
git show-branch --all # Muestra las ramificaciones con un poco más de detalle
gitk # Muestra en una GUI con el detalle del progreso del proyecto
```
