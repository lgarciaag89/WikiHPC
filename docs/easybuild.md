# Ambiente *module*

### Ambiente *module*

La ejecución de aplicaciones en un ambiente HPC depende de un sin número de herramientas de compilación y ejecución  en la mayoría de los casos con diferencias entre las versiones existentes.  En el cluster pueden existir varias versiones de un mismo compilador, por ejemplo, diferentes versiones de **Python** o **GCC** que a su vez pueden depender de versiones distintas de bibliotecas. 

#### Uso básico de `module`

El cluster tiene instalado un conjunto de paquetes con diferentes versiones que son tratados como módulos. Estos paquetes pueden ser compiladores, interpretes, herramientas bioinformáticas o bibliotecas para enumerar algunos. Todos estos módulos son tratados con el comando `module`. 

Para ver la lista de paquetes disponibles en el cluster utilice el comando `module av`.

Este comando muestra la lista de paquetes que pueden ser cargados en el sistema. Algunos paquetes contienen en sus nombres goolf o gompi. Estos están indicando que esos paquetes tienen dependencias con las versiones de goolf o gompi señaladas. Las dependencias son mostradas después del signo *-*. En la lista de paquetes también se encuentran las versiones disponibles. A la derecha del signo */* se encuentra las versiones de los paquetes que se encuentran y se pueden cargar.

Para mostrar los paquetes que están cargados se uiliza el comando `module list`. 

Un módulo es cargado utilizando el comando `module load nombre_modulo`, donde `nombre_module` es el nombre del módulo que se desea cargar. En el caso de que el módulo tenga diferentes versiones se debe expecificar la versión deseada. Si no se expecifica la versión se carga la versión que ordenada lexicograficamente es la última, que normalmente es la versión más reciente.

Si se termina de utilizar un paquete el comando   `module unload nombre_modulo` ellimina el paquete de la lista de paquetes cargados. Si se desean eliminar todos los paquetes cargados se utiliza el comando `module purge`.  Es una buena práctica utilizar `module purge` en los scripts de ejecución antes de cargar los módulos necesarios. Esto evita un conflicto de de versiones. 

### Enlaces de interes

