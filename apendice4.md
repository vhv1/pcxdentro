[^ Índice](README.md) | [Siguiente >](complemento.md)

----

# Apéndice 4

## MODELO CIRCUITAL DIDÁCTICO DE UCP
### Modelo circuital conceptual que no requiere conocimientos previos de circuitos lógicos, con camino de datos de concepción RISC

>El presente modelo apunta a ser una aproximación conceptual del funcionamiento interno de una UCP sin que el lector tenga un conocimiento previo del funcionamiento de los circuitos lógicos que se describen en la obra "De la Compuerta al Computador".  
Teniendo presentes los esquemas las figuras 1.31 y 1.32 con múltiples caminos entre registros se desarrollarán los mismos para comprender más en detalle como funciona un procesador en la ejecución de las instrucciones, sobre la base de un camino de datos ("data path") de 3 buses, como tienen los actuales procesadores.  
A los fines didácticos, a partir de la fig. A4.6 cada nueva figura incorpora (en trazo grisado) las descripciones de pasos en la ejecución de un total de 3 instrucciones llevados a cabo en las figuras anteriores, siendo que las líneas en trazo negro ilustran acerca del paso elemental que se está llevando a cabo. De esta manera, la fig. A4.14, última de la serie, permite integrar las anterior, y que el lector pueda tener una idea más general acerca del interior de una UCP sencilla, y cómo se repite la generación de las señales de control.

#### Descripción general

>Los bloques que aparecen bien delimitados en las figuras A.4.6 hasta A.4.14, que intervienen en la descripción, se comunican entre sí mediante caminos internos, es este caso de 8 ó 4 líneas conductoras, por las que puedan transitar simultáneamente hasta 8 ó 4 bits (como en una autopista de 8 carriles por la que circularían 8 ó 4 autos a igual velocidad como se detalla en la fig. 1.52). Este conjunto de líneas o "bus" se representa mediante una única línea gruesa, con la indicación del número 8 ó el 4 según sea.  
Las líneas de un solo conductor forman parte de la **UC** (no delimitada como bloque para no complicar los dibujos). La **UC**  por un lado *entran pulsos eléctricos* de igual duración de un **Secuenciador** (realizado en forma didáctica mediante una llave rotatoria que permanece igual tiempo en cada posición); y por otro lado la **UC** *recibe la orden que porta cada instrucción* mediante cada una de las líneas que salen del **Decodificador**.  
La **UC** realiza sus funciones de control mediante líneas de un solo conductor denominadas **líneas de control,** la mayoría de las cuales *determina si por el camino (bus) que cada una de ellas controla va a pasar o no información* (Esta alternativa se representa por un contacto o llave designado **L**, que puede estar cerrado o abierto, respectivamente, el cual es comandado por una de dichas líneas de control a él asignada en forma fija. Puesto que cada camino consta de 4 u 8 líneas, cada contacto dibujado representa 4 u 8 contactos que se deben cerrar o abrir al unísono. Otras líneas de control de la **UC** gobiernan la operación que debe hacer la **UAL**, y la línea L/ (que sale al exterior de la UCP) ordena si la memoria será leída o escrita. Otra línea E/ ordena escritura Las líneas de control cierran transitoriamente o mantienen abiertos los contactos **L** según el estado de otras líneas de un solo conductor del interior de la **UC** que las gobiernan. Estas se designan con indicación del tiempo durante el cual están activadas y del código de la instrucción del cual depende su aparición, como ser "3v.(volts) durante T1" ó "3v para 0001 y T3", etc.  
Dado que una línea de control puede cerrar el conjunto (4 u 8) de contactos **L** que comanda durante la ejecución de diferentes instrucciones o en distintos pasos de las mismas (en tal instrucción o en tal otra, o en tal otra o en tal paso de una instrucción o en tal otro de la misma), estas distintas alternativas que se pueden enunciar verbalmente, se representan mediante una compuerta **OR**, que se simboliza como una "media luna". Por lo tanto las líneas de control que salen de la **UC** *en general son salidas de compuertas OR ** (fig. A4.14)

>Los bloques delimitados en las figuras A4.6 hasta A4.14 son:  
>1. La **UAL** que recibe los dos datos a operar mediante los buses **X** e **Y** de 8 líneas que entran a ella, siendo que el resultado que genera en sus salida van al bus de 8 líneas designado **W**.
>2. Los **registros(R,A, RDI, IP),** que guardan información. Ellos pueden tomar o no información del bus **W** según el estado cerrados/abiertos de los contactos **L** que los vinculan con el bus **W**, para luego retenerla. Así mismo **R** y **A**, pueden enviar o no una copia de su contenido al bus **X** conforme el estado de los **L** que los ligan con el bus **X**. Al registro **IP** sus **L** lo comunican con el bus **Y**. El registro **RDI** (Registro de Direcciones) tiene sus 4 salidas conectadas directamente al bus de direcciones, por donde se envía cada dirección a la memoria. Sólo **RDI** e **IP** tienen 4 salidas; los restantes tienen 8.
>3. La **memoria**, que en este esquema consta de 16 celdas para 8 bits cada una, numeradas con direcciones de 0000 a 1111. Ya sea para leerla o escribirla, al registro **RDI** le debe llegar la dirección de la celda a la que se quiere acceder, la cual a través del bus de direcciones que comunica **RDI** con memoria llega al decodificador de ésta que permite localizar la celda direccionada de la forma vista en la figura 1xxx. Cuando la memoria es direccionada con orden de lectura (mediante la línea L/E) puede pasar una copia de los 8 bits contenidos en una celda de la misma al registro **RDA** (Registro de Datos) vinculado a ella. Desde éste una copia de dicha información puede pasar al bus **X** (si los contactos **Lx** está cerrado). Si se direcciona la memoria para escribir una celda, a **RDA** deben llegar los 8 bits a escribir desde el registro **A** por el bus **Y**, para lo cual los contactos **Ly** deben estar cerrados. Luego la línea L/E (lectura./escritura) debe dar la orden de escritura, para que una copia de **RDA** pase a la celda direccionada..
>4. El registro de instrucción, **RI**, que puede tomar directamente su contenido (una instrucción del programa) de **RDA** la cual a su vez provino de memoria, cuando los contactos **Lri** están cerrados.
>5. El **decodificador** cuyo accionar se verá luego, siendo que cada una de sus líneas de salida (una distinta por cada instrucción) determina los pasos para ejecutar la instrucción que activó la línea que le corresponde.
>6. Un **secuenciador** o generador de secuencias de pulsos de igual duración temporal.
Como se ha planteado (Sección 1.7), la ejecución de una instrucción se lleva a cabo mediante una secuencia de pasos que progresan con cada nuevo pulso originado por dicho generador.  
A los fines didácticos supondremos (fig. A4.1) una llave rotativa selectora de varias posiciones, capaz de comunicar los 3 volts (3v) de una batería conectada a su contacto central a la línea conductora que sale del punto donde la llave hace contacto. Si la llave permanece por ejemplo T = 1 segundo en cada posición, mientras queda ese tiempo en la posición o contacto 1, la línea unida al mismo (designada "3 durante T1") estará en toda su longitud con 3v. (fig. A4.2). También se dice que sobre esa línea tiene lugar un pulso de tensión de 3v designado T1, de un segundo de duración.  
Si luego que termina el primer segundo, instantáneamente la llave pasa al contacto 2 permaneciendo otro segundo (designado T2 en relación con el contacto2) en esta posición, los 3v de la batería se comunicarán a la línea "3v durante T2", naciendo un pulso T2 al mismo tiempo que "muere" T1. Del mismo modo, cuando la llave pasa al contacto 3, nace T3 y muere T2 como se aprecia en la (fig. A 4.2)  
*Estos pulsos serán usados por la* **UC** *para generar y determinar la duración de los pulsos de control que proveen las líneas de control, mediante los cuales cierra llaves ó indica órdenes para la UAL*.

![Figura A4.1 ](./img/apendice4/Figura-A4.1.jpg "Figura A.4.1")  
![Figura A4.2 ](./img/apendice4/Figura-A4.2.jpg "Figura A.4.2")  

Puede considerarse a su vez que otros "pulsos reloj" más angostos que caen a 0 volts cada segundo, en los instantes de tiempo 1,2,3,4,5 ...  generados por un cristal piezo-eléctrico, son los que hacen rota la llave. *Esta vuelve siempre al contacto 1*, para generar el pulso T1, pudiendo hacerlo desde el contacto 3,4 ó 5, según se necesite.

>Para un computador supondremos -según el ejemplo de la figura 1.29- que entre la aparición de un pulso reloj y el siguiente transcurre un tiempo de solo 20 nanosegundos (1 nseg. es una milésima de millonésima de segundo), que sería también la duración de los pulsos T1, T2, T3 .... generados hipotéticamente por la llave rotatoria temporizadora descripta. Esta frecuencia de aparición equivale a 50 millones de pulsos reloj generados por segundo, o sea 50 megahertz (MHZ).

>La **UAL** en relación con sus entradas **X** e **Y**, y salida **W**, en general puede hacer sumas o restas: X+- Y = W. Los valores X e Y son la información que viaja por los buses **X** e **Y**, pudiendo ser provista por dos registros como ser **A** y **RDA**. El resultado (que siempre pasa al bus **W**) puede ser asignado a un registro, como el **R**.

>La operación que efectuará la **UAL** depende de este esquema de cuál de sus líneas de operación (X+Y, 0+Y, etc.) esté activada por la línea de control de la **UC** que la activa, mediante un pulso de duración T1, T2, T3 ....  
Si la **UC** ordena hacer W = X + 0, y también ordena cerrar los contactos LrdA,X y Lz,A (que respectivamente permiten pasar información de **RDA** al bus **X**, y del bus **W** al registro **A**) resultará que una copia del registro **RDA** pasará, sin modificación alguna, al registro **A**. *Así pasa una copia del contenido de un registro a otro*. En caso de que la **UC** ordenara hacer W = 0 + Y y cerrar los contactos que correspondan, mediante un pulso de duración T1, T2, T3 ...., es factible transferir una copia del **IP** al **RDI**, o del **RI*** al **RDI**, según se necesite.  
De esta forma, los múltiples caminos entre registros de las figuras 1.31 y 1.32 han sido reemplazados por los tres buses interno **X, Y, W**, que a través de la **UAL** permiten por ejemplo transferencias entre registros, o sumar los contenidos de dos registros y el resultado guardarlo en un tercero.

>Las líneas "3v durante T1", "3v durante T2" .... que salen de la llave rotativa (fig. A4.1), *cuando están en 3v. se emplean mayormente para indicar intervalos de tiempo* (indicados T1, T2 ...) *en que deben permanecer cerradas* las **L** que ellas comandan, a fin de habilitar los caminos (buses) que dichas llaves gobiernan.  
*Cuando dichas líneas dejan de estar en 3v las llaves que dichas líneas comandan quedan abiertas, deshabilitando dichos caminos para que no puedan realizarse movimientos por ellos*.  
En la fig. A4.3a (que es parte de la fig. A4.6) se quiere simbolizar, que la línea "3v durante T1" comanda en ese tiempo T1 en que está en 3v. el cierre de las llaves **Lip,y** (la flecha al final de la línea que llega hasta la llave quiere indicar una fuerza que produce el cierre), para que una copia del contenido del registro **IP** pase al bus **Y**. Al mismo tiempo dicha línea cierra las llaves **Lrdi** para que el registro **RDI** pueda tomar la información 0000. 
![Figura A4.3a ](./img/apendice4/Figura-A4.3a.jpg "Figura A.4.3a")  
![Figura A4.3b ](./img/apendice4/Figura-A4.3b.jpg "Figura A.4.3b")

>La fig. A4.3b (parte de la A4.7) simboliza que al pasar la llave rotativa a la posición 2 deja de estar en 3v la línea "3v durante T1" por lo que aparece en grisado, con lo cual se abren las llaves **Lip,y** (que comunicaban **IP** con el bus **Y**) y las **Lrdi**, a la par que la línea "3v durante T2" cierra durante T2 las **Lip**, para que 0001 pase al **IP**.

### Compuertas AND y OR

>Es factible condicionar el cierre de llaves **L** a que dos (o más) líneas estén simultáneamente en 3v un tiempo T. Para ello dichas líneas deben ser entradas de una compuerta AND, cuya línea de salida comanda el cierre de llaves cuando permanece en 3v, y las abre mientras no se de dicha simultaneidad. Por ejemplo (fig. A4.4 que es parte de la fig A4.8), la línea de salida AND "3v para 0001 y T3" comanda el cierre/apertura de las llaves **Lir,X**. Esta línea durante el tiempo T3 permanecerá en 3v (cerrando las **Lir, X**) si están en 3v la línea "3v durante T3" y también la línea "3v para 0001" (esta última está en 3v mientras se ejecuta la instrucción de código 0001, durante T3 y T4, como se verá).   Puesto que sólo durante el tiempo T3 ambas líneas están en 3v, la salida de la AND "3v para 0001 **y** T3" *sólo estará en 3v durante T3,* **y** *sólo para la instrucción de código 0001*.  
![Figura A4.4 ](./img/apendice4/Figura-A4.4.jpg "Figura A.4.4")  
![Figura A4.5 ](./img/apendice4/Figura-A4.5.jpg "Figura A.4.5")

>De manera general, una **compuerta** circuital genera el estado eléctrico (0v ó 3v) de su línea de salida en función del estado eléctrico (0v ó 3v) de dos o más líneas que son sus entradas.  
En definitiva el cable de salida "3v para 0001 y T3" acompañará el estado de la línea "3v durante T3", o sea que sobre esa línea tendrá lugar un pulso de 3v que durará un tiempo T3. Es como si el pulso hubiese pasado de la línea de entrada "3v durante T3" a la de salida. De esta forma, de todo el tiempo en que "3v para 0001" está en 3v, con la línea "3v durante T3" se determina el tiempo T3 a fin de que las **Lir,X** estén cerradas sólo durante T3.

>Si para dos instrucciones distintas o pasos diferentes de una misma instrucción (durante la concreción de uno o del otro) se necesita cerrar las mismas llaves, se debe recurrir a una compuerta **OR** simbolizada como una media luna. Así (fig. A4.5 que es parte de A4.8), las llaves **Lrdi** se deben cerrar durante T1 por que está en 3v la línea "3v para T1 (fig, A4.3.a) o bien en T3 por estar en 3v la línea "3v para 0001 y T3" (fig. A4.4).  
A su vez como se vio, la salida AND "3v para 0001 y T3" para estar en 3v requiere la conjunción de dos líneas en 3v. En la figura A4.13 la OR se amplió a 4 entrada, pues como se verá, las **Lrdi** se deben cerrar durante T3 en cada una de las 3 instrucciones distintas ejecutadas, y además siempre durante T1 en el primer paso de cualquier instrucción, cuando se la solicita a memoria (en una o en otra o en otra o ....).
*En una OR basta que una entrada esté en 3v. un tiempo T para que su línea de salida también lo esté ese mismo tiempo. Mientras ninguna de sus entradas esté en 3v. su salida tampoco lo estará.

### Ejecución de instrucciones.
>Efectuaremos en el modelo de procesador la operación R = P + Q, teniendo presente sus analogías con una calculadora de bolsillo (fig. 1.2), y siendo: P = 5 = 00000101    Q = 4 = 00000100.  
En la fig. A4.6 y siguientes, las instrucciones tienen 8 bits: los 4 primeros para indicar la operación ordenada **(código de operación)**, y los 4 últimos para indicar en que dirección leer o escribir un dato en memoria.  
Las 3 instrucciones que usaremos se ha supuesto que ocupan las 3 direcciones sucesivas 0000, 0001 y 0010 de la memoria (fig. A4.6). Estas, al igual que los datos P y Q, en la práctica llegan a memoria provenientes de un disco, o desde el teclado.  
La instrucción **I1** (código de operación 0001) ordena llevar el registro **A** una copia del contenido de la celda de memoria de dirección 1010, donde se encuentra el valor de P (código completo: 0001 1010). Esto equivale a llevar el valor de P al visor de una calculadora de bolsillo, como el primer paso para hacer P + Q.  
La instrucción **I1** (código de operación 0001) ordena llevar al registro **A** una copia del contenido de la celda de memoria de dirección 1010, donde se encuentra el valor de P (código completo: 0001 1010). Esto equivale a llevar el valor de P al visor de una calculadora de bolsillo, como primer paso para hacer P + Q.  
La instrucción **I2** (código de operación 0011) ordena sumar al contenido del registro **A** una copia del contenido de la celda de dirección 1100 (donde se ha supuesto que está el valor de Q), y el resultado de la suma (en este caso P + Q) asignarlo al registro **A**, perdiendo éste su valor anterior. En cierto modo es como en una calculadora entrar el valor de Q y apretar la tecla +, de manera que cuando se pulsa la tecla = el resultado de la suma aparecerá en el visor en lugar del número anterior. Código completo: 0011 1100.  
La instrucción **I3** (código de operación 0111) indica llevar a la posición de memoria 1110 una copia del registro **A**. Se puede equiparar en cierta medida a la acción de pulsar en una calculadora la tecla **M**.+ para que una copia de lo que está en el visor se guarde en la memoria de la calculadora. Código completo: 0111 1110.  
Las acciones que ordenan I1, I2 e I3 están escritas en memoria, constituyendo un corto programa, para que se lleven a cabo cuando la UCP las ejecute, como se describe a continuación.

### ¿Cómo se ejecuta un programa constituido por I1, I2 e I3 en el modelo de la figura A4.6 y siguiente ?
>Antes de ejecutar un programa, es necesario que en registro **IP** esté la dirección de su primer instrucción (que en este caso es 0000), la cual en la práctica es determinada por el sistema operativo..
Como se detalla en la figura 1.27, la ejecución de una instrucción comprende en general los siguientes pasos, que progresan en sincronismo con los pulsos reloj:
>1. Obtener la instrucción mediante una lectura de la memoria, y llevar una copia de ella al registro **RI**. Mientras esto sucede la **UC** puede cambiar el valor de la **IP** para que contenga la dirección de la siguiente instrucción a ejecutar, que sigue a continuación en memoria.
>2. Con el código de la instrucción en **RI** la **UC** lo decodificará, con lo cual quedará determinado qué hardware intervendrá en cada uno los pasos siguiente que correspondan a la ejecución propiamente dicha.
>3. Obtener el dato a operar si el mismo está en memoria, para lo cual primero se debe determinar su dirección y luego pasarlo al registro **RDA** mediante una lectura de memoria. Si se debe escribir (un resultado) en la memoria se debe pasar en este paso su dirección al registro **RDI**.
>4. Realizar la operación que ordena la instrucción.

### ¿Cómo son los 4 pasos anteriores en la ejecución de I1?

![Figura A4.6 ](./img/apendice4/Figura-A4.6.jpg "Figura A.4.6")  
![Figura A4.7 ](./img/apendice4/Figura-A4.7.jpg "Figura A.4.7")  
![Figura A4.8 ](./img/apendice4/Figura-A4.8.jpg "Figura A.4.8")  
![Figura A4.9 ](./img/apendice4/Figura-A4.9.jpg "Figura A.4.9")  

>**Paso 1** (Obtención del código de la instrucción Ij en **R1**)
En este paso la llave rotativa temporizadora debe estar primero en la posición I durante T1=20 nseg, tiempo durante el cual la línea 3v durante T1 está en 3v; y luego en la posición 2 durante T2=20 nseg. siguientes.  
Puesto que I1 está en memoria, hay que localizarla en ésta mediante su dirección siempre contenida en el registro **IP** (fig. A4.6). Puesto que el único registro que está conectado al bus  de direcciones que va a memoria es **RDI**, en él se debe constituir cualquier dirección (de instrucción o de dato) a la que se quiere acceder en memoria. Por lo tanto, se debe pasar una copia de **IP** al **RDI**. Para ello la línea de control "3v durante TI" [^apendice4Unidad1Nota3] cerrará las llaves **LIP**,**Y**, lo cual permite que una copia del contenido del **IP** pase al bus **Y**. Asimismo, dicha línea también actúa sobre la entrada "0" + “**Y**” de la UAL para ordenar esa suma, de modo que sea W=Y. Así la copia del contenido del *IP** que viajaba por el bus **Y** pasa sin alteración (pues se le sumó 0) al bus **W**.  
Dado que por otra parte “3v durante T1” actúa cerrando las llaves **Lrdi**, el contenido de **IP** (0000, dirección de I1) que viaja por el bus **W** pasará al **RDI**, con lo cual también viajará por el bus de direcciones hacia memoria. Entonces en la memoria comenzará el tiempo de acceso [^apendice4Unidad1Nota4] para la localización de la instrucción (I1 en este caso), siendo que además se necesita que le llegue una orden de lectura por la línea L que debe estar n 3v, también merced a la línea “3v durante T1”.

>Cuando termina el tiempo T1 todas las llaves cerradas durante el mismo se abren, y la llave rotativa pasa a la posición 2 (figura A4.7), con lo cual queda en 3v durante T2=20 nseg, la línea de control “3v durante T2”.
Esta cierra las llaves **LM r1**, de modo que cuando legue a **RDA** el código de máquina de la instrucción pedida (en este caso 00011010 copia del contenido de la dirección 0000), dicho código pase sólo a **R1**.  
Paralelamente con esto “3v durante T2” cierra las llaves **Lip**, y abre **L’ip** (que volverá a su posición anterior cuando termine T2). Entonces la salida del sumador que suma 1 al contenido del **IP** (que mientras **L’ip** estaba cerrada era 0001 = 0000 + 1) comunicará su valor al **IP**. Este quedará así con 0001, preparado con la dirección de I2, para cuando se pida esta instrucción.  
En definitiva, luego de las acciones determinadas por las líneas de control “3v durante T1” y ” 3v durante T2” se habrá obtenido en **R1** el código 00011010 de I1 (instrucción a ejecutar), y en el **IP** la dirección de I2.  
En la descripción anterior debe observarse que cada transferencia de información que ha tenido lugar *sólo se han cerrado las llaves que permiten dicho movimiento*, siendo que las restantes quedan abiertas. Esto se logra en los tiempos apropiados(T1, T2, T3, …) merced a las líneas de control citadas que comandas dichas llaves.  
**Paso2** (Decodificación de la orden que determina los pasos a seguir)
Al mismo tiempo que en T2 llega la instrucción 00011010 al **R1**, sus primeros 4 bits (0001), que constituye el “**código de operación**” (cod-op) que ordena la operación a realizar, entran (fig A4.7) al circuito **decodificador**.  
Este tiene tantas salidas como instrucciones diferentes existan, pero sólo uno estará en 3v según sea el cod-op presente en el **R1**. Esa línea determinara los pasos a seguir, según se verá a continuación.
Así (fig. A4.8), toda vez que el cod.op sea 0001 (0 y 0 y 1, detectable mediante una And no dibujada) sólo la línea “3v para 0001” queda en 3v, mientras que las restantes salidas del decodificador quedan en 0 volts.
Esta situación subsistirá hasta que se termina a ejecutar la instrucción (tiempo T4 para esta instrucción I1).

>**Paso 3**(Obtención de dato)
Hasta acá luego de los tiempo T1 y T2 se obtuvo en **R1** una copia del código 00011010 de I1 que estaba en memoria. Como se verá a continuación en el tiempo T3 se direcciona el dato (P=5=00000101) que está en memoria (en la dirección 1010; y en el tiempo T4 este dato pasará de **RDA** al registro **A** (paso 4).  
El paso 3 empieza cuando la llave rotativa esta en la posición 3 en la que permanecerá T3=20 nseg, con lo cual quedará en 3v durante ese tiempo la línea “3v durante T3”. En el paso 2 la línea “3v para 0001” del decodificador ya esta en 3v, representando la orden “enviar al registro  **A** una copia del dato que esta en la dirección de memoria (en este caso 1010) que acompaña a la orden 0001”. Esta línea determina que deberá ocurrir en el circuito de los tiempos T3 y T4, para llevar a cabo la orden que ella representa, según se apreciará.  
Durante el tiempo o pulso T3 de ejecución de I1, las señales “3v para 0001” y “3v durante T3” están simultáneamente en 3v. Entonces (fig A4.8), la línea de salida designada “3v para 0001 y T3” de la compuerta AND de las que ellas son entradas estará en 3v durante T3 según se planteó en la fig A4.4. Entonces (fig A4.8), la salida “3v para 0001 y T3”deberá ordenar cerrar durante T3 las **Lrix** y **Lrdi**[^apendice4Unidad1Nota5], y ordenará que la **UAL** realice W=X+0, permitiendo así que la dirección del dato (1010) que está en la mitad de **R1** pase primero al bus **X**, y de este al bus **W**, desde donde pasa al **RDI**. De este registro llegará directamente a memoria a través del bus de direcciones (de forma semejante, en el paso 1 la dirección de I1 llegó a memoria a través del bus de direcciones (de forma semejante, en el paso 1 la dirección de I1 llegó a memoria, pero provista por el **IP**). Entonces la memoria comenzará el tiempo de acceso para la localización del dato (00000101=5=P) que está en la dirección (1010) dada por **RDI**. La línea L debe estar en 3v siendo la salida de una compuerta OR (agregada en la relación con la fig A4.6, pues se necesita ordenar leer en el paso 1 ó en el 3). De este modo L estará en 3v, si en la Or está en 3v su línea de entrada “3v durante T1” (como sucedió en el paso 1) o también si esta en 3v, su línea de entrada “3v para 0001 y T3” conforme ocurre ahora.

[^apendice4Unidad1Nota3]: En los gráficos que siguen las líneas de control que están en 3v s dibujarán en trazo negro.

[^apendice4Unidad1Nota4]: Tiempo que transcurre desde que la dirección se formó en **RDI** hasta que una copia de la información correspondiente a esa dirección llegue a **RDA**
[^apendice4Unidad1Nota5]: Dado que **LRDI** debe cerrarse durante **TI** cuando “3v durante T1” está en 3v  o también cuando “3v para 0001 y T3” está en 3v (como se da ahora), estas líneas deben ser de una **OR** (que no aparece por razones didácticas en la fig A4.6) cuya salida comanda a **LRDI**

>**Paso 4** (Realización de la operación ordenada)
Cuando la llave rotativa pasa a la posición 4 (fig A4.9) la línea “3v durante T4” queda en 3v, y tiene lugar el último paso de la ejecución de I1, durante el cual una copia del dato que en T4 llega a **RDA** pase al registro **A**.  
Para ello la línea de salida de AND “3v para 0001 y T4” cerrará las **LY**, así la salida de **RDA** podrá comunicar su contenido al bus **Y**. De este bus debe pasar al bus **W** para llegar al registro **A**, lo cual también requiere que la salida “3v para 0001 y T4” ordene a la UAL efectuar W=0+Y, y que las **Lw,A** se cierren.  
La operación W=0+Y se ordena haciendo que la línea “0+Y” que entra a la UAL esté en 3v. Como esto debe ocurrir durante T1 de la fase de pedido descripta o también en el presente, la salida OR de entradas “3v durante T1”, “3v para 0001 y T4” (no dibujada en la fig. A4.6) servirá en ambos casos para ordenar 0+Y.  
De esta forma, la señal “3v para 0001 y T4” determina que una copia de **RDA** pasa al registro **A**, quedando éste con el valor del dato (00000101=5=P), por lo que así finaliza la ejecución de I1

## ¿Cómo son los 5 pasos anteriores en la ejecución de I2 de código de operación 0011?

![Figura A4.10](./img/apendice4/Figura-A4.10.jpg "Figura A.4.10")

>**Paso1** (Obtención del código de la instrucción I2 en **RI**)
Como se determinó, durante el tiempo T2 de ejecución de I1, el **IP** había cambiado desde entonces el valor 0001, que es la dirección de I2.
Luego del tiempo correspondiente al último paso de la ejecución de una instrucción (T4 en la instrucción I1 anterior) siempre debe suponerse que la llave rotativa vuelve a su posición 1, para luego pasar a la posición 2,3, etc. Permaneciendo siempre 20 nseg. en cada posición. Así nuevamente se irán generando los tiempos T1, T2, T3, etc., siendo que para todas las instrucciones en T1 y T2, se lleva a cabo la fase de pedido de cada instrucción de manera semejante a como se hizo para I1 (figuras A4.6 y A4.7, de referencia para cualquier instrucción). Por consiguiente se hizo para I1 (figuras A4.6 y A4.7, de referencia para cualquier instrucción). Por consiguiente al cabo del tiempo T2 de la instrucción I2 será **IP**=0010 y **R1**=00111100, lo cual se da por supuesto en el paso posterior ilustrado en la figura A4.10, y en el paso 2 que se describe a continuación.

>**Paso2**(Decodificación de la orden que determina los pasos a seguir)
A la par que durante T2 llega la instrucción 00111100 al **R1**, sus primeros 4 bits (011), cod.op de la operación a realizar, entran al circuito decodificador. En éste, toda vez que el cod.op sea 0011 (0 y 0 y 1 y 1) sólo la línea “3v para 0011” queda en 3v mientras que las restantes salidas estarán en 0 volts. Esta situación perdura hasta que se termina de ejecutar la instrucción (tiempo T5 para esta instrucción I2)

>**Paso 3** (Obtención del dato en RDA)
En los tiempos T1 y T2 se obtuvo en R1 una copia del código 00111100 de I2 que estaba en memoria. En este paso, en el tiempo T3 se obtendrá en **RDA** el dato (Q = 4 = 00000100) que está en memoria (en la dirección 1100). En el tiempo T4 este dato se sumará al contenido registro A (paso 4).  
El paso 3 (ﬁg. A4.10) es igual al paso 3 de I1 (ﬁg. A4.8). Empieza con la llave rotativa en la posición 3 quedando así en 3V la línea “3V durante T3” (T3 = 20 nseg).  
Ya en el paso 2 la línea “3V para 001 l” del decodiﬁcador está en 3V para determinar que deberá ocurrir en el circuito en los tiempos T3, T4 y T5, para llevar a cabo la orden que esta línea representa: “sumarle al registro A una copia del dato que está en la dirección de memoria (en este caso 1100) que acompaña a la orden 0011 y el resultado asignarle al registro A en reemplazo del Valor que tenía “.  
Durante el tiempo T3 de ejecución de I2, las señales “3V para 0011” y “3V durante T3” están simultáneamente en 3V. Por lo tanto, como en la ﬁg. A4.8, la línea de salida “3v para 0011 y T3” de la compuerta AND de las que ellas son entradas estará en 3V durante T3. Entonces (ﬁg. A4.10), dicha salida “3V para 0011y T3” deberá ordenar Cerrar durante T3 las **LriX** Y **Lrdi**[^apendice4Unidad1Nota6], Y ordenará que la UAL realice W = X + 0, permitiendo así que la dirección del dato (1100) que está en la mitad de **RI** pase primero al bus **X**, de éste al bus **W**, desde donde pasa al **RDI**.
De este registro llegará directamente a memoria a través del bus de direcciones vinculado al mismo.  
En la memoria (con orden de lectura dada por la línea L/ en 3V) Comenzará a transcurrir el tiempo de acceso a la celda de dirección 1100, al final del cual (que será durante T4) una copia del contenido de esta celda (00000100 = 4 = Q), pasará al **RDA**.  
La línea L/ estará en 3v siendo la salida de una compuerta OR (con una entrada más en relación con la ﬁg. A4.8), siendo que L/. debe estar en 3v, si está en 3v su línea de entrada “3v durante T1” (como sucede en el paso 1 de la fase de pedido de cada instrucción) o también si está en 3v su línea de entrada “3v para 0001 y T3” (como sucedió en el paso 3 de II) o también si está en 3v su línea de entrada “3v para 0011 y T3” como ocurre en el paso 3 de la presente instrucción.

![Figura A4.11](./img/apendice4/Figura-A4.11.jpg "Figura A.4.11")

>**Paso 4** (Realización de la operación ordenada y almacenamiento del resultado en el registro temporario **R**) Cuando la llave rotativa pasa a la posición 4 (ﬁg. A4.11) la línea “3v durante T4” queda en 3v. Entonces tendrá lugar otro paso de la ejecución de I2. en el cual dicha línea en conjunción con la línea “3v para 0011” pondrán en 3v la línea de salida “3v para O011 y T4” de la AND cuyas entradas son esas dos líneas.



[^apendice4Unidad1Nota6]: Dado que Lrdi debe cerrarse durante T1 cuando "3v durante T1" está en 3v (como en el paso 1 de cualquier instrucción o también cuando "3v para 0001 y T3" está en 3v (como en el paso 3 de I1) o también como en este paso 3 de I2 (Con "3v para 0111 y T3" en 3v), estas 3 líneas deben ser entradas de una OR (que eran 2 en la ﬁg. A4.8) cuya salida comanda a 
Lrdi.  
Análogamente, para Lri,x ella debe cerrarse durante T3 en el paso 3 de I1 o de l2 (presente instrucción), o sea si está en 3v la línea "3v para 0001 y T3" o "3v para 0011 y T3", por lo que estas 2 líneas deben ser 2 entradas de una OR (no dibujada en la ﬁg A48) cuya salida comanda a Lri,x

>Esta salida determinara que la UAL sume el registro **RDA** (al durante T4 llega el dato desde 1100) con el A y que el resultado se guarde en el registro temporario **R** (que no será necesario en el modelo que se expone a continuación de éste). Se requerirá un quinto paso a ﬁn de que durante T5 una copia del registro **R** pase al **A**.  
Para el paso 4 la línea de salida de AND “3v para 0011 y T4” debe ordenar por un lado cerrar las **LY**[^apendice4Unidad1Nota7] así la salida de **RDA** podrá comunicar su contenido al bus **Y**, y por otro cerrar **LA, X** de forma que el registro **A** podrá pasar una copia de su contenido al bus **X**. Al mismo tiempo “3v para 0011 y T4” debe ordenar a la UAL efectúa, W = X + Y (mediante “X + Y”), y que LW,R se cierre a ﬁn de que el resultado de la UAL, siempre presente en el bus **W**, pueda llegar al registro **R**.  
De esta manera hasta acá (T4), la señal “3v para 0011 y T4” ha determinado que una copia de **RDA** se sume en la UAL con una copia del registro **A**, y que el resultado pase al registro **R**, quedando éste con el valor de la suma (00O01001= 9 = 5 + 4 = P + Q).

>**Paso 5** (Almacenamiento del resultado en el registro ordenado) 
Cuando la llave pasa a la posición 5 (ﬁg. A4.12) la línea “3v durante T5”queda en 3v, tendrá lugar el último paso de la ejecución de I2. En este paso dicha línea en conjunción con la línea “3v para 0011” pondrán en 3V la línea de salida “3v para 0011 y T5” de la AND cuyas entradas son esas dos líneas. Esta salida determinará que una copia de **R** pase al **A**.
Ello implica que “3v para 0011 y T5” cerrará las **Lr,X** así la salida del registro **R** podrá comunicar su contenido al bus **X**.  
De este bus debe pasar al bus **W** para llegar al registro **A**, lo cual también requiere que la salida “3v para 0011 y T5” ordene a la UAL efectuar W = X + 0, y que las **Lw,A** se cierren. W = X + 0 se logra haciendo que la línea “X + 0” que entra a la UAL esté en 3V.  
Como esto debe ocurrir en el paso 3 de la instrucción 0001 o también en el T5” servirá para ambos casos.   
De esta forma, la señal “3v para 0011 y T5” determina que una copia de R pase al registro A, quedando este con el valor del resultado (00001001 = P + Q), por lo que así ﬁnaliza la ejecución de I2

![Figura A4.12](./img/apendice4/Figura-A4.12.jpg "Figura A.4.12")

### ¿Cómo son los 4 pasos anteriores en la ejecución de l3?

>**Paso 1** (Obtención del código de la instrucción I2 en RI)
Como se determinó, durante el tiempo T2 de ejecución de I2, el **IP** había cambiado desde entonces al valor 0010, que es la dirección de I3.

[^apendice4Unidad1Nota7]: Siendo que **Ly** debe cerrarse en este caso, cuando la línea "3v para 0011 y T4" está en 3V o también cuando la línea "3v para 0001 y T4" está en 3V (como en el paso 4 de I1) se ha agregado en la ﬁg. A411 (en relación con la ﬁg A4.9) una compuerta **OR** cuyas 2 entradas son esas 2 líneas, para contemplar que su salida comande a **Ly**

>Luego del tiempo correspondiente al último paso de la ejecución de una instrucción (T5 en la instrucción I2 anterior) debe suponerse que la llave rotativa vuelve a su posición 1, para luego pasar a la posición 2, 2, etc, permaneciendo siempre 20 nseg, en cada posición. Así nuevamente se irán generando los tiempos T1,T2,T3,etc, siendo que para todas las instrucciones en T1 y en T2, se lleva a cabo la fase de pedido de cada instrucción de manera semejante a como se hizo para I1(figuras A4,6 y A4,7, de referencia para cualquier instrucción).  
Por consiguiente al cabo del tiempo T2 de la instrucción I3 será **IP**=0011 y **RI**=01111110,lo cual se da por supuesto en el paso 3 ilustrado en la fig.A4.I3.

>**Paso 2** (Decodificación de la orden que determina los pasos a seguir)
A la par que durante T2 llega la instrucción 01111110 al **RI**, sus primeros 4 bits (011), cod-op de la operación a realizar, entran (fig.A4,I3) al circuito decodificador. En este, toda vez que el cod-op sea 0111 (0y1y1) **solo** la línea "3v para 0111" queda en 3v mientras que las restantes salidas estarán en 0 volts. Esta situación perdura hasta que se termina de ejecutar la instrucción (tiempo T4 para esta instrucción I3).  

![Figura A4.13](./img/apendice4/Figura-A4.13.jpg "Figura A.4.13")

>**Paso 3**(Obtención de la dirección de memoria a escribir en **RDI**)
Al cabo del tiempo T2 se obtuvo el **RI**el código 01111110 de I3 que estaba en memoria. En este caso 3,en el tiempo T3 se obtendrá en **RDI** la dirección (1110)de memoria donde escribir el contenido del registro **A**.  
En el tiempo T4 este contenido pasara a **RDA** y se escribirá en memoria (paso$).  
En el paso 2 la línea "3v para 0111"del decodificador ya esta en 3v para determinar que deberá ocurrir en el circuito en los tiempos T3 y T4, para llevar a cabo la orden que esta línea representa:"en la dirección de memoria(en este caso 1110) que acompaña a la orden 0111 escribir una copia del contenido del registro **A**".

>El paso 3 empieza cuando la llave rotativa esta en la posición 3 en la que permanecerá T3= 20 nseg, con lo cual quedara en 3v durante ese tiempo la línea "3v durante T3".  
La dirección donde escribir el contenido de **A** se obtendrá de **RI**, siguiendo el mismo proceso que se hizo en el paso 3 de las instrucciones I1 e I2 (fig, A4,8 y A4,10).  
Durante el tiempo T3 de ejecución I3 las señales "3v para las señales 0111 y T3" de la compuerta AND de las que ellas son entradas estará en 3v durante T3 según se definió en la fig. A4,4. entonces (fig A4,13), dicha salida "3v para 0111 y T3" deberá ordenar cerrar durante T3 los contacto **LriX** y **Lrdi** [^apendice4Unidad1Nota8] y que la UAL realice W=X+0 dependiendo así que la dirección (1110) que esta en la mitad de **RI** pase primero al bus **X**, de este al bus **W** desde donde pasa al **RDI**, de este registro llegara directamente a la memoria a través del bus de direcciones vinculado al mismo. Así termina el paso del desarrollo 3.

[^apendice4Unidad1Nota8]: Dado que la **Lrdi** debe cerrarse durante T1 cuando " 3 durante T1" esta en 3v (como en el paso 1 de cualquier instrucción o también cuando "3v para 0001 y T3" esta en 3v (como en el paso 3 de I1) o también como en el paso 3 de I3 (con "3v  para 0111 y T3" en 3v estas 4 líneas deben se 3 entradas de una OR (que eran 3 en la fig.A4,10) cuya salida comanda **Lrdi**.

>**Paso 4** (Realización de la operación ordenada
)  
![Figura A4.14](./img/apendice4/Figura-A4.14.jpg "Figura A.4.14")

>Estando la dirección 1110 en **RDI**, cuando la lleve rotativa pase a la posición 4 (fig. A4,14)-con lo cual "3v durante T4" queda en 3v-tendrá lugar el ultimo paso de la ejecución de I3 que consistirá simplemente en que una copia del contenido de **A**(00001001 desde la instrucción anterior)pasa al registro **RDA** para que luego la memoria la escriba en la dirección dada por **RDI**. Para ello la línea de salida AND "3v para 0111 y T4" cerrara las **La,X** así a la salida de **A** podrá comunicar su contenido (00001001) al bus **X**. De este bus debe pasar el registro **RDA**lo cual también requiere que la salida "3v para 0001 y T4" ordene que las **LX** se cierren y que la línea E quede en 3 volts durante T4 (orden de escritura a la memoria) mientras dicha línea esta en 3v.   Entonces hacia el  final de T4 una copia de **RDA**(00001001)se escribirá en la dirección 1110, finalizando la ejecución de la presente instrucción.

>De esta forma se ha calculado mediante 3 instrucciones la expresión R=P+Q, habiendo quedado el resultado (00001001) guardado en memoria en la dirección asignada a la variable R.


## ¿Como queda en definitiva el circuito del procesador desarrollado?

>En la fig. A4,14 están integradas las figuras A4,6 y A4,14. Se invita al lector a repetir la ejecución de las instrucciones antes tratadas en este nuevo esquema mas general El circuito de la **AC** esta constituido por líneas de un solo conductor que pueden ser entradas de compuertas And, cuya salida van a compuertas Or, siendo que las salidas de estas ultimas son las líneas de control. El conexiado AND_OR de la **UC** pueden redibujarse según una matriz como en la figura A4,33 del modelo de UPC rápida para instrucciones de tipo RISC.

---
[^apendice4Unidad1Nota9]

[^apendice4Unidad1Nota9]: Análogamente para **Lri,x**,ella debe cerrarse durante T3 en los pasos 3 de I1 o de I2 o de I3(presente instrucción) o sea que si esta en 3v la línea "3v para 0001 y T3"**o** "3v para 0011 y T3"**o** "3v para 0111 y T3" por lo que estas 3 líneas deben ser 3 entradas en una **OR** (dibujada en la fig, A4,10 con dos entradas)cuya salida comanda a **Lri,x**

----

[^ Índice](README.md) | [Siguiente >](complemento.md)