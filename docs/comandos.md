# Ejecución de tareas

El cluster cuenta con [slurm](https://slurm.schedmd.com/) como planificador de tareas.  El usuario tendrá la oportunidad de ejecutar sus tareas en las diferentes colas de ejecución, en dependencia del tiempo y los recursos necesarios para ejecutar la tarea.

#### Introducción

Las tareas en el cluster serán atendidas por slurm. Para poder ejecutar una tarea normalmente un usuario debe preparar un script de ejecución donde define la aplicación que desea ejecutar, los juegos de entrada, la forma en que obtendrá la salida y los recursos que necesita para ejecutar la aplicación. Se podrá definir también si desea ser notificado vía email cuando el estado de sus tareas cambien. Cuando el script esté definido se le entrega a slurm para que este se encargue de ejecutarlo.


### Commandos básicos

* `scontrol` - Herramienta par administrar, ver y modificar configuraciones.
* `sinfo` - Muestra información general acerca del sistema de colas.
* `squeue` - Muestra información detallada de las tareas en las colas.
* `scancel` - Cancela una tarea de ejecución.
* `sbatch ` - Ubica el script de ejecución en la cola definida en el fichero de ejecución, si no se define una cola slurm ubica la tarea en la cola por defecto.
* `srun ` - Ejecuta una tarea paralela, de ser necesario crea antes de ejecutar la tarea,  un espacio con los recursos definidos.


### Definir script de ejecución

Un script de ejecución describe todo lo necesario para ejecutar una tarea(aplicación,datos de entrada, forma de salida, recursos necesarios, etc  ). El caso simple es cuando la ejecución de las tareas necesita solo un nodo de ejecución. 

Poniendo como caso de ejemplo una aplicación que tenga los siguientes requerimientos:

- Ejecutarse en un solo nodo,
- No se ejecutará mas de 10 minutos,
- Se identificará como "miapp1",
- Se quiere ser notificado cada vez que la ejecución cambie de estado.

Suponiendo que el código que se desea ejecutar se llama *miapp*, el siguiente script definiría todos los requerimientos listados arriba y mandaría a ejecutar *miapp*.

``` bash
#!/bin/bash

# definir número de nodos
#SBATCH --nodes=1

# establecer el tiempo máximo que se desea ejecutar la aplicación
#SBATCH --time=00:10:00

# definir el nombre de la ejecución
#SBATCH --job-name=miapp1

# establecer ser notificado cada vez que la ejecución cambie de estado
#SBATCH --mail-type=ALL

# definir a cual dirección de correo deben llegar las notificaciones
#SBATCH --mail-user=john.smith@uci.cu

# mandar a ejecutar la aplicación
miapp
```
El script comienza con ``` #!/bin/bash``` , que indica que el script es script bash de linux.

Después de definir el *shebang* siguen un conjunto de lineas iniciadas con *#SBATCH*, directivas slurm para definir los recursos computacionales y las configuraciones generales de la ejecución tales como nombre, etc. Las directivas  ```#SBATCH``` deben ser ubicadas al inicio de la ejecución antes cualquier otro comando, las directivas definidas después de algún comando son ignoradas. 

#### Definir la cantidad de nodos 

La directiva ```#SBATCH --nodes=1``` determina la cantidad de nodos necesarios para la ejecución, para el ejemplo solo se solicitó un nodo. La cantidad de nodos que se soliciten es un tema importante, si se solicitan más nodos de los que realmente se empleen en la ejecución, los nodos que no se empleen estarán reservados para la ejecución pero no se estarán utilizando.

#### Definir el tiempo máximo de ejecución 

La directiva ```#SBATCH --time=00:10:00``` especifica el tiempo máximo que la aplicación estará ejecutándose, este tiempo no tiene en cuenta el tiempo que la tarea estará en estado de espera en la cola de ejecución. El formato del tiempo estará definido por h:m:s y se espera que la ejecución termine antes de vencerse el tiempo máximo. Cuando el tiempo máximo es alcanzado slurm termina la tarea sin importar el estado de la ejecución.   

#### Definir el nombre de la ejecución

La directiva ```#SBATCH --job-name=miapp1``` define el nombre de la tarea

#### Notificaciones 

Si la directiva ```#SBATCH --mail-user=john.smith@uci.cu``` es especificada un correo de notificación es enviado a la dirección solicitada. Para definir en que momento se desea recibir notificaciones se define la directiva ```#SBATCH --mail-type=<type>```, donde <type> puede ser  ***BEGIN***, ***END***, ***FAIL***, ***REQUEUE*** o ***ALL*** (para cualquier cambio del estado).

Por último se especifica las operaciones que se desean ejecutar utilizando comandos linux. La tarea se inicia en la carpeta desde la cual fue enviada a slurm, pero esto puede ser cambiado desde el script, al igual que desde el script se pueden modificar, crear  o eliminar   variables de entorno, así como definir los módulos que se desean utilizar.

#### Definir el número de procesos por nodo.

Si se desea ejecutar la aplicación de manera concurrente en más de un nodo y utilizando varios procesos se puede definir la cantidad de tareas que se desean ejecutar por nodos utilizando la directiva ```#SBATCH --ntasks-per-node=n```, donde n es un número entero. 

#### Ejemplo de ejecución en multiples nodos

Se dese ejecutar una aplicación utilizando 32 procesadores, en un conjunto de nodos que tienen 16 procesadores cada 1 con los siguientes requerimientos:

- Ejecutar sobre 32 procesadores,
- No se ejecutará mas de 100 horas,
- Se identificará como "miapp2",
- Se quiere ser notificado cada vez que la ejecución cambie de estado,
- Tiene dependencia de mpi.

``` bash
#!/bin/bash

# definir número de nodos
#SBATCH --nodes=1

# Definir el numero de tareas(procesos) a ejecutar en cada nodo.
#SBATCH --ntasks-per-node=16


# establecer el tiempo máximo que se desea ejecutar la aplicación
#SBATCH --time=100:00:00

# definir el nombre de la ejecución
#SBATCH --job-name=miapp2

# establecer ser notificado cada vez que la ejecución cambie de estado
#SBATCH --mail-type=ALL

# definir a cual dirección de correo deben llegar las notificaciones
#SBATCH --mail-user=john.smith@uci.cu

# mandar a ejecutar la aplicación
mpirun $MPI_HOSTS miaap2
```

### Ejecutar un script slurm

Definido el script de ejecución, se enviará a slurm utilizando el comando ```sbatch script_name``` . El sistema de colas devuelve un número de identificación de la tarea en la cola y devuelve el control a la terminal de linux. Por defecto slurm crea ficheros de ejecución donde se van mostrando los mensajes enviados a la salida estándar del sistema. Una vez se envié el trabajo estará en estado pendiente hasta que los recursos necesarios para la ejecución estén disponibles y se cumplan las reglas de prioridad definidas. 

### Monitorear el estado de las ejecuciones

Con el comando ```squeue``` se  puede ver el estado de la ejecución. El comando ```squeue``` muestra la lista de tareas actuales en el estado en el que se encuentran.


             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
               173    normal execClus   user99 PD       0:00      3 (Resources)


La primera columna muestra el identificador de la tarea,  la segunda columna muestra la cola o partición  donde se está ejecutando la tarea, la tercera columna muestra el  nombre que se especificó y la cuarta muestra el propietario de la tarea. La quinta columna muestra el estado de la ejecución, el estado puede ser (R=ejecutando, PD=pendiente, CA=cancelado, CF=configurando, CG=completando, CD=completo, F=fallido). La sexta columna muestra el tiempo durante el cual se ha estado ejecutando  la tarea. Finalmente se muestra el número de nodos pedidos y la lista de nombre de los nodos que están participando en la ejecución. Si la tarea no se está ejecutando esta columna muestra la causa por el cual no se está ejecutando.


### Eliminar tareas

El comando `scancel` elimina las tareas de la cola de ejecución, sin importar el estado en el que esté. `scancel 173` elimina la tarea con identificador 173. Un usuario solo podrá borrar las tareas de su propiedad.

### Enlaces de interés

 * [Comandos básicos de slurm](https://slurm.schedmd.com/pdfs/summary.pdf) 
 
 * [Quick start slurm]( https://slurm.schedmd.com/quickstart.html)

 * [slurm](https://slurm.schedmd.com/) 
 
 