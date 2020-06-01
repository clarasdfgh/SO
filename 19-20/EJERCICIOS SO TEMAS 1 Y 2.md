# EJERCICIOS SO: TEMAS 1 Y 2
###### Clara María Romero Lara
5, 10, 11, 13, 16, 17, 20, 25, 26, 30, y 31 + EJ. ADICIONAL

#### 5. ¿Dónde  es  más compleja  una  llamada  al  sistema,  en  un  sistema  monolítico  o  por capas?
*En un sistema por capas, ya que en el sistema monolítico se ejecuta la llamada de forma directa, sólo pasando del modo usuario al modo kernel. El hecho de atravesar capas jerárquicas dificulta el proceso.*


#### 11. Puesto que el propio núcleo de Linux puede requerir módulos ¿cómo lleva a cabo Linux la carga automáticas de dichos módulos?
*Mediante la tabla de módulos y la tabla de símbolos: *


#### 13.¿Cuáles   la   principal   ventaja   de Namespaces en   comparación   con   entornos virtualizados tales como KVM y VMWare?
*Los entornos virtualizados requieren más recursos, ya que crean kernels individuales para cada usuario. Los namespaces, en cambio, crean varios contenedores dentro de un único kernel compartido*

#### 16.Cuestiones sobre procesos, y asignación de CPU:
##### a)¿Es necesario que lo último que haga todo proceso antes de finalizar sea una llamada al sistema para finalizar? ¿Sigue siendo esto cierto en sistemas monoprogramados?
*Sí, es necesario liberar espacio reservado y el PCB para la llamada del siguiente estado preparado . En sistemas monoprogramados es incluso más importante este proceso.*
##### b)Cuando  un  proceso  se  bloquea,  ¿deberá  encargarse  él  directamente  de  cambiar  el valor de su estado en el descriptor de proceso o PCB?
*El estado del proceso se cambia desde el modo kernel, así que lo tiene que cambiar el PCB*
##### c)¿Qué  debería  hacer  el  planificador  a  corto  plazo  cuando  es invocado  pero  no  hay ningún proceso en la cola de ejecutables?
*Entrar en estado nulo, el cual tiene prioridad mínima (no puede bloquear ningún proceso) y se ejecuta de forma indefinida para que la cola de procesos no esté nunca vacía.* 

##### d)¿Qué algoritmos de planificación quedan descartados para ser utilizados en sistemas de tiempo compartido?

*Descartamos aquellos que no favorecen la concurrencia de procesos, bien porque priorizan los procesos largos (FCFS); bien porque pueden dar a inanición (SJF).*


#### 17. La representación gráfica del cociente 
 `(tiempo_en_cola_ejecutables + tiempo_de_CPU) /tiempo_de_CPU`
#### suele  mostrar  valores  muy  altos  para ráfagas muy cortas en casi todos los algoritmos de asignación de CPU ¿Por qué?
*Un proceso que usa ráfagas cortas pasa más tiempo en cola de ejecutables que en CPU. Según el cociente anterior, cuanto menos tiempo se pase en CPU se obtendrán valores mayores, más aún si el tiempo en cola es alto*


#### 25.En el algoritmo de planificación FCFS, la penalización definida por:
`(t + tº de espera) / t`
#### ¿es creciente, decreciente o constante respecto a t (tiempo de servicio de CPU requerido por un proceso)? Justifique su respuesta.

* *Procesos P1, P2, P3*
* *Tiempo de ejecución: 10 segundos (P1, P2, P3)*
* *Tiempo de espera: (t + te) = 1+(te/t)*
  * *El te siempre crece para cada proceso que se aleje del primero en ejecutarse, por lo que te/t **disminuye** según avanza la t1*


#### 26.En la tabla siguiente se describen cinco procesos:
| Proceso | Tiempo de creación | Tiempo de CPU |
| ------- | :----------------: | :-----------: |
| A       |         4          |       1       |
| B       |         0          |       5       |
| C       |         1          |       4       |
| D       |         8          |       3       |
| E       |         12         |       2       |
#### Si suponemos que tenemos un algoritmo de planificación que utiliza una política FIFO (primero en llegar, primero en ser servido), calcula:

        0   1   2   3   4   5   6   7   8   9   10  11  12  13  14
        __________________________________________________________
    A                   -   -   -   -   -   1
    B   1   2   3   4   5
    C       -   -   -   -   1   2   3   4   
    D                                   -   -   1   2   3
    E                                                   -   1   2
##### a) Tiempo medio de respuesta
Tiempo de respuesta: tiempo de espera + tiempo de CPU
- A = 6, (5+1)
- B = 5, (0+5)
- C = 8, (4+4)
- D = 5, (2+3)
- E = 3, (1+2)
Tiempo medio de respuesta: A+B+C+D+E / 5 =  5.4
##### b) Tiempo medio de espera
Tiempo de espera:
- A = 5
- B = 0
- C = 4
- D = 2
- E = 1
Tiempo medio de espera: A+B+C+D+E / 5 =  2.4

##### c)  La  penalización,  es  decir,  el  cociente  entre  el  tiempo de  respuesta  y  el  tiempo  de CPU
Tiempo de medio de respuesta: 5.4
Tiempo medio de CPU: 1+5+4+3+2 / 5 = 3  (tiempo medio de respuesta-tiempo medio de espera)
Penalización: 5.4 / 3 = 1.8

#### 30. Suponga que debe  maximizar  la  eficiencia  de  un  sistema  multiusuario  y  que  está recibiendo quejas de muchos usuarios sobre los pobres tiempos de respuesta (o tiempos de   vuelta) de sus procesos. Los resultados obtenidos con una herramienta de monitorización del sistema nos muestran que la CPU se utiliza al 99'9% de  su tiempo y que los procesadores de E/S están activos solo un 10% de su tiempo ¿Cuáles pueden ser las razones de estos tiempos de respuesta pobres y por qué?
a) El quantum en la planificación Round-Robin es muy pequeño.
~~b) La memoria principal es insuficiente.~~
c) El sistema operativo tiene que manejar mucha memoria principal por lo que las rutinas de gestión de memoria están consumiendo todos los ciclos de CPU
~~d) La CPU es muy lenta.~~
~~e) El quantum en la planificación Round-Robin es muy grande.~~

#### 31. Compare el  rendimiento  ofrecido al planificar el  conjunto  de tareas multi-hebras descrito en la tabla y bajo las siguientes configuraciones: 
###### a) Sistema  operativo  multiprogramado  con  hebras  de  usuario.  En  este  sistema  se dispone de una biblioteca para la programación con hebras en el espacio de usuario. El  algoritmo  de  planificación  de  CPU  utilizado  por  el  SO  es Round-Robincon  un quantum de  50  u.t.  (unidades de  tiempo).  El  planificador  de  la  biblioteca  de  hebras reparte el quantum del proceso  (tarea) entre  las hebras utilizando Round-Robin con un quantum para cada hebra de 10 u.t. Suponga que no existe coste en el cambio de contexto entre hebras ni entre procesos.

###### b) Sistema  operativo  multiprogramado  con  hebras  kernel.  El  SO  planifica  las  hebras usando Round-Robincon  un  quantum  de  10  u.t. Como  en  el  apartado  anterior, suponga  que  no  existe  coste  en  la  operación  de  cambio  de  contexto.  Considere además que las operaciones de E/S de un proceso únicamente bloquean a la hebra que las solicita.Suponga en ambos casos que los dos procesos están disponibles y que el planificador entrega la CPU al proceso P1. Para realizar la comparación represente en cada caso el diagrama de ocupación de CPU y calcule la ocupación de la CPU (tiempo CPU ocupada /tiempo total).

| Proceso | Hebras | Ráfaga de CPU | Tiempo de E/S | Ráfaga de CPU |
| ------- | :----: | :-----------: | :-----------: | :-----------: |
| **P1**  | Hebra1 |      20       |      30       |      10       |
|         | Hebra2 |      30       |       1       |       1       |
|         | Hebra3 |      10       |       1       |       1       |
| **P2**  | Hebra1 |      30       |      40       |      20       |
|         | Hebra2 |      40       |       1       |       1       |


## EJERCICIO ADICIONAL
 ##### Teniendo en cuenta las diferentes clases de planificación de procesos en Linux, y las políticas dentro de éstas, ponga un ejemplo de forma clara y descriptiva (mediante un diagrama de asignación de CPU) que muestre cómo Linux lleva a cabo la ejecución de procesos, considerando las siguientes indicaciones:
 ###### 1.  Que hay al menos 8 procesos repartidos entre las diferentes clases (Tiempo Real y CFS) y políticas (FIFO o ROUND-ROBIN dentro de Tiempo Real, y NORMAL e IDLE dentro de CFS) de planificación.
 ###### 2.  Decida los valores que considere oportunos acerca del comportamiento de cada uno de los procesos en cuanto a su ejecución (tiempo creación, duración de ráfagas de CPU, y tiempos de bloqueos en E/S), de forma análoga al Ejercicio 34 de la relación de problemas). 
 ###### 3.  Decida los valores de planificación que aplicaría el sistema en cuanto a target latency y minimum floor. 
 ###### 4.  Calcule algunos los parámetros explicados en clase y ejercicios resueltos (tiempo medio de espera, tiempo medio de respuesta, etc.) para dicha ejecución. 
