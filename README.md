# TranscripHealth

**TranscripHealth** es una aplicación web simple diseñada para profesionales de la salud que necesitan registrar resultados de pruebas de manera rápida y manos libres. La aplicación escucha instrucciones de voz, registra únicamente los comandos que comienzan con **"prueba de ... resultado ..."** y genera un texto final al finalizar la evaluación.

## Características principales

* **Reconocimiento de voz** usando la API de reconocimiento de voz del navegador (Web Speech API). La aplicación inicia y detiene la grabación según el control del usuario.
* **Parser estricto**: solo persiste la información si el comando de voz comienza con `prueba de` seguido de un nombre de prueba y un valor de resultado.
* **Edición de ítems**: el usuario puede editar o eliminar cada prueba registrada de manera manual si lo desea.
* **Plantilla única editable**: existe un único formato de salida que el usuario puede modificar a través de un área de texto. La plantilla soporta placeholders básicos para meta‐información y datos de las pruebas.
* **Generación de informe**: al decir "fin de evaluación" o al presionar el botón *Finalizar Evaluación*, se genera el texto final reemplazando placeholders con la información registrada. El informe se muestra en pantalla.
* **Exportación**: el informe puede descargarse como **TXT** o **PDF**. La generación de PDF utiliza `jsPDF` cargado desde un CDN.
* **Persistencia local mínima**: la plantilla personalizada se guarda en `localStorage` para que se conserve entre sesiones.

## Cómo usar la aplicación

1. Abre `index.html` en un navegador compatible (por ejemplo, Chrome). Es posible habilitar la aplicación como PWA desde el navegador si se desea.
2. Pulsa **Iniciar Grabación** para empezar a dictar. La aplicación escuchará continuamente. Solo se registrarán las frases que correspondan al patrón:

   ```
   prueba de <nombre de prueba>, resultado <valor>
   ```

3. Para finalizar la sesión y generar el informe, di en voz alta "fin de evaluación" o pulsa el botón **Finalizar Evaluación**.
4. Usa el apartado de **Plantilla del Informe** para modificar el formato del texto final. Los placeholders permitidos se listan debajo del área de texto.
5. Después de generar el informe, utiliza los botones **Descargar TXT** o **Descargar PDF** para exportar el resultado.

## Limitaciones

* La API de reconocimiento de voz funciona con conexión a internet y depende del soporte del navegador. Para un uso completamente offline y con modelos personalizados sería necesario integrar un motor de STT local (p. ej. `whisper.cpp` o `Vosk`), lo cual escapa al alcance de esta implementación simplificada.
* El campo de **rol profesional**, **contexto** y **alias del paciente** no se capturan mediante la interfaz; se pueden dejar vacíos o adaptarse editando la plantilla manualmente.

## Estructura del repositorio

```
transcriphealt/
├── index.html   # Aplicación web principal (sin compilación)
├── README.md    # Este documento
```

## Instalación

Este proyecto no requiere dependencias externas ni proceso de compilación. Simplemente abre `index.html` en tu navegador. Para servirlo en producción puedes alojarlo en un hosting estático (como GitHub Pages) y la aplicación funcionará directamente.