# Documentacion

## Diseño

En la etapa de diseño primero entendimos el funcionamiento del sistema con todas sus partes, después de esto elegimos con que componentes íbamos a automatizar, llegando a la conclusión que para el control de los taques usaríamos sensores de proximidad capacitivos y un PLC para la programación en Ladder y su correcto funcionamiento, con esto en mente pasamos a diseñar la lógica del programa, como se muestra en el diagrama, la activación de las motobombas dependían del nivel del líquido, por ende, si el sensor de proximidad, puesto en la parte superior de los tanques, están desactivados significaba que el tanque no estaba lleno, por ende se activaban las motobombas, y llenado el tanque, desactivando las motobombas cuando el sensor se activaba, después se tenía que verificar el nivel de los dos tanques, si los dos están llenos se activaban las válvulas 1 y 2 para llenar el tanque de la mezcladora, y con un sensor en la mezcladora se mide si esta llena del todo, ósea que los dos tanques de los líquidos se vaciaron, para posteriormente cerrar las válvulas y empezar el proceso de mezclado por el tiempo indicado, después de que paso este tiempo indicado la válvula 3 se activa para llenar los respectivos envases de los detergentes, y con otro sensor en la parte final del tanque de la mezcladora se indica si toda la mezcla salió, por ende se procede a cerrar la válvula 3, y finalizado este proceso su suma uno al contador del proceso, y este se repite hasta que llegan a los litros indicados.

## Desarrollo

En la etapa de desarrollo implementamos una simulación en codesys para verificar el buen funcionamiento de la programación PLC en Ladder, para esto utilizamos contactos, bobinas, contadores y temporizadores, para simular el correcto funcionamiento usamos temporalizadores que simulan el llenado de los tanques en cada paso, mas no con entradas en los sensores, con todo esto se programó la lógica del PLC y se diseñó una HMI que le mostrara al usuario como el proceso estaba en funcionamiento y una indicación visual de cada estado en el proceso, esta implementación de entradas de los sensores se implementó en open PLC.

## Implementación:

En la implementación de la aplicación usamos un Arduino 1 usado como PLC, y cargamos el código mediante OPENPLC, en esta parte tuvimos en cuenta en funcionamiento normal del sistema, generando los cambios en el sistema cuando se activan los sensores, y no simulando un tiempo de llenado en cada tanque, para la simulación se planeó usar servo moteres para la simulación de las válvulas y un motor D.C para la mezcladora, pero finalmente se optó mostrar la salida del plc mediante leds, siendo cada led una representación del estado del sistema.

## Variables:
Start, Entrada, BOOL, es la representación del botón que inicia el proceso entero. 
Stop, Entrada, BOOL, es la representación del botón de emergencia, que para todo el proceso.
Reinicio, relay interno, BOOL, es el valor que reinicia todo el sistema para contar otra vez.
sensorTanque1, entrada, BOOL, es el valor que representa el sensor de nivel del tanque 1.
sensorTanque2, entrada, BOOL, es el valor que representa el sensor de nivel del tanque 2.
Las siguientes 3 variables representan que si está lleno el tanque igualmente no se activa el sensor.
aST1, relay interno, BOOL, es el valor que desactiva la señal del sensor del tanque 1.
aST2, relay interno, BOOL, es el valor que desactiva la señal del sensor del tanque 2. 
aSM, relay interno, BOOL, es el valor que desactiva la señal del sensor del tanque del mezclador. 
motoBomba 1, relay interno, BOOL: es el valor que representa la activación de la motobomba 1.
motoBomba2, relay interno, BOOL: es el valor que representa la activación de la motobomba 2.
valvula1, relay interno, BOOL, es el valor que representa la activación de la válvula 1.
valvula2, relay interno, BOOL, es el valor que representa la activación de la válvula 2.
válvulas, relay interno, BOOL, es el valor que representa la activación de las válvulas.
valvula3, relay interno, BOOL, es el valor que representa la activación de la válvula 3.
sensorMezcladora, relay interno, BOOL, es el valor que representa el sensor de nivel de la mezcladora llena.
sensorMezcladoraVacia, relay interno, BOOL, es el valor que representa el sensor de nivel de la mezcladora vacía
Mezclado, relay interno, BOOL, es el valor que representa que la mezcla esta lista.
aSST, relay interno, BOOL, es el valor que desactiva los sensores.
timerMezclar, tiempo, TON, controla el objeto TON del tiempo de mezcla.
tiempoMezclado, tiempo, TIME, es el tiempo que se demora el mezclado.
CTU_0, contador, CTU, controla el objeto CTU del contador.
Finaliza, relay interno, BOOL, es la variable que apaga todo el proceso cuando esta ha terminado;
salidaTotal, contador, INT, es la variable que lleva el conteo de cuantas veces se ha repetido el proceso.
aSMV, BOOL, apagar el sensor de la mezcladora cuando está vacía.
Contar, relay interno, BOOL, es la variable que indica si el contador debe funcionar.
Estas variables se usaron para la simulación de llenado de tanques en codesys
TON_MotoBomba1, tiempo, TON, controla el objeto TON del tiempo de llenado del tanque 1.
tiempoMotoBomba1, tiempo TIME, es el tiempo que se demora llenando el tanque 1.
TON_MotoBomba2, tiempo TON, controla el objeto TON del tiempo de llenado del tanque 2.
tiempoMotoBomba2, tiempo TIME, es el tiempo que se demora llenando el tanque 2.
timerValvula1, tiempo TON, controla el objeto TON del tiempo de vaciado del tanque 1.
tiempoValvula1, tiempo TIME, es el tiempo que se demora en vaciar el tanque 2.
timerValvula2, tiempo TON, controla el objeto TON del tiempo de vaciado del tanque 2.
tiempoValvula2, tiempo TIME, es el tiempo que se demora en vaciar el tanque 2.
timerValvula3, tiempo TON, controla el objeto TON del tiempo vaciar la mezcla.
tiempoValvula3, tiempo TIME, es el tiempo que se demora en vaciar la mezcla.
tanque1, relay interno, BOOL, es la que indica si el tanque 1 ya se llenó.
tanque2, relay interno, BOOL, es la que indica si el tanque 2 ya se llenó.
tanqueMezcladora: BOOL, es la que indica si el tanque de la mezcladora ya se llenó.

## Diagrama de actividades:
![proceso](https://user-images.githubusercontent.com/53841624/162262364-1f20173e-c3e2-4f9a-b87c-d255053d1b14.png)

## Diagrama del circuito eléctrico:
![circuito](https://user-images.githubusercontent.com/53841624/162262418-5e7c328d-76c9-4e3a-babe-5f55f16e9d7e.png)

