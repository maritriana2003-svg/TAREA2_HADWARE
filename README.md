````markdown
# Control remoto de actuador PC ↔ Arduino UNO

Proyecto desarrollado para la asignatura **Hardware Digital**.

## Descripción del proyecto

Este proyecto consiste en implementar un sistema de control remoto de actuadores mediante comunicación serial **UART** entre un **PC** y un **Arduino UNO**.

El PC envía comandos desde el **Monitor Serial** del Arduino IDE y el Arduino recibe, interpreta y ejecuta la orden correspondiente. Según el comando recibido, el sistema permite encender, apagar o consultar el estado de un **LED** y un **buzzer**.

Además, el programa genera una trama interna de 4 bytes con un byte de inicio `0xAA` y un `checksum` para validar la estructura del mensaje.

---

## Integrantes

- María Triana
- Camila Montes
- Fernanda Godoy
- Gabriela Ovalle

---

## Asignatura

**Hardware Digital**  
Docente: Diego Miranda  
Universidad de Valparaíso

---

## Objetivo general

Diseñar e implementar un sistema electrónico de control embebido utilizando Arduino UNO, gobernado por comunicación serial UART y orientado al control remoto de actuadores.

---

## Objetivos específicos

- Enviar comandos desde el PC hacia el Arduino UNO mediante UART.
- Controlar un LED y un buzzer usando comandos desde el Monitor Serial.
- Generar una trama interna de 4 bytes para estructurar la información.
- Incorporar un byte de inicio de trama `0xAA`.
- Calcular un `checksum` como método de verificación.
- Comprobar el funcionamiento mediante simulación en Tinkercad y montaje físico.

---

## Componentes utilizados

- Arduino UNO
- Cable USB
- Protoboard
- LED rojo
- Buzzer piezoeléctrico
- Resistencia de 220 Ω
- Cables jumper
- PC con Arduino IDE

---

## Conexiones del circuito

| Elemento | Conexión |
|---|---|
| LED positivo | Pin digital D13 |
| LED negativo | Resistencia de 220 Ω hacia GND |
| Buzzer positivo | Pin digital D8 |
| Buzzer negativo | GND |
| GND Arduino | Línea negativa de la protoboard |
| Alimentación | Cable USB desde el PC |

---

## Comunicación UART

La comunicación entre el PC y el Arduino UNO se realiza mediante UART utilizando el puerto serial disponible a través del cable USB.

| Parámetro | Valor |
|---|---|
| Velocidad | 115200 baudios |
| Bits de datos | 8 bits |
| Paridad | Sin paridad |
| Bits de parada | 1 bit |
| Control de flujo | Ninguno |

---

## Comandos disponibles

| Comando | Acción |
|---|---|
| `ON` | Enciende el LED y activa el buzzer |
| `OFF` | Apaga el LED y desactiva el buzzer |
| `ESTADO` | Consulta el estado actual del sistema |
| Otro texto | Muestra mensaje de comando inválido |

---

## Protocolo de comunicación

El sistema utiliza una trama interna de 4 bytes:

| Byte | Función | Descripción |
|---|---|---|
| Byte 0 | SOF | Inicio de trama, valor fijo `0xAA` |
| Byte 1 | ID de comando | Identifica si es control o consulta |
| Byte 2 | Valor | Indica encendido, apagado o estado |
| Byte 3 | Checksum | Suma de comprobación |

---

## Ejemplos de tramas

| Comando | Trama generada |
|---|---|
| `ON` | `[0xAA, 0x01, 0x01, 0xAC]` |
| `OFF` | `[0xAA, 0x01, 0x00, 0xAB]` |
| `ESTADO` | `[0xAA, 0x02, Estado, Checksum]` |

---

## Funcionamiento del sistema

1. El usuario escribe un comando en el Monitor Serial.
2. El Arduino UNO recibe el comando mediante comunicación UART.
3. El programa interpreta la orden recibida.
4. Se genera una trama interna de 4 bytes.
5. Se calcula el checksum.
6. Según el comando recibido, se activa o desactiva el LED y el buzzer.
7. El Arduino responde al PC con un mensaje de confirmación, estado o error.

---

## Archivos del proyecto

El repositorio contiene los siguientes archivos y carpetas principales:

| Archivo / Carpeta | Descripción |
|---|---|
| `CODIGO_FUENTE/` | Carpeta que contiene el código fuente del proyecto Arduino. |
| `control_remoto_actuador.ino` | Código principal cargado en el Arduino UNO. |
| `EvidenciaArduino/` | Carpeta con fotografías del montaje físico del circuito. |
| `Imagen del diagrama de bloques.png` | Diagrama de bloques del funcionamiento del sistema. |
| `esquema_conexiones_y_pines.png` | Imagen del esquema de conexiones y pines utilizados. |
| `Informe Control remoto de actuador PC ↔ Arduino UNO.pdf` | Informe técnico del proyecto. |
| `Video_Demostracion_Control_Remoto_Actuador.mp4` | Video demostrativo del sistema funcionando. |
| `README.md` | Documento principal del repositorio con la descripción del proyecto. |

---

## Código fuente

El código principal del proyecto se encuentra en la carpeta:

```text
CODIGO_FUENTE/
````

Archivo recomendado:

```text
control_remoto_actuador.ino
```

El programa configura el LED en el pin digital **D13** y el buzzer en el pin digital **D8**. Además, inicia la comunicación serial a **115200 baudios**, interpreta los comandos recibidos desde el PC y genera una respuesta mediante el Monitor Serial.

---

## Video demostrativo

El video de demostración muestra el funcionamiento del sistema **PC ↔ Arduino UNO + LED + Buzzer**.

En el video se evidencia:

* Conexión física del Arduino UNO.
* Envío de comandos desde el Monitor Serial.
* Activación del LED y buzzer con el comando `ON`.
* Desactivación del LED y buzzer con el comando `OFF`.
* Consulta del estado mediante el comando `ESTADO`.
* Respuesta del Arduino al PC mediante comunicación UART.

Archivo del video:

```text
Video_Demostracion_Control_Remoto_Actuador.mp4
```

---

## Pruebas realizadas

| Prueba           | Resultado esperado                    | Resultado obtenido |
| ---------------- | ------------------------------------- | ------------------ |
| Inicialización   | Actuadores apagados y mensaje inicial | Correcto           |
| `ON`             | LED encendido y buzzer activo         | Correcto           |
| `OFF`            | LED y buzzer apagados                 | Correcto           |
| `ESTADO`         | Respuesta del estado actual           | Correcto           |
| Comando inválido | Mensaje de error                      | Correcto           |

---

## Evidencias

El sistema fue probado en:

* Simulación en Tinkercad.
* Montaje físico con Arduino UNO.
* Monitor Serial del Arduino IDE.
* Pruebas de encendido, apagado y consulta de estado.
* Evidencia fotográfica del circuito armado.

Carpeta de evidencias:

```text
EvidenciaArduino/
```

---

## Limitaciones

* El sistema depende del cable USB para la comunicación con el PC.
* Al desconectar o reiniciar el Arduino, el sistema vuelve al estado inicial apagado.
* Los comandos deben escribirse correctamente para ser reconocidos.
* El uso de lectura por texto puede introducir pequeños tiempos de espera internos.

---

## Mejoras futuras

* Implementar interrupciones UART por hardware.
* Guardar el último estado usando memoria EEPROM.
* Agregar más comandos de control.
* Crear una interfaz gráfica en el PC.
* Mejorar el control de frecuencia del buzzer.

---

## Conclusión

El proyecto permitió implementar un sistema funcional de comunicación UART entre un PC y un Arduino UNO. A través del Monitor Serial fue posible controlar un LED y un buzzer de forma remota. Además, el uso de una trama estructurada y checksum permitió reforzar la validación del protocolo, demostrando comunicación bidireccional y control remoto de actuadores.

---

```
```
