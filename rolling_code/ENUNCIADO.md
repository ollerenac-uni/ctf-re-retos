# Rolling Code

**Categoría:** Reverse Engineering / RF
**Dificultad:** intermedia

---

Tienes una captura IQ sintética que simula la señal de un mando de coche al
pulsar un botón. Una parte de la trama cambia entre pulsaciones para simular
el *rolling code*. El flag está en la parte fija.

## Qué se entrega

```
keyfob_434M_1000k.cu8
```

Un archivo IQ crudo en formato de captura SDR. El nombre del fichero
sigue una convención habitual en capturas de SDR; si no te suena, merece la
pena averiguar qué significa antes de abrirla.

El formato `.cu8` son muestras complejas en `uint8` intercaladas (`I,Q,I,Q,…`).
Ojo con dónde está el cero en ese formato.

## Qué se pide

Llega desde la señal de radio hasta la trama digital, separa lo que cambia de
lo que no, y extrae de la parte fija el **número de serie** del mando (28 bits)
y el **código de botón** (4 bits).

## Formato del flag

```
C3TF{<aaaa>_<bbbb>}
```

- Junta el **número de serie** (28 bits → 7 hex) y el **código de botón**
  (4 bits → 1 hex): salen **8 dígitos hexadecimales en minúscula**.
- Pártelos por la mitad con un `_`: 4 hex, `_`, 4 hex.

Ejemplo del formato (no es el flag): `C3TF{0a1b_2c35}` (serie `0a1b2c3`,
botón `5`).

## Convención PWM

Cada bit ocupa tres unidades de tiempo. Un pulso alto de una unidad representa
un `0`. Un pulso alto de dos unidades representa un `1`.

Compara las ráfagas para localizar la parte fija de la trama.

## Si tu herramienta se cierra al abrir la captura

Si `inspectrum` termina con *Instrucción ilegal* (`SIGILL`) nada más abrir el
fichero, el problema no es la captura: la `libliquid` de tu instalación (por
ejemplo la de conda/radioconda) usa instrucciones (AVX2/AVX-512) que tu CPU no
tiene. Prueba con el `inspectrum` del gestor de paquetes de tu sistema
(`apt install inspectrum`, ejecutándolo por su ruta, `/usr/bin/inspectrum`), con
URH, o con Python y numpy.

## Herramientas que pueden ayudar

[Inspectrum](https://github.com/miek/inspectrum),
[Universal Radio Hacker](https://github.com/jopohl/urh),
[GNU Radio](https://www.gnuradio.org/),
[rtl_433](https://github.com/merbanan/rtl_433),
o Python con numpy.

---

*El reto se resuelve analizando el archivo IQ sin transmitir por radio.*
