# CTFs de Reverse Engineering

Dos retos de *Reverse Engineering* independientes. Cada uno se juega descargando
un único ZIP y resolviéndolo con las herramientas que prefieras. **No hay que
romper ningún cifrado** en ninguno de los dos. El flag de ambos sigue el formato
**`C3TF{...}`**; cada enunciado explica cómo construirlo.

| Reto | Categoría | Dificultad | Descarga | Enunciado |
|---|---|---|---|---|
| **Rolling Code** | RE / RF (SDR) | Intermedia | [`rolling_code.zip`](rolling_code.zip) | [md](rolling_code/ENUNCIADO.md) · [pdf](rolling_code/ENUNCIADO.pdf) |
| **La última etiqueta** | RE / firmware | Intermedia | [`ultima_etiqueta.zip`](ultima_etiqueta.zip) | [md](ultima_etiqueta/ENUNCIADO.md) · [pdf](ultima_etiqueta/ENUNCIADO.pdf) |

Cada ZIP contiene el enunciado (`.md` + `.pdf`) y los ficheros del reto. También
puedes abrir los ficheros sueltos directamente en las carpetas de arriba.

## Rolling Code

Capturamos con un SDR la señal que emite un mando de coche al pulsar un botón.
Parte de la trama va cifrada y cambia en cada pulsación (*rolling code*); el
flag está en la **parte fija**.

- **Contenido:** `ENUNCIADO.md` (+ `.pdf`) y `keyfob_434M_1000k.cu8` (captura IQ).
- **Objetivo:** llegar desde la señal IQ hasta la trama digital y extraer el
  número de serie y el código de botón de la parte que no cambia.
- **Herramientas:** Inspectrum, URH, GNU Radio, rtl_433, o Python con numpy.

## La última etiqueta

Recuperamos el firmware de un controlador de impresora térmica y los bytes de un
trabajo de impresión a medias. La etiqueta contiene un código de recogida.

- **Contenido:** `ENUNCIADO.md` (+ `.pdf`), `controller.elf` y `pending_job.bin`.
- **Objetivo:** analizar el firmware ARM Cortex-M3, deducir el formato del
  trabajo y reconstruir la etiqueta para leer el código.
- **Herramientas:** Ghidra, un emulador (Unicorn), o Python.

---

*Los retos son sintéticos: no se ha transmitido nada por radio y no corresponden
a ningún sistema, vehículo ni dispositivo real.*
