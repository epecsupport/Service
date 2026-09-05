---
layout: default
title: 3WA / ETU600
---

## 3WA / ETU600

### Interruptores giratorios:
Los interruptores giratorios de la ETU600 anulan cualquier parámetro correspondiente configurado mediante la pantalla integrada o PowerConfig, salvo que estén en la posición **e.SET**.

### Conector de opciones:
El conector de opciones (denominado "rating plug" en 3WL) debe insertarse por completo hasta que encaje con un clic; de lo contrario, pueden aparecer códigos de error. Tenga en cuenta que se debe tener cuidado para no doblar los pines dentro del receptáculo, ya que esto puede dañar permanentemente la ETU.

### No es posible realizar pruebas en banco fuera del interruptor:
Una ETU600 NO se encenderá cuando esté desconectada del ACB, incluso con una fuente de alimentación externa.

### Consideraciones específicas sobre alimentación, cable USB y PC:
Si es necesario alimentar la unidad de disparo mediante USB, la fuente debe tener un puerto USB-C nativo y capacidad para suministrar 1.5A a 5VDC.

Para comunicarse con la unidad de disparo mediante USB, se debe utilizar una PC con un puerto USB 3.2 "Power Delivery" nativo y conector tipo C, junto con un cable USB-C capaz de transmitir datos *y* suministrar 1.5A. Para mayor seguridad, utilice un cable compatible con Thunderbolt 4 o 5, ya que esta norma supera los requisitos y garantiza que tanto la capacidad de alimentación como la de transmisión de datos alcancen los niveles necesarios. Llevo una batería externa de 15W y un cable Thunderbolt 5, y esta combinación alimenta de forma fiable una ETU600.

### Modo DAS+ (AERMS):
DAS+/AERMS solo puede desactivarse mediante el mismo método con el que se activó. Se trata de un bloqueo de seguridad para garantizar que el interruptor no salga accidentalmente del modo DAS+ mientras alguien tiene abierto el equipo. El modo DAS+ se indicará mediante un LED azul brillante, el cuarto desde la izquierda, debajo del botón F2.

### Batería e indicador:
El indicador de la batería tiene tres "barras", pero estas no disminuyen realmente como en la mayoría de los dispositivos alimentados por batería. El indicador muestra "lleno", lo que indica que la batería está en buen estado, o "vacío", lo que indica que es necesario reemplazarla. La batería solo alimenta el reloj interno y es una batería de litio de tamaño ½AA y 3.6V. Número de catálogo de Siemens: 3WA9111-0EE81.

### Almacenamiento de la causa del disparo y consideraciones sobre la alimentación de control:
La última causa de disparo se conserva en la memoria mientras haya alimentación de control. Si se pierde la alimentación de control después de un disparo, la unidad recurrirá a su condensador interno para almacenar la causa. Para que este condensador pueda hacerlo, la ETU debe haber estado activa durante al menos dos horas antes del disparo; además, dispone de aproximadamente 24 horas de tiempo de descarga antes de que se pierda la causa del disparo. Para recuperar la causa del disparo sin alimentación de control, se requiere una conexión a una PC o una batería USB capaz de suministrar 1.5A.
 
La unidad de disparo solo puede registrar los disparos que detecte a través de los transformadores de corriente (CT) del interruptor y de la toma de tensión (si está instalada). Los disparos provocados por un relé de mínima tensión o una bobina de disparo NO se registran, ya que la unidad de disparo no los "detecta".

### Autoprueba de la unidad de disparo:
1. Cierre el interruptor
2. En la pantalla de estado de la ETU, seleccione TEST (compruebe la pantalla; normalmente es F3)
3. Pulse F3 para bajar hasta "ETU self-test with trip" (autoprueba de la ETU con disparo)
4. Pulse F4 para seleccionar
5. Inicie con "T" (compruebe la pantalla; normalmente es F3)
6. La ETU se comprobará a sí misma; aparecerá una marca de verificación junto a cada paso superado
7. Después de la última comprobación y una breve pausa, el interruptor se abrirá y mostrará una advertencia TRIP, que debería registrarse como TEST.
8. Si se produce una falla en cualquier momento, la prueba se detendrá y mostrará una precaución o advertencia, según corresponda.

### Indicadores LED:
- ACT (Activo)
	- Apagado - ETU no activada
	- Verde intermitente una vez por segundo - ETU activa
- AL (Alarma)
	- Apagado - La corriente es inferior al ajuste AL1.
	- Ámbar - La corriente de al menos una fase supera el ajuste AL1.
	- Rojo - La corriente de al menos una fase supera I~r~ (protección contra sobrecarga)
- INFO
	- Apagado - La unidad funciona con normalidad.
	- Amarillo - Hay una advertencia presente en el sistema.
	- Rojo - Hay un error presente en el sistema.
- DAS+
	- Apagado - AERMS no está activado.
	- Azul - AERMS está activado.

### Accesorios:
- La pequeña palanca negra utilizada para activar el bloqueo forma parte de la palanca del dispositivo de bloqueo. Si no se utilizan cilindros, el tipo de candado es el predeterminado, 3WA9111-0BA37.
- Se ha confirmado que las bobinas de disparo, las bobinas de cierre y los motores de carga de 3WL son intercambiables con los de 3WA.

### Consideraciones específicas de COM 190:
- Es una limitación conocida que la ETU600 no puede procesar una actualización de firmware mediante COM 190. Lamentablemente, las actualizaciones masivas de firmware deben instalarse individualmente mediante la conexión USB-C.

### Códigos de error y posibles soluciones:
- ERROR OPTION PLUG - Compruebe que el conector de opciones sea el correcto para el tamaño del bastidor. Desconecte la alimentación de control, retire el conector y compruebe si hay pines doblados dentro del receptáculo de la unidad de disparo o daños en el conector situado en la parte posterior del conector de opciones. Vuelva a insertarlo hasta que encaje con un clic. Restablezca la alimentación de control y vuelva a comprobarlo.
