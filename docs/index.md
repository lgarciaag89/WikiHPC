# POLÍTICAS DE USO DE LOS SERVICIOS DEL HPC DE LA UNIVERSIDAD DE LAS CIENCIAS INFORMÁTICAS.

### Introducción
El presente documento tiene como objetivo definir las políticas de acceso de la infraestructura HPC UCI, así como las políticas de seguridad y uso de los recursos por parte de los investigadores que accedan al mismo. Las políticas definidas en este documento serán revisadas periódicamente y cualquier cambio en las mismas, será aprobado por la dirección de la universidad y trasmitido a toda la comunidad universitaria.

### Objetivo del HPC UCI
Proveer a la comunidad científica de la UCI, de una infraestructura de computación de alto desempeño (High Performance Computing, HPC), para el desarrollo y ejecución de proyectos de investigación que requieran alto procesamiento de datos.  

### Políticas de Uso

1. El uso del HPC UCI es libre para todos los miembros de la comunidad universitaria que requieran cómputo de alto rendimiento en sus actividades de investigación y estará regido por éstas “Políticas de Uso”.
2. El acceso al HPC se realizará a través del protocolo Secure Shell (SSH) con los mecanismos de autenticación usuario-contraseña o llave pública-llave privada. 
3. El acceso de un investigador al HPC será aprobado por 	el “Comité de Administración del HPC UCI” y dicho investigador deberá estar relacionado a un proyecto de investigación de la Universidad en ejecución. La autorización de acceso al HPC UCI y a los recursos obedecerá a un proceso de análisis y evaluación de las 	necesidades que presenten los proyectos que requieran tiempo de cómputo en el HPC.
4. Por razones de seguridad, no se podrá acceder vía SSH al sistema HPC UCI desde una computadora que se encuentre fuera de la red de datos UCI. Solo en casos excepcionales, se autorizará el ingreso de un usuario al HPC desde fuera de la Universidad a través de este protocolo.
5. A cada investigador autorizado a usar el sistema HPC UCI se le asignará un límite de tiempo para cada trabajo de cálculo. La asignación del tiempo para cada cálculo se determinará en base a las necesidades que tenga cada investigador.
6. Los proyectos estarán organizados por prioridad, siendo tarea del “Comité de Administración del HPC UCI” definir la prioridad 	para cada proyecto. Esta prioridad define el orden y los recursos a utilizar en el HPC, siendo las tareas asociadas a proyectos con mayor prioridad las primeras en ser ejecutadas. La prioridad para cada proyecto dependerá del impacto de la investigación o el fin de la misma y se definirá como (alto, medio, bajo).
7. Para la ejecución de tareas en el HPC serán definidas diferentes colas de ejecución configuradas con SLURMi. Cada proyecto será asignado a una cola en dependencia de la importancia y el tiempo asignado. 
8. El usuario deberá ejecutar las tareas solamente en la cola (o las colas) que se le defina al proyecto al que está asociado. La ejecución de tareas fuera de la cola definida no se realizará, definiéndose un ambiente interactivo en el caso de que el usuario necesite realizar pruebas pre-ejecución.
9. El sistema HPC UCI es un clúster para cómputo de alto rendimiento y no un equipo de almacenamiento, por lo que su espacio en disco es limitado. Considerando esto, es obligación de cada usuario, eliminar los archivos que resulten de sus cálculos de forma regular para evitar el mal funcionamiento del equipo.
10. La instalación de cualquier programa, componente o librería dentro del sistema HPC UCI deberá ser aprobada por el “Comité de Administración del HPC UCI”.
11. Las publicaciones resultantes (parciales o completas) de ejecuciones realizadas en el HPC UCI deberán poner en Agradecimientos, que sus resultados o parte de ellos fueron obtenidos en el HPC UCI. Se recomienda poner: “Los recursos computacionales utilizados en este trabajo fueron proporcionados por el Sistema de Alto Rendimiento de la Universidad de las Ciencias (UCI).
12. Todos los usuarios del HPC UCI deberán firmar un documento de aceptación de estas Políticas de Uso.