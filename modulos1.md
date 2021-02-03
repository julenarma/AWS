# Módulos

## core.c :Esta directiva controla si las peticiones que contienen información de path añadida a continuación de un nombre de fichero existente serán aceptadas o rechazadas.

## mod_log_config.c: Con este módulo puede configurar el aspecto de los archivos de registro de Apache. Este módulo está habilitado por defecto.

## mod_logio.c: Registro del número de bytes recibidos y enviados en cada respuesta.

## prefork.c: El módulo MPM prefork implementa un servidor Web sin hilos y previo a la bifurcación. Hace que el servidor Web se comporte de manera similar a la versión 1.x de Apache en el sentido en que aísla cada petición y la gestiona bifurcando un proceso hijo independiente. Por lo tanto, las peticiones problemáticas no pueden afectar a otras, lo que evita el bloqueo del servidor Web.

## https_core.c: Carga el protocolo https.

## mod_so.c: Carga los demas modulos en el inicio y parada del servidor


## Comprobaciones de estado




![Comprobación estado](https://github.com/julenarma/AWS/blob/main/Imagenes/Modulos/1.JPG?raw=true)
