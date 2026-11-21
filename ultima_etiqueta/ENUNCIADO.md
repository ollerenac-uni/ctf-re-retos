# La última etiqueta

**Categoría** Reverse Engineering  
**Dificultad** Intermedia

El paquete salió del almacén, pero nunca llegó a su destino.

Alguien alteró su etiqueta de envío. La impresora se apagó durante el trabajo
y recuperamos el firmware del controlador junto con los bytes del trabajo pendiente.
Sospechamos que la etiqueta contiene las instrucciones para recoger el paquete desviado.

Reconstruye la etiqueta y recupera su código de recogida, con formato `C3TF{...}`.
Respeta exactamente las mayúsculas, minúsculas, números y signos que aparezcan impresos.

## Archivos

- `controller.elf` contiene el firmware de un controlador ARM Cortex-M3,
  little-endian, con instrucciones Thumb/Thumb-2. Las direcciones de carga
  están incluidas en el ELF.
- `pending_job.bin` contiene el flujo de aplicación completo, desde el inicio
  hasta el final del trabajo. Los encabezados del transporte USB ya están retirados.

Puedes analizar el firmware y reconstruir el trabajo con las herramientas que
prefieras. Todos los datos necesarios están en estos archivos. El reto se
resuelve por software.
