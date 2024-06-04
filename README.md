

Detalle de las Tareas:
Inicializar variable errors

Descripción: Inicializa la variable errors como un diccionario vacío.
Módulo: set_fact
Detectar el sistema operativo

Descripción: Establece las variables os_family y os_version con la familia y versión del sistema operativo detectado.
Módulo: set_fact
Depurar información del sistema operativo

Descripción: Muestra un mensaje de depuración con la información del sistema operativo.
Módulo: debug
Obtener la lista de interfaces de red

Descripción: Ejecuta el comando ip -o link show para obtener la lista de interfaces de red.
Módulo: command
Registro: interfaces_output
Parsear las interfaces de red

Descripción: Extrae los nombres de las interfaces de red a partir de la salida del comando anterior.
Módulo: set_fact
Variable: interfaces
Depurar lista de interfaces de red

Descripción: Muestra un mensaje de depuración con la lista de interfaces encontradas.
Módulo: debug
Verificar errores y paquetes descartados

Descripción: Bloque de tareas que incluye la obtención y el análisis de estadísticas de errores y paquetes descartados.
Módulo: block
7.1. Obtener estadísticas de errores y paquetes descartados
- Descripción: Ejecuta el comando ip -s link show {{ item }} para cada interfaz para obtener estadísticas.
- Módulo: command
- Registro: interface_stats
- Bucle: {{ interfaces }}

7.2. Parsear estadísticas de errores y paquetes descartados
- Descripción: Extrae las estadísticas relevantes (paquetes recibidos, transmitidos, errores y descartes) y las guarda en parsed_stats.
- Módulo: set_fact
- Bucle: {{ interface_stats.results }}
- Condición: when: item.stdout is not search('errors:|dropped:')

7.3. Mostrar estadísticas de interfaces
- Descripción: Muestra un mensaje de depuración con las estadísticas parseadas.
- Módulo: debug

Mostrar estadísticas de interfaces con paquetes dropeados o mensaje de interfaz sin paquetes dropeados

Descripción: Muestra un mensaje indicando el estado de cada interfaz en términos de paquetes dropeados y errores de recepción/transmisión.
Módulo: debug
Bucle: {{ parsed_stats }}
