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
+ Untraked: Cualquier otro archivo en tu directorio de trabajo que no estaba en tu última instantánea y que no está en el área de preparación.

>[!TIP]
>Básicamente, la diferencia entre los untracked y los tracked es que Git ignora los untracked, pero con los tracked si que tiene en cuenta su estado y versiones. 

![image](https://github.com/13sauca13/Git/assets/33026257/962531e7-3a89-420f-8c8b-190e8b68d57d)

Podemos comprobar el estado de los archivos con  el comando ```git status```

Más adelante veremos en detalle acerca de los estados de archivos y su relación con los estados del repositorio.

### Ramificaciones
Git es un sistema que sirve para el control de versiones. Cuando hablamos de ramificaciones, significa que tomamos la rama principal de desarrollo (***master***) y a partir de ahí continuamos trabajando sin seguir esta rama principal de desarrollo.

En cada confirmación de cambios (***commit***), Git almacena una instantánea, esta instantánea contiene además unos metadatos con el autor, un mensaje, y uno o varios apuntadores a las confirmaciones que sean padres directos de esta (un padre en los casos de confirmación normal, y múltiples padres en los casos de estar confirmando una fusión (***merge***) de dos o más ramas).

Una rama Git es simplemente un apuntador móvil apuntando a una de esas confirmaciones. La rama por defecto de Git es la rama ***master***. Con la primera confirmación de cambios que hacemos, se creará esta rama principal master apuntando a dicha confirmación. En cada confirmación de cambios que realicemos, la rama irá avanzando.

Podemos crear nuevas ramas desde el punto en el que estamos con el comando:
```git
git branch <nombre_rama>
```
Esto creará una rama que apunta donde está ahora mismo la rama en la que estábamos. Sólo creamos la rama, ahora tenemos que ponernos en ella para que nuestros commit sean ahí y no el rama actual, esto es mediante el apuntador ***HEAD***, que indica la rama local en la que estamos en cada momento. Para mover este HEAD de rama se utiliza el ```checkout```:
```git
git checkout <nombre_rama>
```
(también podemos usar ```git switch <nombre_rama>```, en nuestro caso es lo mismo, aunque ```checkout``` es más versátil para otras ocasiones)

Así movemos el HEAD a la rama que indiquemos.

Podemos ver las ramas y donde tenemos el HEAD con el comando ```git branch```

![image](https://github.com/user-attachments/assets/df6b68d3-671c-454e-9417-56f94530ce1b)

![image](https://github.com/user-attachments/assets/87fc834b-bbed-414a-be7b-1a8ab9db3d54)

Cuando movemos el HEAD todos los archivos del repositorio local cambian a como están (o estaban) el la instantánea de la rama a la que acabamos de ir.

Una vez hayamos trabajado en un branch y queramos incorporar los cambios a otro para unir ambas ramas (lo más habitual es tener un branch con una línea de desarrollo y cuando esta esté lista, traer los cambios a la rama main), pondremos el HEAD en la rama a la que queremos incorporar los cambios y luego haremos un ***merge***:
```git
git merge -m "Aqui va el comentario igual que en los commit" <rama_a_incorporar>
```

![image](https://github.com/user-attachments/assets/9a790036-0578-42dd-856d-8c2401ab6cdf)

Ahora ambos branches siguen existiendo, pero todo lo que cambió en testing con respecto a main está modificado en main también (no así los cambios de main, que no se pasaron a testing), ahí está una de as fortalezas de git, dos personas pueden trabajar en diferentes partes de un  proyecto usando distintas ramas, y el trabajo de cada uno, una vez aprobado, se pasa a main (o la que sea la rama principal del proyecto), pero los cambios de terceros no afectan a mi rama incluso aunque hayan hecho todos merge a main.

>[!TIP]
>Si un mismo fichero cambió en ambas ramas a unir saltará un "merge conflict" y se cargarán en el fichero las dos versiones, hay que entrar al fichero que causa el conflicto y editar a mano borrando lo no deseado.
>
>Una vez hacho eso se realiza un commit normal

Una vez hecho un merge, si no hiciese falta ya ese branch o si simplemente queremos borrarlo:
```git
git branch -d <nombre_rama>
```

## Usando Git
Hay que tener claro el estado de los archivos para entender esta parte, cuando queramos "guardar nuestro trabajo", lo que vamos a hacer es una confirmación de cambios, un ***commit***, pero para esto los archivos tienen que estar en el área de preparación, en ***staging***, ya sean tracked modificados o untracked. Ejecutando el comando ```git status``` vemos como está el repositorio y sus archivos.

![image](https://github.com/user-attachments/assets/b15b7ee5-a885-4ddf-bf77-b32e53deffec)

Podemos ver que tengo dos archivos untracked, para que se incluya en el próximo commit tenemos que "rastrearlo", pasarlo a tracked, de lo contrario aunque hagamos un commit no se incluirán (para evitar incluir archivos por error). Para hacer esto se usa el comando ```git add```

![image](https://github.com/user-attachments/assets/2d617485-cc31-451d-9f92-d2ecdc65d711)

Si modificamos un archivo aun después de hacer el ```git add``` tendremos que volver a hacerlo para incluir estos cambios al commit tal y como nos avisa el sistema al hacer el ```git status```

Para añadir todos los archivos se usa ```git add --all```

![image](https://github.com/user-attachments/assets/346622d1-d43d-437c-a2c9-d1f4b658c94c)

Ahora que el área de staging está como queremos podemos confirmar los cambios:
```git
git commit
```
Automáticamente se abrirá el editor que configuramos con el ```git config```, en nuestro caso el Visual Studio Code, y nos pedirá el mensaje de la confirmación de cambios (una explicación sobre lo que hicimos o cambiamos), en cuanto guardemos el archivo podemos cerrarlo y el commit estará hecho

![image](https://github.com/user-attachments/assets/b45b75c9-5b02-4ed5-9a47-e19144671087)

Un atajo sería usar el siguiente comando para saltarnos el paso del editor y hacer el commit con el comentario en la propia línea de comando:
```git
git commit -m "Aqui entre comillas va el comentario"
```

Para ver un histórico de los commits realizados se utiliza el comando ```git log```. Si queremos información detallada incluyendo el comentario obligatorio de cada commit usaremos
```git
git log --oneline
```
### Eliminar archivos
Para eliminar un archivo basta con ejecutar el comando:
```git
git rm <nombre_archivo>
```
En el próximo commit el archivo será eliminado del repositorio local y de la rama
### Renombrar archivos
Para renombrar un archivo se usa el comando:
```git
git mv <nombre_original> <nombre_nuevo>
```
Este comando también será efectivo en el próximo commit

### Volver a un commit anterior
Puede que queramos volver a una versión antigua de nuestro código. Lo primero que tendríamos que hacer es revisar el apuntador del commit (con ```git log --oneline```) y luego ejecutar:
```git
git reset <codigo_commit>
```


## Trabajar en remoto
Hasta ahora todo fue con un repositorio local, que es útil para llevar un control de cambios e incluso volver atrás si fuese necesario, pero lo realmente útil es la posibilidad de trabajar con repositorios remotos y de manera simultánea y colaborativa.

Los repositorios remotos son versiones del proyecto que están hospedadas en Internet o en cualquier otra red. Podemos tener varios de ellos, y en cada uno tendremos generalmente permisos de solo lectura o de lectura y escritura. Colaborar con otras personas implica gestionar estos repositorios remotos enviando y trayendo datos de ellos cada vez que necesitemos compartir trabajo.

Para añadir un repositorio remoto se utiliza el siguiente comando:
```git
git remote add <nombre> <url>
```
Podemos consultar los remotos que tenemos configurados ejecutando ```git remote```. Si queremos más detalles sobre algún remoto concreto podemos utilizar ```git remote show <nombre>```

![image](https://github.com/user-attachments/assets/f7bb46d1-19c1-48b2-86a1-b07f575b3910)

Ahora tenemos los remotos configurados (podemos tener todos los que queramos) y ya no es necesario usar la URL entera, podemos usar el nombre que acabamos de darle para todos los comando que vienen en adelante.

