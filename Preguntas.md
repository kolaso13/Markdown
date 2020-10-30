### 1- Pregunta: ¿Hay alguna manera de deshacer el mismo manteniendo esos cambios en mi copia local para volver a commitearlos correctamente?

### 1- Respuesta:
Si quieres mantener los cambios:

git reset [--mixed] HEAD~1
Si además no quieres cargarte el commit (sólo mover el head al anterior):

git reset --soft HEAD~1
Y si no quieres mantenerlos (y volver al estado del commit anterior, en la práctica, destruir el último commit completamente como si nunca hubiera existido):

git reset --hard HEAD~1

### 2- Pregunta: ¿Cuáles son específicamente las diferencias entre hacer un git pull y un git fetch?

### 2- Respuesta:
De la documentación:

git pull is shorthand for git fetch followed by git merge FETCH_HEAD.

o haciendo una traducción libre:

git pull es una abreviación de git fetch seguido de git merge FETCH_HEAD.

Es decir, git fetch trae los cambios, pero los deja en otro branch, hasta que se hace el git merge para traerlos al branch local.

### 3- Preguntas:  ¿cuál es la diferencia entre git rebase y git merge?

### 3- Respuesta: 
Resumen para lectores ávidos de conocimiento rápido: con git rebase tendrás un historial más claro, por lo que suele ser la opción preferida.

Cuando haces git rebase:

- los commits locales se eliminan de la rama temporalmente.
- se ejecuta un git pull.
- los commits locales se insertan nuevamente.

Esto quiere decir que todos tus commits locales aparecen al final, después de los commits remotos. Esto es, si haces git log, los commits de la rama que has rebasado aparecen como si fueran más antiguos, independientemente de cuándo se hicieran.

### 4- Pregunta: Dado que no he hecho commit ¿cómo quito archivoQueNoQuieroCommitear.js del commit?

### 4- Respuesta: 
Debes removerlos del index con:

git reset <paths>
Tomado de la documentación:

git reset [-q] [<tree-ish>] [--] <paths>…​

Esta forma restablece las entradas del "index" para todos los <paths> a su correspondiente estado en <tree-ish> (Esto no affecta el "working tree" ni el "branch" actual).

Esto quiere decir que git reset <paths> es lo opuesto a git add <paths>


### 5- Pregunta: ¿Cómo puedo traer los cambios del remoto?

### 5- Respuesta:
El primer paso es recibir todos los commits que están en el remoto, para eso hacé

git fetch
Asumo que estamos hablando de master. Si no, reemplazá master por el nombre de la branch con la que estés trabajando.

# Reset
Para apuntar las branches locales al mismo commit que está en el remoto, tenés que usar git reset.

# Si no te importa perder tus cambios locales:
git reset origin/master --hard
Esto va a deshacer todos tus cambios y traer lo mismo que está en el remoto. A partir de ahora, git push y git pull van a funcionar como siempre.

# Si querés mantener tus cambios locales:
En vez de un hard reset, hacé un soft reset

git reset origin/master --soft
Se pueden aplicar tus commits locales arriba de lo que está en el remoto usando git rebase

git rebase -i origin/master
Esto va a ejecutar un rebase en modo interactivo, donde podés elegir cómo aplicar tus commits locales que no están en el remoto arriba del HEAD actual.

Si los cambios en la historia borraron algún commit que vos tenés local, van a aparecer como commits pendientes de aplicar de vuelta. Si no querés que se apliquen, vas a tener que borrarlos como parte del rebase.

Usá git command --help para más detalles y ejemplos de cómo aplicar cualquiera de estos comandos.

### 6- Pregunta: ¿Existe alguna manera de hacer un pull request de commits que no contenga los últimos commits que he realizado en mi repositorio?

### 6- Respuesta:
puedes usar rebase:

git checkout master 
git pull
git checkout <branch>
git rebase master
Así tendrás tu branch arriba del master actual.

O si quieres usar solo algunos ciertos comits, puedes hacer una copia de master, y después cherry-pick de tu branch, solo los comits que quieres en tu pull request.

git checkout master
git pull
git checkout -b branch_nuevo
git cherry-pick <revisión 1> <revisión 2> ... <revisión N>
Así tendrás un branch nuevo con sólo los comits que quieres, y lo puedes usar como normal en GitHub.

### 7- Pregunta: Cual es la diferencia entre --force y --force-with-lease en git?

### 7- Respuesta:
Git push --force es destructiva porque incondicionalmente sobrescribe el repositorio remoto con lo que tenga a nivel local, posiblemente sobrescribir cualquier cambio que un miembro del equipo ha empujado, lo cual puedes borrar los cambios de algún miembro. Sin embargo hay una manera mejor la opción --force-with-lease la cual es la mejor recomendada puede ayudar cuando se necesita hacer un empuje forzado pero todavía asegurarse de no sobrescribir el trabajo de otros.

### 8- Pregunta: Agregar usuarios a un proyecto Git

### 8- Respuesta:

Debes de dirigirte a <u>Settings -> User and group access -> Users y agrega el usuario por su correo.</u> Recuerda que el usuario debe de estar registrado en bitbucket para que te aparezca en la lista.

Aqui una imagen para que te puedas guiar:
![Imagen1](https://i.stack.imgur.com/ttMMN.png)

Tambien comprueba que la url del repositorio no contenga tu usuario. Ejecuta el siguiente comando:

git remote -v
Si en la url aparece tu usuario entonces tienes que editar y cambiarlo por el usuario que va utilizar el repositorio. Eso se hace con el siguiente comando:

git remote set-url origin  https://<nombre_de_tu_cuenta>@bitbucket.org/<la_nueva_cuenta>/<nombre_repositorio>

### 9- Pregunta: ¿En que momento debo realizar un commit en git?

### 9- Respuesta: 
De forma general y no específicamente en Git siempre es recomendable hacer commits seguidos para tener tus cambios versionados y disponibles en el control de código fuente.

De manera específica en Git y respondiendo la pregunta específica que has formulado:

Suponiendo lo siguiente:

Tienes una tarea asignada cuya especificación es crear una barra de navegación
Estas trabajando en un topic branch (también llamado feature branch)
Mi recomendación es la siguiente:

- Si te sientes a gusto y confiado en que puedes entregar los cambios correspondientes a toda la especificación sin problemas ya que la tarea no es muy compleja, <u>entonces bastará con un solo commit.</u>
- Si la tarea es demasiado compleja, <u>te recomendaría proponer dividir la tarea en varias subtareas de modo que puedas asociar cada paso particular de la construcción de por ejemplo la barra de navegación a un commit específico.</u>

Al final lo mas importante que debes recordar es lo que menciona @Kristian Damian en su respuesta: Básicamente que cada checkin debe contener cambios que funcionalmente estén completos sin que rompa el código, unit test o proceso de build que tengas establecido.

El resto puede ser muy subjetivo y depende de cada caso y cada persona

### 10- Pregunta: ¿Cómo obtener el nombre del autor de un repositorio GIT?

### 10- Respuestas:
He revisado la documentación oficial y lo he logrado usando:

git show --format=format:"Autor: %an" --no-patch
Donde --format me permite definir el formato y la información del repositorio que quiero mostrar, en este caso uso %an que significa author name, y con --no-patch elimino la salida diff
