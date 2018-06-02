# Ambiente *module* y paquete *EasyBuild*

### Ambiente *module*

La ejecución de aplicaciones en un ambiente HPC depende de un sin número de herramientas de compilación y ejecución  en la mayoría de los casos con diferencias entre las versiones existentes.  En el cluster pueden existir varias versiones de un mismo compilador, por ejemplo, diferentes versiones de **Python** o **GCC** que a su vez pueden depender de versiones distintas de bibliotecas. 

#### Uso básico de `module`

El cluster tiene instalado un conjunto de paquetes con diferentes versiones que son tratados como módulos. Estos paquetes pueden ser compiladores, interpretes, herramientas bioinformáticas o bibliotecas para enumerar algunos. Todos estos módulos son tratados con el comando `module`. 

Para ver la lista de paquetes disponibles en el cluster utilice el comando `module av`.


``` bash
-----/opt/ohpc/pub/moduledeps/gnu-openmpi----
   scalapack/2.0.2

---- /opt/ohpc/pub/moduledeps/gnu ----
   numpy/1.11.1    
   openblas/0.2.19    
   openmpi/1.10.6 (L)

---- /opt/ohpc/pub/modulefiles ----
   EasyBuild/3.4.1        
   cmake/3.9.2        
   gnu7/7.2.0      
   llvm4/4.0.1        
   pmix/1.2.3        
   valgrind/3.13.0
   autotools       (L)    
   gnu/5.4.0   (L)    
   hwloc/1.11.8    ohpc        (L)    
   prun/1.2   (L)

  Where:
   L:  Module is loaded

Use "module spider" to find all possible modules.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".
```

Este comando muestra la lista de paquetes que pueden ser cargados en el sistema. Algunos paquetes contienen en sus nombres goolf o gompi. Estos están indicando que esos paquetes tienen dependencias con las versiones de goolf o gompi señaladas. Las dependencias son mostradas después del signo *-*. En la lista de paquetes también se encuentran las versiones disponibles. A la derecha del signo */* se encuentra las versiones de los paquetes que se encuentran y se pueden cargar.

Para mostrar los paquetes que están cargados se uiliza el comando `module list`. 

``` bash
module list 

Currently Loaded Modules:
  1) autotools   2) prun/1.2   3) gnu/5.4.0   4) openmpi/1.10.6   5) ohpc
```

Un módulo es cargado utilizando el comando `module load nombre_modulo`, donde `nombre_module` es el nombre del módulo que se desea cargar. 

``` bash
module load Beast/1.8.4
module list

Currently Loaded Modules:
  1) autotools   
  2) prun/1.2   
  3) gnu/5.4.0   
  4) openmpi/1.10.6   
  5) ohpc   
  6) EasyBuild/3.4.1   
  7) Java/1.8.0_144   
  8) Beast/1.8.4
```

En el caso de que el módulo tenga diferentes versiones se debe especificar la versión deseada. Si no se especifica la versión se carga la versión que ordenada lexicograficamente es la última, que normalmente es la versión más reciente.

Si se termina de utilizar un paquete el comando   `module unload nombre_modulo` elimina el paquete de la lista de paquetes cargados. Si se desean eliminar todos los paquetes cargados se utiliza el comando `module purge`.  Es una buena práctica utilizar `module purge` en los scripts de ejecución antes de cargar los módulos necesarios. Esto evita un conflicto de de versiones. 

### Paquete EasyBuild

Según la [documentación oficial](https://easybuild.readthedocs.io/en/latest/index.html) `EasyBuild` es un *framework* para la compilación e instalación de aplicaciones y sus dependencias en sistemas HPC de manera eficiente.

El comando básico es `eb` y para decirle a `EasyBuild` que aplicación utilizar se puede hacer de dos maneras:

1. Mediante un archivo de configuración *easyconfig*.
2. Mediante linea de comandos.( Solo se va a explicar la primera ) 

La manera más sencilla es definir un fichero de configuración donde se definen los pasos y las direcciones de los fuentes que se desean instalar. `eb easyconfig` busca los códigos fuentes  desde una ubicación local o lo descarga desde uns dirección remota y  ejecuta los pasos que se especifiquen en el fichero `easyconfig`. 

```
 eb Beast-1.8.4.eb --robot
```
Si es necesario instalar dependencias existe la opción `--robot` que busca primero las dependencias y luego procesa la aplicación objetivo. 

Luego de  instalar la aplicación esta podrá ser tratada por el paquete `module`.

En el [proyecto de easyBuild en GitHub](https://github.com/easybuilders/easybuild-easyconfigs/tree/master/easybuild/easyconfigs) hay un conjunto de ficheros easyconfig para la mayoría de las aplicaciones que se ejecutan hoy en ambientes HPC.

### Enlaces de interés

* [Documentación EasyBuild](https://easybuild.readthedocs.io/en/latest/)
* [man Module](http://modules.sourceforge.net/man/module.html)
* [Documentación module](http://modules.readthedocs.io/en/latest/index.html)

