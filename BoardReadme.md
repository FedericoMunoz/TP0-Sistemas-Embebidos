Descripción de la estructura de la carpeta Board del firmware de la EDU-CIAA:

La carpeta board posee cuatro subcarpetas:
- 'edu_ciaa_nxp': Esta carpeta posee los headers y sources específicos de la placa EDU-CIAA. Dentro de esta carpeta encontraremos:
		- board.h: (EDU-CIAA) Header donde figuran las posiciones específicas de los leds, botones, puertos ethernet, CAN y demás cosas que son propias de la placa EDU-CIAA
			Define además la frecuencia de la UART en 115200 baudios por default, el puerto I2C en 100 kHz y modo rápido, el sampling rate del ADC en 400 kHz y demás cosas que son propias de la placa.
		- board_api.h: (NXP) Define los prototipos de las funciones API necesarias para inicializar la placa. En la jerarquía se encuentra en un nivel más bajo que board.h

		- board.c: (EDU-CIAA) Funciones para inicializar la placa EDU-CIAA. Define la frecuencia del oscilador en 12MHz, la estructura de los puertos y los estados iniciales de los registros y puertos.
		- board_sysinit.c: (EDU-CIAA) Funciones para configurar los MUX y la SDRAM antes del main(). Propias de la placa EDU-CIAA.

- 'lib': Archivos para el linker del GCC. Entre los archivos que contiene se halla 'mem.ld' el cual define las regiones de memoria RAM y FLASH del microcontrolador.
- 'lpc_chip_43xx': Contiene las bibliotecas de NXP para el manejo de los chips 43xx y 18xx. Esta carpeta posee una gran cantidad de headers y sources que hacen de driver para manejar cada uno de los puertos y registros especiales (ADC, SPI, USB, EEPROM, etc). 
		Además de los drivers mencionados contiene algunos archivos que cabe la pena resaltar:
		- chip.h: Es el 'chip inclusion selector file'. Básicamente define si vamos a utilizar la familia 18xx o la 43xx. En base a esto se usan unos headers u otros. Define además los prototipos para configurar el clock y la preinicialización del USB.
		- chip_lpc43xx.h: Header que básicamente hace incluir todos los headers particulares de la familia 43xx.
		- sys_config.h: Definición de la arquitectura a utilizar: Se puede elegir entre Cortex M4 o Cortex M0
		- cmsis.h: En base a la arquitectura seleccionada incluye los headers que correspondan a la tupla (18xx/43xx,M0/M4).
		- cmsis_lpc43xx.h: Define la version del núcleo Cortex y los tipos para manejar las excepciones de las funciones.
		- lpc_types.h: Definicion de tipos básicos (bool, status, etc.)
- 'lpc_startup': Funciones para inicialización de la placa.


Entonces en orden de jerarquía sería lo siguiente:
		1) Bibliotecas propias del núcleo Cortex
		2) Bibliotecas propias de la familia LPC
		3) Bibliotecas propias de la placa EDU-CIAA