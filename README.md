 # Tarea 2: Sistema de Comunicación Serial entre Dispositivos

## 🏛️ Universidad de Valparaíso
* **Facultad:** Ingeniería
* **Escuela:** Ingeniería en Informática (Campus San Felipe)
* **Asignatura:** Hardware Digital (ISF-215)
* **Docente:** Diego Miranda

---

## 👥 Integrantes y Roles
| Nombre Completo | Rol Asignado | Correo Institucional |
| :--- | :--- | :--- |
| **Adriana Castillo Uribe** | Coordinadora de Firmware / QA | adriana.castillo@alumnos.uv.cl |
| *[Nombre Integrante 2]* | Diseñador de Protocolo / UML | *[Correo]* |
| *[Nombre Integrante 3]* | Encargado de Documentación | *[Correo]* |

---

## 🚀 Avance 1: Prueba de Concepto (Esquema Polling)
Este repositorio contiene el avance inicial para el desarrollo de la **Tarea 2**. Actualmente se encuentra implementada la infraestructura física básica y una solución de software de prueba basada en **Polling**, permitiendo verificar la correcta respuesta de los periféricos y la conexión física con la PC.

### 🛠️ Hardware y Periféricos Utilizados:
* **Nodo 1 (Maestro):** Computadora Personal (PC) como terminal de control.
* **Nodo 2 (Esclavo):** Arduino UNO R3.
* **Actuador Sonoro:** Buzzer Piezoeléctrico conectado al **Pin Digital 8** para alertas del sistema.
* **Actuador Lumínico:** LED Indicador integrado conectado al **Pin Digital 13**.
* **Canal de Enlace:** Cable USB de Arduino (Interfaz UART mapeada a puerto COM virtual).

---

### ⚙️ Funcionalidad del Código Base
El sistema lee cadenas de caracteres mediante funciones de lectura serial tradicionales en el lazo principal. Reacciona ante los siguientes comandos directos ingresados en el Monitor Serial de la PC:
* `"ON"`: Enciende el LED del pin 13 y activa un tono continuo en el buzzer.
* `"OFF"`: Apaga el LED y silencia las frecuencias del buzzer.
* `"ESTADO"`: Envía un reporte de confirmación en texto plano de vuelta a la pantalla de la PC.

---

## 📅 Próximos Hitos de Desarrollo (Hacia la Entrega Final)
Para cumplir con las exigencias de la rúbrica y los requerimientos del profesor, las siguientes versiones incluirán:
1. **Migración a Interrupciones (ISR):** Configuración del registro `UCSR0B` para lectura por hardware mediante `ISR(USART_RX_vect)`.
2. **Estructura de Trama Binaria:** Definición formal de un paquete de 4 bytes con campo de sincronización (`SOF = 0xAA`) y verificación **Checksum (XOR)**.
3. **Control de Robustez:** Rutina de manejo de errores físicos ante tramas corruptas (ráfagas de alerta audibles).
4. **Análisis Cuantitativo:** Mediciones de latencia con `micros()` para las gráficas comparativas del informe técnico.
