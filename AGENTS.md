# Instrucciones del proyecto

## Objetivo
Este proyecto contiene los componentes para construir una aplicación de gestion de activos.
la carpeta dev es el entorno de desarrollo dentro de ella esta el proyecto Oracle Apex, en formato ApexLang, la carpeta prod es el entorno de producción, la Aplicación se llama ADRI, el sufijo indica el entorno.



## Entorno
- Oracle APEX: [26.1.2].
- Oracle Database: [19.0.0].
- Aplicación APEX: [ID y nombre].
- Páginas relacionadas con mapas: [números y nombres].
- Biblioteca de mapas: [APEX Maps / MapLibre ].
- Sistema de coordenadas: [por ejemplo, WGS 84 / EPSG:4326].
- Todas las tablas de la aplicación empiezan con el prefijo SGT_, a excepción de la tabla AUDIT_MASTER y AUDIT_DETAIL 
- Se namejan dos WORKSPACE'S de oracle Apex, el de desarrollo es DTE_SC y el de producción es DTESC_PROD. 

## Estructura
- [db/dev]: Todos los objetos de la base de datos de desarrollo.
      |_ [dev.describe.md]: Contiene la descripción de todos los objetos de la db en desarrollo. 
- [db/prod]: Todos los objetos de la base de datos en producción.
      |_ [prod.describe.md]: Contiene la descripción de todos los objetos de la db en Producción.
- [docs]: Toda la información de la  implementación de la Aplicación:  realizados, en curso y pendientes. 
- [pages]: Todas las páginas APEX de la aplicación.
- [shared-components]: Componentes compartidos en APEX, archivos estaticos, themas.
- [supporting-objects]: scripts SQL para instalar la App, cargar datos, o actualizar objetos de la base de datos.
- [deployments]: datos para despliegue de Apex, indica el ID de la App.

Consultar los archivos existentes antes de asumir esta estructura.

## Forma de trabajar
- Responder y documentar en español.
- Revisar la implementación existente antes de modificarla.
- Mantener los cambios centrados en la tarea solicitada.
- No reformatear archivos completos por cambios puntuales.
- Explicar qué cambió, cómo se verificó y qué queda pendiente.
- No asumir que el nombre de una carpeta indica la versión de APEX instalada.
- Cualquier cambio de la App se deberá realizar en la carpeta dev, una una de las carpetas con sufijo numérico, en caso que no se indique siempre preguntar a cual desarrollo se esta refiriendo.

## Convenciones de Oracle APEX
- Mantener los nombres existentes de items, regiones y acciones dinámicas.
- Usar identificadores estáticos para acceder a regiones desde JavaScript.
- Preferir las API públicas de APEX.
- Usar variables bind en SQL y PL/SQL cuando corresponda.
- Evitar valores fijos de aplicación, sesión, servidor o workspace.
- Conservar los mecanismos de autorización y protección de sesión.

## Convenciones de mapas
- Verificar el orden de coordenadas requerido por cada API.
- En GeoJSON, usar el orden longitud, latitud.
- Documentar el sistema de referencia y cualquier transformación.
- Manejar coordenadas nulas o inválidas sin romper el mapa.
- Escapar los datos mostrados en etiquetas y ventanas emergentes.
- Conservar filtros, selección y comportamiento de las capas,
  salvo que la tarea requiera cambiarlos.
- Considerar el rendimiento al cargar grandes cantidades de geometrías.

## Seguridad y datos
- No guardar contraseñas, tokens ni credenciales en el repositorio.
- No incluir datos sensibles en ejemplos, registros o capturas.
- No ejecutar cambios destructivos ni desplegar en producción
  sin autorización explícita.
- No modificar los archivos originales de datos geográficos
  si la tarea solo requiere consultarlos.

## Validación
- Ejecutar las comprobaciones disponibles y pertinentes al cambio.
- Para cambios visuales, comprobar cuando haya acceso al entorno:
  - Carga del mapa y de sus capas.
  - Filtros e interacción con elementos.
  - Etiquetas y ventanas emergentes.
  - Comportamiento con datos vacíos o coordenadas inválidas.
  - Consola del navegador sin errores nuevos.
- Si no hay acceso a APEX o a la base de datos, indicar qué
  se pudo verificar localmente y qué requiere prueba en el entorno.

## Entrega
- Resumir los archivos modificados y el motivo.
- Indicar las pruebas realizadas y sus resultados.
- Detallar los pasos manuales de importación o configuración necesarios.