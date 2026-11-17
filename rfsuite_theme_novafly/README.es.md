# Tema NovaFly para el dashboard de Rotorflight (EdgeTX, TX16S)

[English](README.md) | [Deutsch](README.de.md) | Español | [Français](README.fr.md) | [Italiano](README.it.md) | [Nederlands](README.nl.md)

El cockpit de NovaFly como tema para el dashboard de la Rotorflight Suite para EdgeTX (RFSuite), y una pantalla
detrás: BANK, para leer, ajustar y guardar las vueltas de rotor del banco con el que estás volando.

Las imágenes muestran la emisora y RFSuite en inglés. Con la emisora en español, el tema muestra sus textos en español.

![Cockpit en vuelo](images/07_cockpit_flight.png)

## Qué necesitas

- RadioMaster TX16S MK3 con EdgeTX 2.12.5 (el tema está dibujado para 800 x 480)
- RFSuite 0.2.2 en la tarjeta SD

## Instalación

1. Toma el ZIP de la carpeta `rfsuite_theme_novafly` de este repositorio y descomprímelo. Copia la carpeta `novafly` a
   la tarjeta SD de la emisora:

   `SCRIPTS/RFSUITE/user/dashboard/novafly/`

2. Reinicia la emisora.

3. Pulsa **SYS** e inicia **RFSuite** en Apps.

   ![Apps](images/01_system_rotorflight.png)

4. Abre **Settings**.

   ![Menú de Rotorflight](images/02_rotorflight_menu.png)

5. Abre **Dashboard**.

   ![Settings](images/03_settings_dashboard.png)

6. Abre **Theme**.

   ![Dashboard](images/04_dashboard_theme.png)

7. En **Theme**, elige **NovaFly**. Guarda con el símbolo de guardar de arriba.

   ![Theme](images/05_theme_novafly.png)

8. Vuelve a **Dashboard** y abre **Settings**.

   ![Dashboard](images/15_dashboard_settings.png)

   NovaFly tiene aquí su propia casilla. Abre **NovaFly**.

   ![Settings](images/16_theme_tiles.png)

   En **Colour**, elige el color del cockpit. Guarda con el símbolo de guardar de arriba y confirma con **Yes**.

   ![NovaFly](images/17_novafly_colour.png)

9. Pon el widget RFSuite en una pantalla. Si ya está en una de tus pantallas, sáltate este paso.
   Pulsa **TELE**: se abren los ajustes de las pantallas. Pulsa **+** arriba y luego **Add Screen**.

   ![Add Screen](images/12_add_screen.png)

   En **Layout**, elige **App mode**.

   ![Layout](images/13_layout_app_mode.png)

   Pulsa **Setup widgets** y luego el campo vacío. Elige **RFSuite**.

   ![Select widget](images/14_select_widget.png)

Vuelve a la pantalla con el widget RFSuite. Este es el cockpit en tierra:

![Cockpit en tierra](images/06_cockpit_ground.png)

Mantén el dedo sobre la pantalla: el cockpit pasa a pantalla completa. Se ve igual, pero solo en pantalla completa
acepta pulsaciones. Una pulsación larga de **RTN** sale de la pantalla completa.

## El cockpit

Es una pantalla de datos. Todos los valores vienen de la telemetría de RFSuite, en RFSuite no se cambia nada.

Vueltas de rotor en la esfera, tensión y carga de la batería, tensión del BEC, batería de la emisora, corriente,
temperatura del ESC y de la MCU, carga RT, enlace (RSSI y VFR), armado o desarmado, banco y rate activos, timer de
vuelo y nombre del modelo.

- **Timer de vuelo.** El reloj grande es el tiempo de vuelo de RFSuite. Cuenta mientras el modelo está armado; al
  desarmar se queda el tiempo del último vuelo. Las tres filas de debajo son los demás relojes de NovaFly; el tema no
  las rellena.
- **Batería.** El porcentaje se calcula a partir de la tensión por celda: 3,5 V por celda es 0 %, 4,2 V es 100 %.
- **RT.** La carga en tiempo real del FC. Si el FC no la envía, ahí pone CPU con la carga de la CPU.
- **VFR.** Con ELRS, detrás de VFR está la calidad del enlace (RQly).

Tres cosas puedes hacer en el cockpit en pantalla completa:

- **Color.** En tierra, mantén pulsada la cabecera de arriba, en el centro. Cada pulsación larga pasa con un pitido al
  siguiente de diez colores. El color se recuerda por modelo.
- **Menú rápido.** Una pulsación en el campo del estado de armado abre el menú rápido de RFSuite.
- **BANK.** Una pulsación en el campo **BANK | RATE** abre la pantalla BANK.

## BANK

Pulsa el campo **BANK | RATE** en el cockpit. BANK lee el banco en el que está el FC.

![BANK, banco 1 leído](images/08_bank_read.png)

El número son las vueltas de rotor de ese banco. Según el modo de governor del FC son las vueltas en rpm o el gas
máximo en %. Mientras gira el rotor, el banco activo muestra las vueltas de ese momento. El tema no rellena las dos
filas de debajo (- y +). Los demás bancos dicen NOT READ hasta que cambies a ellos con el interruptor de banco de
la emisora.

Pulsa el banco activo. Aparecen menos y más junto al número.

![BANK, menos y más](images/09_bank_chosen.png)

Cada pulsación cambia el valor un paso (10 rpm para las vueltas de rotor). Un valor cambiado está en amarillo y
SAVE se pone verde.

![BANK, valor cambiado](images/10_bank_changed.png)

Pulsa **SAVE**. El tema escribe el perfil de governor de ese banco a través de RFSuite, lo relee y lo compara, lo
escribe en la EEPROM y lo lee una vez más. Cuatro campos verdes y un pitido significan: guardado y comprobado.

![BANK, guardado](images/11_bank_saved.png)

Lo que BANK no hace:

- No lee ni escribe mientras el modelo está armado. Dice "Model is armed. Disarm first." y no sale nada.
- No escribe cuando el estado de armado es desconocido.
- No da por guardado un valor que el FC ha tomado de otra forma. Vuelve el perfil anterior y la pantalla dice
  "Read-back differs. NOT confirmed as saved."

**BACK** o la tecla **RTN** cierra BANK y el cockpit vuelve a estar ahí. Si se pierde el enlace con el heli, BANK
se cierra solo.

## Notas

- **Cambio de fase de vuelo.** RFSuite reconstruye la pantalla en cada cambio de fase de vuelo: cuando el governor se
  activa o el gas sube por encima del 35 %, cuando desarmas después del vuelo y cuando vuelves a armar después. La
  pantalla queda en negro alrededor de un segundo. BANK conserva lo que ha leído.
- **Gas en la emisora.** El tema no cambia nada en tu emisora. Si vuelas con el governor del FC, el gas de la emisora
  tiene que estar fijo en cada banco y no debe depender del stick de paso (colectivo). Quien copia un modelo en la
  emisora se lleva su curva de gas: el paso negativo a fondo puede entonces apagar el motor.

## Idiomas

Alemán, inglés, español, francés, italiano y neerlandés. El tema sigue el idioma de la emisora. Las palabras son las
mismas que en NovaFly. Con cualquier otro idioma de la emisora, el tema está en inglés.

## Licencia

GPLv3, como RFSuite.
