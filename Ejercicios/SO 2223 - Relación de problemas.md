# SO 22/23 - Relación de problemas

## Temas 1 y 2: Estructura de sistemas operativos; Procesos y hebras

###### Clara Mª Romero

### 1. ¿Cuáles podrían ser las principales razones para que un sistema operativo no sea diseñado de forma modular? 

1. Seguridad y estabilidad. Un sólo módulo que comete un error puede crashear el kernel completo y, de hecho, los módulos maliciosos son una posibilidad.
2. Programación y planificación más compleja.

### 2. ¿Cuáles son los principales problemas de una arquitectura monolítica? 

1. Poco fiables: si un proceso falla, falla todo el kernel.
2. Seguridad: al estar todo interconectado, es difícil mantener las partes sensibles aisladas y seguras
3. Tamaño: el kernel es un único programa de cientos de MB
4. Difíciles de mantener y escalar
5. Aplicar los cambios requieren reiniciar el sistema

### 3. ¿Cómo interactúan los programas de usuario y los servicios del sistema operativo con una arquitectura basada en microkernel? 

Cuando el programa de usuario quiere usar una utilidad del sistema, no se comunica directamente con el servicio, sino que hablan mediante paso de mensajes con el microkernel

### 4. ¿Cuáles son las ventajas y desventajas de la arquitectura microkernel? 

Ventajas:

1. Kernel más ligero
1. Kernel escalable, las funciones se implementan en espacio de usuario y no requieren modificar el kernel
1. Kernel fácilmente modificable debido a su reducido tamaño
1. Más portables, seguros y fiables.

Inconvenientes:

1. Pueden llegar a tener peor rendimiento, debido a la carga extra generada por las funciones del sistema que quedan fuera del microkernel.

### 5. ¿Dónde es más compleja una llamada al sistema, en un sistema monolítico o por capas? 

Para el programador, daría igual: ambos son una llamada al sistema a través de la API.

Para un desarrollador de sistemas, en un sistema monolítico. Aunque en un sistema por capas haya que lidiar con la comunicación entre capas, en el monolítico tenemos que "seguir" a la llamada por todo el sistema. Aunque sea tedioso atravesar capas y capas que no estamos usando, es mucho más fácil que seguir la pista a la llamada por todo el sistema monolítico.

### 6. Describa objetivo principal de las máquinas virtuales, tanto desde el punto de vista de un diseñador de sistemas operativos como de un usuario. Ventajas y desventajas de las máquinas virtuales. 

El objetivo de una MV es abstraer el hardware de la computadora (CPU, memoria, discos, redes...) y así poder formar entornos de ejecución diferentes, que aunque se ejecutan sobre la misma máquina física, dan la ilusión de operar sobre su propia computadora privada.

Ventajas:

- Protección completa de los recursos del sistema, cada VM está aislada totalmente de las demás
- Al estar aisladas, son perfectas para hacer cambios e investigar sobre el kernel
- Permiten implementar cambios y hacer pruebas sin detener el sistema

Desventajas:

- Difícil de implementar
- Difícil de implementar la compartición de recursos
- Los recursos son limitados y virtuales
- Rendimiento poco predecible, en ocasiones es necesario tener que simular todas las órdenes en el computador host

### 7. ¿Cuáles son las diferentes configuraciones a las que puede dar lugar el monitor de máquina virtual? Ponga ejemplos. 

Modo usuario virtual y modo kernel virtual. La VM es un programa de usuario, así que corre en modo kernel. Cuando en la VM se hace una llamada al sistema (en modo usuario virtual), se produce una transferencia al monitor de la VM en la máquina host. Cuando el monitor de la máquina virtual obtiene el control, ejecuta la llamada, cambia los registros, el CP... hace lo que tuviera que hacer en modo kernel; de esta forma simula el modo kernel virtual.   

### 8. Los contextos abarcan todas las actividades que realiza el núcleo ¿Cuáles son los diferentes contextos que ejecuta un procesador? 



### 9.¿Cómo consigue Linux evitar problemas de rendimiento que tienen los sistemas operativos microkernel, y aproximarse a la características de tener en memoria el núcleo mínimo posible y ser extensible a la vez? Enumere las ventajas adicionales que se obtienen con la propuesta de Linux al respecto. 

Utilizando un sistema modular. Está estructurado como una colección de módulos cargables, que se cargan y descargan bajo demanda. Las ventajas son que se pueden crear módulos cargables apilables, y definir dependencias entre módulos. Esto nos permite, por ejemplo, crear un módulo con el código común y que el código específico de cierto hardware sea dependiente de este módulo común. 

### 10. Describa las tareas típicas de las funciones que se realizan cuando se inicia y finaliza la utilización de un módulo.

Iniciar un módulo:

