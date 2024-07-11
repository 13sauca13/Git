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
Lo primero será configurar tres parámetros con ```git config``` para establecer el funcionamiento de Git:
``` git
git config --global user.name "MiNombre"
git config --global user.email mimail@mail.com
git config --global core.editor "code --wait"
```
De esta manera configuramos en los dos primeros comandos nuestro nombre y mail para que quede registrado en los cambios que hagamos y con el tercero establecemos el editor de texto por defecto para Git, en este caso Visual Studio Code.
