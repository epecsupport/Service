---
layout: default
title: 3WA / ETU600 (Español)
autolink: true
---

## 3WA / ETU600

---
layout: default
title: 3WA / ETU600
autolink: true
---

## 3WA / ETU600

### Interruptores giratorios:
Los interruptores giratorios de la ETU600 anulan cualquier parámetro correspondiente configurado mediante la pantalla integrada o PowerConfig, salvo que estén en la posición **e.SET**. Tenga en cuenta que los interruptores deben colocarse *entre* las líneas y no sobre ellas; de lo contrario, la unidad de disparo no interpretará correctamente los ajustes.

### Option Plug:
El Option Plug (denominado "rating plug" en el 3WL) debe insertarse completamente hasta que encaje con un clic; de lo contrario, pueden aparecer códigos de error. Tenga cuidado de no doblar los pines dentro del conector, ya que esto puede dañar permanentemente la ETU.

### Prueba en banco de la ETU600 fuera del interruptor:
Es posible realizar una "prueba en banco" de una ETU600; sin embargo, para hacerlo es necesario disponer del arnés del interruptor. Como mínimo, debe conectarse el conector grande X21 situado sobre el soporte de las tomas de tensión, así como los dos conectores negros más pequeños del módulo TUI600 (USB/Bluetooth) situado en la parte posterior de la unidad de disparo. Esto permitirá alimentar la unidad de disparo mediante el puerto USB o mediante las conexiones de alimentación de control de 24 VCC. Dependiendo de cuántos componentes del interruptor estén conectados, pueden aparecer varios códigos de error, tal como se detalla en la sección "Códigos de error y posibles soluciones" más adelante.

### Especificaciones de alimentación, cable USB y PC:
Si es necesario alimentar la unidad de disparo mediante USB, la fuente debe disponer de un puerto USB-C nativo y ser capaz de suministrar 1,5 A a 5 VCC.

Para comunicarse con la unidad de disparo mediante USB, debe utilizarse un PC con un puerto USB 3.2 "Power Delivery" nativo con conector tipo C, junto con un cable USB-C capaz de transmitir tanto datos *como* 1,5 A. Para mayor seguridad, utilice un cable compatible con Thunderbolt 4 o 5, ya que este estándar supera los requisitos y garantiza que tanto la capacidad de alimentación como la de transmisión de datos sean suficientes. Yo llevo una batería externa de 15 W y un cable Thunderbolt 5, y esta combinación alimenta de forma fiable una ETU600.

### Solución de problemas de "bloqueo en DAS+" (modo AERMS):
DAS+/AERMS solo puede desactivarse mediante el mismo método con el que fue activado. Se trata de un bloqueo de seguridad destinado a evitar que el interruptor salga accidentalmente del modo DAS+ mientras alguien está trabajando con el equipo abierto. El modo DAS+ se indica mediante un LED azul brillante, el cuarto desde la izquierda, debajo del botón F2.

Las condiciones DAS+ pueden "acumularse". Si DAS+ ha sido activado por varias fuentes (por ejemplo, interruptor con llave, teclado, COM190 y Bluetooth), **TODAS** esas fuentes deben desactivarse antes de que la unidad de disparo pueda salir del modo DAS+.

Si una unidad de disparo no sale del modo DAS+, conéctela a un PC que ejecute la versión más reciente de PowerConfig. Cargue el 3WA, vaya a la página **"Measurements"** (botón con el indicador) y haga clic en **"Go Online"** (botón con las gafas de sol). Dependiendo de la conexión, los datos pueden tardar hasta un minuto en actualizarse.

En **Status Values -> Status -> DAS+ enabled from**, deberían aparecer 15 valores true/false. Cualquier valor que aparezca como **"true"** debe resolverse mediante el método correspondiente antes de que la ETU pueda salir del modo DAS+. A continuación se explican algunos de los tipos:

**ETU display** - DAS+ fue activado mediante la pantalla y el teclado de la ETU. Vuelva al menú principal, pulse la tecla programable DAS+ y debería aparecer la opción para restablecerlo.

**ETU input** - DAS+ fue activado mediante la entrada digital de la ETU. En equipos QT, esta debería corresponder al interruptor con llave. Colóquelo en "off". Si ya estaba en "off", colóquelo en "on" y compruebe si el valor cambia. Si cambia, el AERMS está cableado incorrectamente.

**COM A/COM B** - DAS+ fue activado mediante COM190 (PROFINET/Modbus TCP) o COM150 (Modbus RTU). El interruptor deberá recibir una señal para desactivar este bit a través de su módulo de comunicaciones para poder desactivar DAS+. No existe ningún método para omitir este requisito.

**TUI600** - DAS+ fue activado mediante USB o Bluetooth. El firmware no diferencia entre ambos métodos, y debería ser posible desactivarlo mediante PowerConfig desde un PC o mediante la aplicación móvil.

### Consejos para la conexión Bluetooth:
PowerConfig Mobile presenta numerosos errores y con frecuencia rechaza o no logra establecer una conexión con la ETU. Si indica que el código de emparejamiento es incorrecto aunque haya introducido el código correcto, fuerce el cierre de la aplicación e intente conectarse de nuevo. No he encontrado un método fiable para hacerlo funcionar aparte de intentarlo repetidamente.

Existen dos modos Bluetooth que no se mencionan en el manual del 3WA: RO y RW. RO significa **"read only"** (solo lectura) y RW significa **"read/write"** (lectura/escritura). Solo pueden realizarse cambios en modo RW. En ocasiones es necesario alternar entre estos modos para que el TUI600 recuerde en qué modo se encuentra.

Para borrar una conexión se requieren tres pasos:

1. En el menú Bluetooth de la unidad de disparo, seleccione **"Clear Devices"**.
2. En PowerConfig Mobile, elimine el dispositivo.
3. En la configuración Bluetooth del dispositivo, busque la entrada **"3WA"** y seleccione **"forget this device"**.

### Batería e indicador:
El indicador de batería tiene tres "barras", pero estas barras no disminuyen progresivamente como en la mayoría de los dispositivos alimentados por batería. El indicador solamente muestra **"lleno"**, lo que indica que la batería está en buen estado, o **"vacío"**, lo que indica que la batería debe sustituirse.

La batería únicamente alimenta el reloj interno y es una batería de litio de tamaño ½AA y 3,6 V. Número de catálogo Siemens: **3WA9111-0EE81**.

### Almacenamiento de la causa de disparo y consideraciones sobre la alimentación de control:
La causa del último disparo se conserva en memoria mientras haya alimentación de control. Si se pierde la alimentación de control después de un disparo, la unidad utilizará su condensador interno para almacenar la causa.

Para que este condensador pueda hacerlo, la ETU debe haber estado activa durante al menos dos horas antes del disparo. El condensador dispone de aproximadamente 24 horas de tiempo de descarga antes de que se pierda la causa del disparo.

Para recuperar la causa del disparo sin alimentación de control se requiere una conexión a un PC o una batería externa USB capaz de suministrar 1,5 A.

La unidad de disparo solo puede registrar disparos basándose en aquello que puede detectar mediante los transformadores de corriente (CT) del interruptor y las tomas de tensión, si están instaladas. Los disparos provocados por un relé de subtensión o una bobina de disparo **NO** se registran, ya que la unidad de disparo no los "detecta".

### Autoprueba de la unidad de disparo:
1. Cierre el interruptor.
2. Desde la pantalla de estado de la ETU, seleccione **TEST** (compruebe la pantalla; normalmente F3).
3. Utilice F3 para desplazarse hasta **"ETU self-test with trip"**.
4. Pulse F4 para seleccionar.
5. Inicie la prueba con **"T"** (compruebe la pantalla; normalmente F3).
6. La ETU realizará una comprobación interna. Aparecerá una marca de verificación junto a cada paso superado.
7. Después de la última comprobación y una breve pausa, el interruptor se abrirá y mostrará una advertencia **TRIP**, que debería quedar registrada como **TEST**.
8. Si se produce un fallo en cualquier momento, la prueba se detendrá y se mostrará la precaución o advertencia correspondiente.

### Indicadores LED:
- **ACT (Active)**
	- Apagado - ETU no activada.
	- Verde intermitente una vez por segundo - ETU activa.
- **AL (Alarm)**
	- Apagado - La corriente es inferior al ajuste AL1.
	- Ámbar - La corriente en al menos una fase supera el ajuste AL1.
	- Rojo - La corriente en al menos una fase supera I~r~ (protección contra sobrecarga).
- **INFO**
	- Apagado - La unidad funciona normalmente.
	- Amarillo - Hay una advertencia presente en el sistema.
	- Rojo - Hay un error presente en el sistema.
- **DAS+**
	- Apagado - AERMS no está activado.
	- Azul - AERMS está activado.

### Accesorios:
- La pequeña palanca negra utilizada para accionar el bloqueo forma parte de la palanca del dispositivo de bloqueo. Si no se utilizan cilindros de cerradura, la configuración predeterminada es la versión para candado, **3WA9111-0BA37**.
- Se ha confirmado que las bobinas de disparo, las bobinas de cierre y los motores de carga del 3WL son intercambiables con los del 3WA.

### Especificaciones de COM 190:
- Es una limitación conocida que la ETU600 no puede procesar una actualización de firmware mediante COM 190. Lamentablemente, las actualizaciones masivas de firmware deben realizarse individualmente mediante la conexión USB-C y tardan aproximadamente 10 minutos por unidad.

### Códigos de error y posibles soluciones:
- **ERROR OPTION PLUG** - Compruebe que el Option Plug sea el correcto para el tamaño del bastidor. Desconecte la alimentación de control, retire el plug y compruebe si hay pines doblados dentro del conector de la unidad de disparo o daños en el conector situado en la parte posterior del Option Plug. Vuelva a insertarlo hasta que encaje con un clic. Restablezca la alimentación de control y vuelva a comprobarlo.

- **ERROR N-CT** - Si hay un CT de neutro instalado, compruebe la conexión y el cableado. Si no hay un CT de neutro instalado, compruebe que exista un puente entre X8-9 y X8-10. Si no existe ningún puente, desconecte la alimentación de control, conecte los terminales X8-9 y X8-10 mediante un puente o un trozo de cable y, a continuación, restablezca la alimentación de control y vuelva a comprobarlo. Para pruebas en banco, localice los cables identificados con estos números de terminal y conéctelos utilizando, por ejemplo, un conector Wago.

- **ERROR GF-CT** - Si hay un CT de falla a tierra instalado, compruebe la conexión y el cableado. Si no hay un CT de falla a tierra instalado, compruebe que exista un puente entre X8-11 y X8-12. Si no existe ningún puente, desconecte la alimentación de control, conecte los terminales X8-11 y X8-12 mediante un puente o un trozo de cable y, a continuación, restablezca la alimentación de control y vuelva a comprobarlo. Para pruebas en banco, localice los cables identificados con estos números de terminal y conéctelos utilizando, por ejemplo, un conector Wago.

- **ERROR CURRENT SENSOR (1/2/3)** - La documentación de solución de problemas de Siemens indicará un fallo del CT de fase. Aunque estos CT son accesibles, Siemens no los ofrece como piezas reemplazables en campo. Tenga en cuenta que este error también puede deberse a un error de suma si la detección de falla a tierra está configurada como **"direct"** o **"dual"** cuando no hay ningún CT de falla a tierra instalado. Si no se utiliza un GF-CT, configure la falla a tierra como **"residual"** en los ajustes de protección. Para pruebas en banco, conecte un juego de CT de fase si dispone de ellos.
