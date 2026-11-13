 # Pendientes de comparación entre desarrollo y producción

 Comparación realizada entre [db.describe.md](../dev/db.describe.md) y [prod.describe.md](./prod.describe.md).

 ## Resumen

 - Objetos descritos en desarrollo: **72**.
 - Objetos descritos en producción: **43**.
 - Objetos presentes en desarrollo y ausentes en producción: **29**.
 - Objetos presentes en producción y ausentes en desarrollo: **0**.
 - Las diferencias de producción que no tengan correspondencia en desarrollo deben marcarse como **NECESITA VERIFICAR** antes de modificar desarrollo o producción. En esta comparación no se encontraron objetos en esa condición.

 ## Objetos de desarrollo ausentes en producción

 **Pendiente: verificar si deben incorporarse a producción y revisar dependencias, datos y scripts de despliegue.**

 ### Tablas

 - `SGT_CAT_OT_ESTADO`
 - `SGT_CAT_OT_PRIORIDAD`
 - `SGT_CAT_OT_TIPO_TRABAJO`
 - `SGT_CAT_TIPO_ACCION_EVENTO`
 - `SGT_CAT_TIPO_ACTIVO_EVENTO`
 - `SGT_CEO_ELEMENTOS`
 - `SGT_EVENTOS_FO`
 - `SGT_EVENTO_ACCION`
 - `SGT_EVENTO_ACTIVO`
 - `SGT_EVENTO_COMENTARIO`
 - `SGT_EVENTO_EVIDENCIA`
 - `SGT_EVENTO_OPERATIVO`
 - `SGT_EVENTO_SUBTAREA`
 - `SGT_OT`
 - `SGT_OT_ASIGNACION`
 - `SGT_OT_HISTORIAL`
 - `SGT_OT_NOTIFICACION`
 - `SGT_OT_SERVICIO`
 - `SGT_TAREA`
 - `SGT_TRAZADOS_FO`

 ### Vistas

 - `V_ARCHIVOS_ENTIDADES`
 - `V_AUDIT_ENLACES_FO`
 - `V_AUDIT_INTERFACES`
 - `V_AUDIT_RACKS`
 - `V_AUDIT_SALAS`
 - `V_AUDIT_SITIOS`
 - `V_LEGAJO_ACTIVO`
 - `V_OT_TOPOLOGIA_SERVICIO`
 - `V_TAREA`

 ## Diferencias estructurales en objetos compartidos

 Todas las siguientes diferencias quedan con estado **NECESITA VERIFICAR**. No se debe aplicar automáticamente ninguna modificación hasta confirmar cuál ambiente representa la definición correcta.

 ### `SGT_ARCHIVOS`

 - Desarrollo: `ENTIDAD NUMBER(38)` y `ESTADO NUMBER(38)`.
 - Producción: `ENTIDAD NUMBER` y `ESTADO NUMBER`.
 - **NECESITA VERIFICAR:** confirmar si la precisión explícita `NUMBER(38)` es requerida.

 ### `SGT_EQUIPOS`

 - `TIPO_EQUIPO_ID`: desarrollo `NOT NULL`; producción nullable.
 - `SITIO_ID`: desarrollo nullable; producción `NOT NULL`.
 - **NECESITA VERIFICAR:** validar datos existentes y reglas funcionales antes de modificar restricciones.

 ### `SGT_INTERFACES`

 - Desarrollo contiene `VELOCIDAD_MBPS` y también `VELOCIDAD_MPBS`.
 - Producción contiene solamente `VELOCIDAD_MBPS`.
 - **NECESITA VERIFICAR:** `VELOCIDAD_MPBS` parece una columna duplicada por error tipográfico; confirmar dependencias antes de eliminarla o crearla en producción.

 ### `SGT_SALAS`

 - Desarrollo: `SIGLAS` y `NOMBRE` son nullable.
 - Producción: `SIGLAS` y `NOMBRE` son `NOT NULL`.
 - **NECESITA VERIFICAR:** comprobar filas con valores nulos y confirmar la regla de obligatoriedad.

 ### `SGT_TIPO_INTERFAZ`

 - Desarrollo: `NOMBRE VARCHAR2(64) NOT NULL`.
 - Producción: `NOMBRE VARCHAR2(255) NOT NULL`.
 - **NECESITA VERIFICAR:** confirmar la longitud objetivo y revisar dependencias de la aplicación.

 ### `V_AUDIT_EQUIPOS`

 - `AUDIT_ID`: desarrollo `NOT NULL`; producción nullable.
 - `TABLA_ORIGEN`: desarrollo `CHAR(11)`; producción `VARCHAR2(14)`.
 - `TIPO_COMPONENTE`: desarrollo `CHAR(16)`; producción `VARCHAR2(16)`.
 - Producción contiene además `REGISTRO_ID` y `FECHA_HORA_FILTRO`, ausentes en desarrollo.
 - **NECESITA VERIFICAR:** revisar la consulta de la vista y sus consumidores en APEX.

 ### `V_TRAMOS_NOMBRES`

 - Desarrollo declara `EQUIPO_A_ID` y `EQUIPO_B_ID` como `NOT NULL`.
 - Producción no marca esas dos columnas como `NOT NULL`.
 - **NECESITA VERIFICAR:** confirmar si la obligatoriedad procede de la vista o de las tablas base.

 ### `V_ZONAS_VISTA_GENERAL`

 - Desarrollo: `SALA_NOMBRE` y `SALA_SIGLAS` son nullable.
 - Producción: `SALA_NOMBRE` y `SALA_SIGLAS` son `NOT NULL`.
 - **NECESITA VERIFICAR:** revisar la consulta de la vista y el origen de la nulabilidad.

 ## Diferencias de nombres de restricciones e índices

 Se observaron nombres distintos para índices únicos generados por Oracle, aunque la clave o unicidad descrita es equivalente. **NECESITA VERIFICAR** solamente si algún script, vista, proceso de mantenimiento o herramienta referencia estos nombres literalmente.

 Objetos afectados:

 - `AUDIT_DETAIL`
 - `AUDIT_MASTER`
 - `SGT_CIUDAD`
 - `SGT_CONEXIONES_ENLACE_WAN`
 - `SGT_CONEXIONES_SERVICIO`
 - `SGT_DEPTO`
 - `SGT_ENLACES_FO`
 - `SGT_ENLACES_TRAMOS`
 - `SGT_ENLACES_WAN`
 - `SGT_ENLACES_WAN_SERVICIO`
 - `SGT_EQUIPOS`
 - `SGT_INTERFACES`
 - `SGT_INTERFACES_L2`
 - `SGT_INTERFACES_L3`
 - `SGT_IP_ADM`
 - `SGT_RACKS`
 - `SGT_SALAS`
 - `SGT_SERVICIOS`
 - `SGT_SITIOS`
 - `SGT_TIPO_CABLE`
 - `SGT_TIPO_EQUIPOS`
 - `SGT_TIPO_INTERFAZ`
 - `SGT_TIPO_WAN`
 - `SGT_ZONAS`

 ## Objetos presentes en producción y ausentes en desarrollo

 **Resultado: ninguno identificado.** Si una próxima comparación encuentra objetos en esta sección, deben marcarse como **NECESITA VERIFICAR** y no eliminarse ni replicarse automáticamente.

 ## Próximos pasos

 1. Confirmar si los 29 objetos exclusivos de desarrollo deben formar parte del alcance productivo.
 2. Validar las diferencias de nulabilidad, longitud y columnas de `SGT_EQUIPOS`, `SGT_INTERFACES`, `SGT_SALAS`, `SGT_TIPO_INTERFAZ` y las vistas indicadas.
 3. Comparar los scripts de `db/prod/ddl` y `db/dev/ddl` antes de generar cambios Liquibase.
 4. Ejecutar la validación contra las bases de datos, porque los archivos descriptivos no sustituyen una consulta directa al diccionario Oracle.
