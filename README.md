# Git
Pruebas y apuntes de GIT

---
## Introducción
### Qué es Git?
Git es un sistema de control de versiones distribuido que permite a los programadores rastrear y administrar los cambios en su código fuente. Te proporciona una forma de guardar y documentar todas las modificaciones realizadas en tus archivos, lo que facilita la colaboración con otros desarrolladores y te ayuda a mantener un historial completo de tu proyecto.

Una de las principales ventajas de Git es su enfoque distribuido, lo que significa que todos los desarrolladores tienen una copia local completa del repositorio. Esto permite trabajar de manera independiente, sin depender de una conexión a Internet o un servidor.

### Instalar Git
Para utilizar Git hay que tenerlo instalado en sistema. Lo rpimero es acceder al sitio web oficial de [Git](https://git-scm.com/) y descargarlo para nuestro SO.

![image](https://github.com/13sauca13/Git/assets/33026257/935355e9-8184-4747-907e-e75de9a6e9f0)

Una vez descargado lo instalamos; no hay ociones, sólo instalamos y listo, ahora veremos como funciona.

## Configurar Git
Lo primero será configurar tres parámetros con ```git config``` para establecer el funcionamiento de Git. Estos 
```git
git config --global user.name "MiNombre"
git config --global user.email mimail@mail.com
git config --global core.editor "code --wait"
```
De esta manera configuramos en los dos primeros comandos nuestro nombre y mail para que quede registrado en los cambios que hagamos y con el tercero establecemos el editor de texto por defecto para Git, en este caso Visual Studio Code.

Podemos comprobar la configuración usando el comando ```git config --list```

>[!TIP]
>Podemos obtener ayuda en cualquier momento o sobre cualquier comando usando ```got --help``` o ```git <comando> --help```

## Los repositorios
Un repositorio es el lugar donde está el proyecto y todos sus archivos, como si fuese la carpeta raiz donde puede habar más carpetas y/o todos los tipos de archivos que queramos. Lo primero es navegar desde la linea de comandos hast ala ubicación donde queremos el repositorio en local, y ahora tenemos dos posibilidades:
+ Iniciar un nuevo repositorio: ```git init <nombre_repositorio_local>```
+ Clonar un repositorio existente: ```git clone <url_repo_original> <nombre_repositorio_local>``` (Esto descarga toda la información de ese repositorio y saca una copia de trabajo de la última versión.)

En ambos casos se creará una carpeta llamada "nombre_repositorio_local" y en su interior estará nuestro repositorio.

### Sobre los archivos y su estado en Git
Ahora toca hablar sobre como funciona Git para todo lo que viene por delante. En un repositorio los archivos pueden tener dos estados:
+ Tracked: Son todos aquellos archivos que estaban en la última instantánea del proyecto; pueden ser archivos sin modificar, modificados o preparados.
+ Untraked: Cualquier otro archivo en tu directorio de trabajo que no estaba en tu última instantánea y que no está en el área de preparación

![image](https://github.com/13sauca13/Git/assets/33026257/962531e7-3a89-420f-8c8b-190e8b68d57d)

Podemos comprobar el estado de los archivos con  el comando ```git status```

Más adelante veremos en detalle acerca de los estados de archivos y su relación con los estados del repositorio.

### Ramificaciones
Git es un sistema que sirve para el control de versiones. Cuando hablamos de ramificaciones, significa que tú has tomado la rama principal de desarrollo (***master***) y a partir de ahí has continuado trabajando sin seguir la rama principal de desarrollo.

En cada confirmación de cambios (***commit***), Git almacena una instantánea del trabajo preparado. Dicha instantánea contiene además unos metadatos con el autor y el mensaje explicativo, y uno o varios apuntadores a las confirmaciones que sean padres directos de esta (un padre en los casos de confirmación normal, y múltiples padres en los casos de estar confirmando una fusión (***merge***) de dos o más ramas).

Una rama Git es simplemente un apuntador móvil apuntando a una de esas confirmaciones. La rama por defecto de Git es la rama master. Con la primera confirmación de cambios que realicemos, se creará esta rama principal master apuntando a dicha confirmación. En cada confirmación de cambios que realicemos, la rama irá avanzando automáticamente.
