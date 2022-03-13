# IAW-PRACTICA-MKDOCS
Álvaro Alejandro Fababú López  
Creación de páginas con MKDOCS  
2º ASIR - IES Celia Viñas
#
### MkDocs es una herramienta que permite generar sitios web estáticos . El contenido de las páginas está escrito en formato Markdown, y la configuración del sitio se hace a través de un fichero en formato YAML.
*** 
## Creación del proyecto
En primer lugar tendremos que situarnos sobre el directorio donde queramos crear el proyecto. Una vez allí crearemos la estructura de archivos de MkDocs haciendo uso del comando
~~~
docker run --rm -it -p 8000:8000 -v "$PWD":/docs squidfunk/mkdocs-material new .
~~~
Este comando crea el directorio docs dentro del directorio del proyecto con el archivo index.md que corresponde con la página por defecto, y el archivo de configuración mkdocs.yml 
~~~
└── proyecto
    ├── docs
    │   └── index.md
    └── mkdocs.yml
~~~
Las páginas que vayamos creando deberán estar descritas en Markdown y situarse dentro del directorio docs. En mi caso el contenido del directorio del proyecto quedaría así.
~~~
.
└── proyecto
    ├── docs
    │   ├── index.md
    │   ├── about.md
    │   ├── practicas.md
    │   └── deprueba.md
    └── mkdocs.yml
~~~
***
## Archivo mkdocs.yml
Como he mencionado antes, este archivo se encuentra en el raíz del directorio del proyecto y contiene la configuración de nuestro sitio. Su contenido inicial es similar a este
~~~
site_name: IAW

nav:
    - Principal: index.md
    - Acerca de: about.md

theme: material
~~~
La directiva *site_name* indica el nombre del sitio, la directiva *nav* contiene las páginas que aparecerán en el menú de navegación, y la directiva *theme* el tema que utilizará la página.  
En primer lugar tenemos que añadir las páginas que hemos creado a la barra de navegación.
~~~
nav:
  - Principal: index.md
  - Acerca de: about.md
  - Practicas: practicas.md
  - Pruebas: deprueba.md
~~~
Las modificaciones que realicemos sobre la configuración inicial del tema las añadiremos dentro de la directiva *theme*
~~~
theme:
  name: material
  language: es
  palette:
    primary: lime    
    accent: cyan
  font:
    text: roboto
  features:
    - header.autohide
  logo: images/panda.jpeg
~~~
En este caso hemos seleccionado el idioma español como el idioma base del site, hemos configurado la paleta del colores para que el banner del header aparezca en color lima y que los enlaces cambien a color cyan cuando coloquemos el cursor encima. También hemos seleccionado roboto como la fuente principal del site, hemos configurado el header para que ocultarlo al hacer scroll por la página, y hemos cambiado el logo por defecto por una imágen que hemos guardado en el directorio images que cuelga del raíz del proyecto.  
Si queremos vincular el proyecto con el sitio web de GitHub Pages solamente tendremos que ejecutar el siguiente comando (desde la raíz del directorio del proyecto):
~~~
docker run --rm -it -v ~/.ssh:/root/.ssh -v "$PWD":/docs squidfunk/mkdocs-material gh-deploy
~~~
