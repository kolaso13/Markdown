# CMD:
code . : arranca VSC del directorio donde estamos 

rd /s/q directorio: es para borrar un directorio en cmd


## GIT:
git version

git init: para inicializar git

git status -s: para saber que archivos no tienen seguimientos

git add . : añadimos todos los archivos al área temporal. Si quieres añadir solo un archivo quitamos el “.” y añadimos el nombre del archivo.

git commit -m “el mensaje”: para mandarlo al siguiente nivel y guardar su momento exacto (como una foto) con un mensaje.

git log --oneline : sirve para ver los identificadores de los commit

git reset --hard (identificador) : sirve para viajar a ese archivo guardado según su identificador

git push : sirve para subir a github archivos

### dos maneras:
git remote add origin https://github.com/kolaso13/Markdown

git remote add origin git@github.com/kolaso13/git-ejemplo.git 
  
esto sirve para añadir el repositorio donde guardar los archivos en github.


## GITHUB:
creamos un repositorio


git clone https://github.com/kolaso13/Markdown

## RAMAS:
git branch "nombre": sirve para crear una rama
git checkout "nombre": se usa para cambiar entre ramas
git merge "nombre": se usa para juntar los datos de las ramas



## Crear
git init

echo “hola mundo” > leeme.txt

echo “hola mundo2” > leeme2.txt

echo “# titulo” > leeme.md

git status -s

git add *.txt

git commit -m “añadimos los archivos .txt”

git status -s

type nombredearchivo