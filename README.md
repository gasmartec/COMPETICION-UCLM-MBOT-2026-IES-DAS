# COMPETICION-UCLM-MBOT-2026-IES-DAS
Repositorio destinado a subir los materiales de la Competición de Robótica de la UCLM 2026, en su modalidad de MBOT

En este repositorio se encuentran los siguientes documentos:
* Archivos formato mblock con los programas de las 3 misiones.
* Documento "Memoria Tecnica", formato pdf. Se compone de una descripción técnica detallada del robot a nivel mecánico y de funcionamiento (sensores, actuadores, extensiones, movimiento,...). También tiene un apartado con un buen número de imágenes del robot en sus distintas configuraciones. En el apartado siguiente se comentan los programas generados para las tres misiones, así como la estrategia seguida. Finalmente se añade el link para visualizar el video del robot en funcionamiento, que se ha subido a la nube.
Por tanto, las imágenes que se solicitan sobre el robot se pueden consultar en dicho documento, y no se envían como archivos independientes.

A continuación se añade una descripción general de todo lo anterior. La información más detallada se puede encontrar en el documento "Memoria Técnica".

* HARDWARE
  
El robot se basa en el kit comercial Mbot2, que en su formato estandar viene dotado con dos motores con sus respectivas ruedas, como elementos motrices, y una rueda libre que estabiliza el vehículo. El controlador es una placa CyberPi, alimentada por una batería de litio. Como sensores, el robot lleva instalados un sensor ultrasónico capaz de medir distancias, y un sensor de luminosidad RGB enfocado hacia abajo que puede detectar diferencias de color en la superficie por la que se mueve el robot.

Para las misión 1 se usa el robot básico, pero para las misiones 2 y 3 se le añaden extensiones, en forma de brazos robóticos construidos con perfiles de madera y pletinas metálicas atornilladas. Estos brazos se mueven mediante servomotores conectados al robot. Para la misión 2 se han diseñado dos brazos que se cierran verticalmente en forma de pinza para "coger" las alpacas, y para la misión 3 se ha diseñado un brazo con una placa, que inicialmente está en posición vertical y baja hasta tapar la vela y apagarla.

* SOFTWARE
  
Los programas se han construido todos mediante el software mBlock.

Misión 1: La cadena de código principal diferencia entre si el sensor RGB detecta verde o no. Si no detecta verde simplemente avanza, y si detecta verde, dependiendo de con qué sensor lo detecte (izquierda o derecha) llama a dos funciones que giran 90º el robot y siguen la línea verde corrigiendo su dirección en función de los sensores que se activen, para mantenerla siempre a la izquierda.

Misión 2: Se comienza con una función "línea negra", que va ajustando la trayectoria para mantener al robot sobre la línea negra según los sensores que se activen. Cuando el robot detecta una intersección (los cuatro sensores se activan) llama a otras rutinas que siguen maniobras específicas (girar hacia almacén, girar hacia la alpaca). Para recoger la alpaca el robot se aproxima lentamente hasta que el sensor ultrasónico queda fuera de rango (<4cm) y entonces activa los servos que atrapan la alpaca. El robot diferencia entre los colores leyendo los valores RGB del sensor, y según el color detectado desarrolla unas maniobras u otras. También hay otra función para dejar la alpaca, abriendo las pinzas y realizando una maniobra de retroceso y giro.

Mision 3: En esta misión hemos trabajado principalmente con variables. El programa es bastante complejo, pero se podría resumir en que asigna valores a unas variables dependiendo del color que se haya detectado basándonos en los parámetros RGB de cada uno. Un programa principal, según la variable que se haya activado y haya tomado un valor alto llama a una función determinada, que ejecuta un movimiento tipo "siguelineas" en el robot. El robot detecta que está cerca de una llama cuando el camino que lleva se bifurca hacia los dos lados, muestra de que está ante el círculo que contiene la vela, entonces ejecuta una función de "apagarvela" que hace descender la placa. La estrategia de esta misión es que el robot se vaya moviendo siempre girando hacia la derecha en las bifurcaciones, ya que se ha comprobado que de esta manera recorre el circuito completo. Finalmente retorna a la línea negra principal y se mueve hasta estar a la altura del círculo blanco, momento en el que gira para buscarlo.
