# S4D400 - Unit 4: Database Reading - Práctica Avanzada
## Lectura de Datos con SELECT - Tabla /DMO/CONNECTION

> **Objetivo**: Profundizar en operaciones de lectura de base de datos usando diferentes variaciones de SELECT.  
> **Tabla principal**: `/DMO/CONNECTION`  
> **Enfoque**: Código funcional completo con explicaciones concisas y precisas.  
> **Metodología**: Desarrollo incremental - cada método agrega funcionalidad al anterior.

---

## 📑 Tabla de Contenidos

- [Estándares de Nomenclatura](#-estándares-de-nomenclatura)
- [Estructura de la Tabla /DMO/CONNECTION](#-estructura-de-la-tabla-dmoconnection)
- [Método 1: get_single_connection](#método-1-get_single_connection)
- [Método 2: get_connections_by_carrier](#método-2-get_connections_by_carrier)
- [Método 3: get_connections_with_multiple_filters](#método-3-get_connections_with_multiple_filters)
- [Método 4: get_connections_with_operators](#método-4-get_connections_with_operators)
- [Método 5: get_all_connections](#método-5-get_all_connections)
- [Método 6: get_connections_with_carrier_name](#método-6-get_connections_with_carrier_name)
- [Método 7: get_connections_with_airport_names](#método-7-get_connections_with_airport_names)

---

## 📐 Estándares de Nomenclatura

Este documento sigue la **notación húngara adaptada a ABAP**, un estándar ampliamente utilizado en desarrollos SAP.

### Variables

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `lv_*` | Variable local (valor simple) | `lv_carrier_id`, `lv_count` |
| `gv_*` | Variable global (valor simple) | `gv_max_connections` |

### Estructuras

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `ls_*` | Estructura local | `ls_connection`, `ls_carrier` |
| `gs_*` | Estructura global | `gs_current_connection` |

### Tablas Internas

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `lt_*` | Tabla interna local | `lt_connections`, `lt_results` |
| `gt_*` | Tabla interna global | `gt_all_connections` |

### Constantes

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `lc_*` | Constante local | `lc_max_records`, `lc_carrier` |
| `gc_*` | Constante global | `gc_default_carrier` |

### Objetos (Referencias a Clases)

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `lo_*` | Objeto local | `lo_reader`, `lo_processor` |
| `go_*` | Objeto global | `go_connection_manager` |

### Parámetros de Métodos

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `iv_*` | IMPORTING value (valor simple) | `iv_carrier_id` |
| `is_*` | IMPORTING structure | `is_connection_key` |
| `it_*` | IMPORTING table | `it_carrier_list` |
| `ev_*` | EXPORTING value | `ev_record_count` |
| `es_*` | EXPORTING structure | `es_connection` |
| `et_*` | EXPORTING table | `et_connections` |
| `cv_*` | CHANGING value | `cv_counter` |
| `cs_*` | CHANGING structure | `cs_connection` |
| `ct_*` | CHANGING table | `ct_connections` |
| `rv_*` | RETURNING value (valor simple) | `rv_distance` |
| `rs_*` | RETURNING structure | `rs_connection` |
| `rt_*` | RETURNING table | `rt_connections` |

### Otros Elementos

| Prefijo | Descripción | Ejemplo |
|---------|-------------|---------|
| `lcl_*` | Clase local | `lcl_connection_reader` |
| `zcl_*` | Clase global (Z custom) | `zcl_##_db_practice` |
| `lo_*` | Objeto (instancia local) | `lo_reader` |
| `go_*` | Objeto (instancia global) | `go_manager` |
| `lr_*` | Referencia local (REF TO) | `lr_data_ref` |
| `gr_*` | Referencia global | `gr_shared_ref` |
| `<fs_*>` | Field-symbol | `<fs_connection>` |
| `ty_*` | Tipo local | `ty_connection_range` |
| `gty_*` | Tipo global | `gty_connection_table` |

### Nombres de Métodos

| Patrón | Propósito | Ejemplo |
|--------|-----------|---------|
| `get_*` | Obtener/Leer datos | `get_single_connection` |
| `set_*` | Establecer/Asignar datos | `set_connection_status` |
| `process_*` | Procesar datos | `process_connections` |
| `validate_*` | Validar datos | `validate_carrier_code` |
| `calculate_*` | Calcular valores | `calculate_distance` |

---

## 📊 Estructura de la Tabla /DMO/CONNECTION

### Descripción
Tabla que almacena las conexiones (rutas) disponibles entre aeropuertos para cada aerolínea en el modelo de datos Flight Reference Scenario.

### Campos (Columnas)

| Campo | Tipo de Dato | KEY | Descripción | Ejemplo |
|-------|--------------|-----|-------------|---------|
| `CLIENT` | MANDT | ✓ | Mandante (cliente) | 100 |
| `CARRIER_ID` | /DMO/CARRIER_ID | ✓ | Código de aerolínea | 'AA', 'LH', 'SQ' |
| `CONNECTION_ID` | /DMO/CONNECTION_ID | ✓ | ID de conexión (4 dígitos) | '0017', '0400' |
| `AIRPORT_FROM_ID` | /DMO/AIRPORT_FROM_ID | | Aeropuerto origen (3 letras) | 'JFK', 'FRA' |
| `AIRPORT_TO_ID` | /DMO/AIRPORT_TO_ID | | Aeropuerto destino (3 letras) | 'SFO', 'LAX' |
| `DEPARTURE_TIME` | /DMO/FLIGHT_DEPARTURE_TIME | | Hora de salida | '10:30:00' |
| `ARRIVAL_TIME` | /DMO/FLIGHT_ARRIVAL_TIME | | Hora de llegada | '14:45:00' |
| `DISTANCE` | /DMO/FLIGHT_DISTANCE | | Distancia en km/mi | 4135.00 |
| `DISTANCE_UNIT` | /DMO/DISTANCE_UNIT | | Unidad de distancia | 'KM', 'MI' |

### Clave Primaria
La clave primaria está compuesta por:
- `CLIENT` (implícito - manejado automáticamente por el sistema)
- `CARRIER_ID` (código de aerolínea)
- `CONNECTION_ID` (identificador único de conexión)

**Nota**: El campo CLIENT no debe especificarse en la cláusula WHERE, ya que el sistema lo maneja automáticamente.

### Ejemplo de Registros

| CARRIER_ID | CONNECTION_ID | AIRPORT_FROM_ID | AIRPORT_TO_ID | DISTANCE | DISTANCE_UNIT |
|------------|---------------|-----------------|---------------|----------|---------------|
| AA | 0017 | JFK | SFO | 4135.00 | KM |
| LH | 0400 | FRA | JFK | 6162.00 | KM |
| LH | 0401 | FRA | SFO | 9090.00 | KM |
| SQ | 0001 | SIN | SFO | 13593.00 | KM |
| UA | 0900 | SFO | FRA | 9090.00 | KM |

### Relaciones con Otras Tablas

| Tabla Relacionada | Campo de Unión | Descripción |
|-------------------|----------------|-------------|
| `/DMO/CARRIER` | `CARRIER_ID` | Información de la aerolínea (nombre, moneda) |
| `/DMO/AIRPORT` | `AIRPORT_FROM_ID` | Información del aeropuerto origen |
| `/DMO/AIRPORT` | `AIRPORT_TO_ID` | Información del aeropuerto destino |
| `/DMO/FLIGHT` | `CARRIER_ID + CONNECTION_ID` | Vuelos específicos con fechas y precios |

---

## Método 1: get_single_connection

### 🎯 Objetivo
Leer **UN SOLO** registro de la tabla usando su clave completa (carrier_id + connection_id).

---

### 📝 Código Completo - Versión 1

En esta primera versión, la clase tiene únicamente el método `get_single_connection`.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    " Leer un solo registro con clave exacta
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
    " Si sy-subrc <> 0, rs_connection queda INITIAL
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE`

```abap
CLASS zcl_##_db_practice DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_db_practice IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA lo_reader            TYPE REF TO lcl_connection_reader.
    DATA ls_single_connection TYPE /dmo/connection.
    
    " Instanciar clase local
    "**************************
    lo_reader = NEW #( ).
    
    " Método 1: Leer una conexión específica
    "**************************
    out->write( |--- MÉTODO 1: SELECT SINGLE ---| ).
    out->write( |Buscar: Carrier='AA', Connection='0017'| ).
    out->write( | | ).
    
    ls_single_connection = lo_reader->get_single_connection(
      iv_carrier_id    = 'AA'
      iv_connection_id = '0017'
    ).
    
    IF ls_single_connection IS NOT INITIAL.
      out->write( '✓ Conexión encontrada:' ).
      out->write( ls_single_connection ).
    ELSE.
      out->write( '✗ No se encontró la conexión' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### SELECT SINGLE
```abap
SELECT SINGLE
  FROM /dmo/connection
  FIELDS *
  WHERE ...
  INTO @rs_connection.
```

**Características**:
- Lee **máximo 1 registro** de la base de datos
- Si encuentra varios que cumplan la condición, toma el primero
- Más eficiente que SELECT normal cuando solo necesitas 1
- Retorna una **estructura**, no una tabla
- Ideal cuando buscas por clave primaria completa

**¿Cuándo usar?**
- Búsqueda por clave primaria
- Solo necesitas un registro
- Verificar existencia de un registro

#### FIELDS *
```abap
FIELDS *
```

**Significado**:
- `*`: Lee **todos los campos** de la tabla
- Equivalente a listar todos los campos manualmente

**Alternativa (Recomendada en Producción)**:
```abap
FIELDS carrier_id, connection_id, airport_from_id, airport_to_id
```

**Ventajas de especificar campos**:
- Más eficiente (menos datos transferidos)
- Código más claro y mantenible
- Mejor rendimiento en tablas grandes

#### WHERE con AND
```abap
WHERE carrier_id    = @iv_carrier_id
  AND connection_id = @iv_connection_id
```

**Características**:
- Combina múltiples condiciones con **AND**
- **Todas** las condiciones deben cumplirse
- Orden de las condiciones no importa para el resultado
- Usa la clave completa para búsqueda óptima

**Operadores disponibles**:
- `=`: Igual
- `<>`: Diferente
- `>`, `<`, `>=`, `<=`: Comparaciones
- `IN`: Dentro de un rango
- `LIKE`: Coincidencia de patrón

#### INTO @variable
```abap
INTO @rs_connection
```

**Características**:
- `@`: Prefijo obligatorio para variables en SQL moderno
- `rs_connection`: Estructura de tipo `/dmo/connection`
- Si no encuentra: La estructura queda INITIAL (vacía)
- Prefijo `rs_`: Returning Structure (estándar de nomenclatura)

**Verificación de resultado**:
```abap
IF rs_connection IS NOT INITIAL.
  " Registro encontrado
ELSE.
  " No encontrado
ENDIF.
```

#### sy-subrc (No usado aquí)
```abap
" No es necesario verificar sy-subrc en este caso
" Mejor usar: IF rs_connection IS NOT INITIAL
```

**¿Por qué no usar sy-subrc?**
- Si no encuentra: `rs_connection` queda INITIAL
- Verificar `IS NOT INITIAL` es más directo
- sy-subrc es útil en operaciones más complejas

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA ls_connection TYPE /dmo/connection.
DATA lo_reader     TYPE REF TO lcl_connection_reader.
DATA lv_distance   TYPE /dmo/flight_distance.

" Crear instancia
lo_reader = NEW #( ).

" Buscar conexión específica
ls_connection = lo_reader->get_single_connection(
  iv_carrier_id    = 'LH'
  iv_connection_id = '0400'
).

" Procesar resultado
IF ls_connection IS NOT INITIAL.
  
  WRITE: / 'Conexión encontrada:'.
  WRITE: / 'Aerolínea:', ls_connection-carrier_id.
  WRITE: / 'De:', ls_connection-airport_from_id.
  WRITE: / 'A:', ls_connection-airport_to_id.
  
  " Calcular algo con los datos
  lv_distance = ls_connection-distance.
  WRITE: / 'Distancia:', lv_distance, ls_connection-distance_unit.
  
ELSE.
  WRITE: / 'ERROR: Conexión no encontrada en la base de datos'.
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `iv_carrier_id = 'AA'`
- `iv_connection_id = '0017'`

**Output en Consola**:
```
--- MÉTODO 1: SELECT SINGLE ---
Buscar: Carrier='AA', Connection='0017'
 
✓ Conexión encontrada:
CLIENT: 100
CARRIER_ID: AA
CONNECTION_ID: 0017
AIRPORT_FROM_ID: JFK
AIRPORT_TO_ID: SFO
DEPARTURE_TIME: 10:30:00
ARRIVAL_TIME: 19:50:00
DISTANCE: 4135.00
DISTANCE_UNIT: KM
```

**Si no existe el registro**:
```
--- MÉTODO 1: SELECT SINGLE ---
Buscar: Carrier='XX', Connection='9999'
 
✗ No se encontró la conexión
```

---

## Método 2: get_connections_by_carrier

### 🎯 Objetivo
Leer **MÚLTIPLES** registros que cumplan una condición específica (todas las conexiones de una aerolínea).

---

### 📝 Código Completo - Versión 2

En esta segunda versión, agregamos el método `get_connections_by_carrier` **sin eliminar** el método anterior.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    " Leer un solo registro con clave exacta
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
    " Si sy-subrc <> 0, rs_connection queda INITIAL
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    " Leer múltiples registros con una condición
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
    " Si no encuentra registros, rt_connections queda vacía
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE`

```abap
CLASS zcl_##_db_practice DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_db_practice IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA lo_reader              TYPE REF TO lcl_connection_reader.
    DATA ls_single_connection   TYPE /dmo/connection.
    DATA lt_carrier_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lv_connection_count    TYPE i.
    DATA ls_connection          TYPE /dmo/connection.
    
    " Instanciar clase local
    "**************************
    lo_reader = NEW #( ).
    
    
    " Método 1: Leer una conexión específica
    "**************************
    out->write( |--- MÉTODO 1: SELECT SINGLE ---| ).
    out->write( |Buscar: Carrier='AA', Connection='0017'| ).
    out->write( | | ).
    
    ls_single_connection = lo_reader->get_single_connection(
      iv_carrier_id    = 'AA'
      iv_connection_id = '0017'
    ).
    
    IF ls_single_connection IS NOT INITIAL.
      out->write( '✓ Conexión encontrada:' ).
      out->write( ls_single_connection ).
    ELSE.
      out->write( '✗ No se encontró la conexión' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 2: Leer múltiples conexiones por aerolínea
    "**************************
    out->write( |--- MÉTODO 2: SELECT con WHERE simple ---| ).
    out->write( |Buscar: Todas las conexiones de Carrier='LH'| ).
    out->write( | | ).
    
    lt_carrier_connections = lo_reader->get_connections_by_carrier(
      iv_carrier_id = 'LH'
    ).
    
    lv_connection_count = lines( lt_carrier_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( | | ).
      
      " Mostrar resumen de cada conexión
      LOOP AT lt_carrier_connections INTO ls_connection.
        out->write( |  { ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### SELECT (sin SINGLE)
```abap
SELECT
  FROM /dmo/connection
  FIELDS *
  WHERE carrier_id = @iv_carrier_id
  INTO TABLE @rt_connections.
```

**Características**:
- Lee **todos los registros** que cumplan la condición
- Resultado: 0, 1 o N registros
- Retorna una **internal table**, no una estructura
- Más costoso que SINGLE si solo necesitas 1

**Diferencia con SELECT SINGLE**:

| Aspecto | SELECT SINGLE | SELECT |
|---------|---------------|--------|
| Registros leídos | Máximo 1 | 0 a N |
| Destino | Estructura (`ls_*`) | Tabla interna (`lt_*`) |
| INTO | `INTO @estructura` | `INTO TABLE @tabla` |
| Rendimiento | Más rápido | Más lento |
| Uso típico | Búsqueda por clave | Búsqueda con filtros |

#### INTO TABLE
```abap
INTO TABLE @rt_connections
```

**Características**:
- `INTO TABLE`: Destino es una **internal table**
- `@rt_connections`: Tipo `STANDARD TABLE OF /dmo/connection`
- Si no encuentra: La tabla queda **vacía** (no es un error)
- Prefijo `rt_`: Returning Table (estándar de nomenclatura)

**Declaración del tipo**:
```abap
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
```

#### Verificar Resultados

**Opción 1: IS INITIAL**
```abap
IF lt_connections IS INITIAL.
  " Tabla vacía - no se encontraron registros
ELSE.
  " Hay al menos un registro
ENDIF.
```

**Opción 2: lines( tabla )**
```abap
DATA lv_count TYPE i.

lv_count = lines( lt_connections ).

IF lv_count = 0.
  " No hay registros
ELSEIF lv_count = 1.
  " Un solo registro
ELSE.
  " Múltiples registros
  out->write( |Se encontraron { lv_count } registros| ).
ENDIF.
```

**Opción 3: Verificar en LOOP**
```abap
LOOP AT lt_connections INTO ls_connection.
  " Si entra al loop, hay registros
  " Procesar ls_connection
ENDLOOP.

IF sy-subrc <> 0.
  " No entró al loop - tabla vacía
ENDIF.
```

#### WHERE con una condición
```abap
WHERE carrier_id = @iv_carrier_id
```

**Características**:
- Solo una condición (sin AND)
- Busca **todos** los registros con ese carrier_id
- Filtra por un campo que NO es la clave completa
- Puede retornar muchos registros

**Equivalente SQL**:
```sql
SELECT * FROM /dmo/connection 
WHERE carrier_id = 'LH';
```

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA ls_connection  TYPE /dmo/connection.
DATA lo_reader      TYPE REF TO lcl_connection_reader.
DATA lv_total_dist  TYPE /dmo/flight_distance.
DATA lv_count       TYPE i.

" Crear instancia
lo_reader = NEW #( ).

" Obtener todas las conexiones de Lufthansa
lt_connections = lo_reader->get_connections_by_carrier(
  iv_carrier_id = 'LH'
).

" Verificar si se encontraron registros
lv_count = lines( lt_connections ).

IF lv_count > 0.
  
  WRITE: / |Conexiones de LH: { lv_count }|.
  WRITE: / |-------------------------------------|.
  
  " Procesar cada conexión
  LOOP AT lt_connections INTO ls_connection.
    
    WRITE: / |{ sy-tabix }. |,
             |{ ls_connection-connection_id } |,
             |{ ls_connection-airport_from_id } → |,
             |{ ls_connection-airport_to_id } |,
             |({ ls_connection-distance } { ls_connection-distance_unit })|.
    
    " Acumular distancia total
    lv_total_dist = lv_total_dist + ls_connection-distance.
    
  ENDLOOP.
  
  WRITE: / |-------------------------------------|.
  WRITE: / |Distancia total: { lv_total_dist } KM|.
  
ELSE.
  WRITE: / 'No se encontraron conexiones para esa aerolínea'.
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `iv_carrier_id = 'LH'`

**Output en Consola**:
```
--- MÉTODO 1: SELECT SINGLE ---
Buscar: Carrier='AA', Connection='0017'
 
✓ Conexión encontrada:
CLIENT: 100
CARRIER_ID: AA
CONNECTION_ID: 0017
AIRPORT_FROM_ID: JFK
AIRPORT_TO_ID: SFO
DEPARTURE_TIME: 10:30:00
ARRIVAL_TIME: 19:50:00
DISTANCE: 4135.00
DISTANCE_UNIT: KM
 

--- MÉTODO 2: SELECT con WHERE simple ---
Buscar: Todas las conexiones de Carrier='LH'
 
✓ Conexiones encontradas: 5
 
  0400: FRA → JFK (6162 KM)
  0401: FRA → SFO (9090 KM)
  0402: FRA → LAX (9481 KM)
  2402: FRA → GRU (9883 KM)
  2403: FRA → BUE (11845 KM)
```

**Si no existen registros**:
```
--- MÉTODO 2: SELECT con WHERE simple ---
Buscar: Todas las conexiones de Carrier='XX'
 
✗ No se encontraron conexiones
```

---

### 🔄 Comparación: Método 1 vs Método 2

| Aspecto | Método 1 (SINGLE) | Método 2 (Múltiple) |
|---------|-------------------|---------------------|
| **Objetivo** | Buscar 1 conexión específica | Buscar todas las conexiones de una aerolínea |
| **SELECT** | SELECT SINGLE | SELECT |
| **WHERE** | 2 condiciones (clave completa) | 1 condición (carrier) |
| **INTO** | INTO @estructura | INTO TABLE @tabla |
| **Retorno** | Estructura (ls_*) | Tabla interna (lt_*) |
| **Registros** | 0 o 1 | 0 a N |
| **Parámetro** | rs_connection | rt_connections |
| **Verificación** | IS NOT INITIAL | lines( tabla ) > 0 |
| **Procesamiento** | Acceso directo a campos | LOOP AT tabla |

---

**Continuará con Métodos 3-7 en siguientes secciones...**

---

## Método 3: get_connections_with_multiple_filters

### 🎯 Objetivo
Leer conexiones aplicando **MÚLTIPLES FILTROS** en la cláusula WHERE (más de una condición con AND).

---

### 📝 Código Completo - Versión 3

En esta tercera versión, agregamos el método `get_connections_with_multiple_filters` que demuestra el uso de múltiples condiciones WHERE.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 3: Leer con MÚLTIPLES filtros
    METHODS get_connections_with_multiple_filters
      IMPORTING
        iv_airport_from_id TYPE /dmo/airport_from_id
        iv_distance_min    TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    " Leer un solo registro con clave exacta
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    " Leer múltiples registros con una condición
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_multiple_filters.
    
    " Leer con múltiples condiciones combinadas
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE airport_from_id = @iv_airport_from_id
        AND distance        >= @iv_distance_min
      ORDER BY distance DESCENDING
      INTO TABLE @rt_connections.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE`

```abap
CLASS zcl_##_db_practice DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_db_practice IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA lo_reader              TYPE REF TO lcl_connection_reader.
    DATA ls_single_connection   TYPE /dmo/connection.
    DATA lt_carrier_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_filtered_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lv_connection_count    TYPE i.
    DATA ls_connection          TYPE /dmo/connection.
    
    " Instanciar clase local
    "**************************
    lo_reader = NEW #( ).
    
    
    " Método 1: Leer una conexión específica
    "**************************
    out->write( |--- MÉTODO 1: SELECT SINGLE ---| ).
    out->write( |Buscar: Carrier='AA', Connection='0017'| ).
    out->write( | | ).
    
    ls_single_connection = lo_reader->get_single_connection(
      iv_carrier_id    = 'AA'
      iv_connection_id = '0017'
    ).
    
    IF ls_single_connection IS NOT INITIAL.
      out->write( '✓ Conexión encontrada:' ).
      out->write( ls_single_connection ).
    ELSE.
      out->write( '✗ No se encontró la conexión' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 2: Leer múltiples conexiones por aerolínea
    "**************************
    out->write( |--- MÉTODO 2: SELECT con WHERE simple ---| ).
    out->write( |Buscar: Todas las conexiones de Carrier='LH'| ).
    out->write( | | ).
    
    lt_carrier_connections = lo_reader->get_connections_by_carrier(
      iv_carrier_id = 'LH'
    ).
    
    lv_connection_count = lines( lt_carrier_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( | | ).
      
      LOOP AT lt_carrier_connections INTO ls_connection.
        out->write( |  { ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 3: Leer con múltiples filtros
    "**************************
    out->write( |--- MÉTODO 3: SELECT con MÚLTIPLES filtros ---| ).
    out->write( |Buscar: Desde 'FRA' con distancia >= 9000 KM| ).
    out->write( | | ).
    
    lt_filtered_connections = lo_reader->get_connections_with_multiple_filters(
      iv_airport_from_id = 'FRA'
      iv_distance_min    = '9000'
    ).
    
    lv_connection_count = lines( lt_filtered_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( |  (Ordenadas por distancia - mayor a menor)| ).
      out->write( | | ).
      
      LOOP AT lt_filtered_connections INTO ls_connection.
        out->write( |  { sy-tabix }. { ls_connection-carrier_id }-{ ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones con esos criterios' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### WHERE con Múltiples Condiciones
```abap
WHERE airport_from_id = @iv_airport_from_id
  AND distance        >= @iv_distance_min
```

**Características**:
- Combina 2 o más condiciones con **AND**
- **Todas** las condiciones deben cumplirse simultáneamente
- Permite filtros más específicos y precisos
- Más condiciones = menor cantidad de resultados (más restrictivo)

**Operadores de Comparación**:
- `=`: Igual a
- `<>` o `!=`: Diferente de
- `>`: Mayor que
- `<`: Menor que
- `>=`: Mayor o igual que
- `<=`: Menor o igual que

#### ORDER BY
```abap
ORDER BY distance DESCENDING
```

**Características**:
- Ordena los resultados según un campo
- `ASCENDING` (ASC): De menor a mayor (por defecto)
- `DESCENDING` (DESC): De mayor a menor
- Se ejecuta **después** del WHERE (primero filtra, luego ordena)

**Múltiples campos de ordenamiento**:
```abap
ORDER BY carrier_id ASCENDING, distance DESCENDING
```

#### Parámetros de Entrada Múltiples
```abap
IMPORTING
  iv_airport_from_id TYPE /dmo/airport_from_id
  iv_distance_min    TYPE /dmo/flight_distance
```

**Características**:
- Método puede recibir varios parámetros
- Cada parámetro se usa en una condición WHERE diferente
- Mayor flexibilidad en las búsquedas
- Nomenclatura: `iv_*` (importing value)

#### Comparación de Filtros

**Método 2** (1 condición):
```abap
WHERE carrier_id = @iv_carrier_id
```
- Retorna: Todas las conexiones de una aerolínea

**Método 3** (2+ condiciones):
```abap
WHERE airport_from_id = @iv_airport_from_id
  AND distance >= @iv_distance_min
```
- Retorna: Solo las conexiones que cumplen AMBAS condiciones
- Resultado más específico y filtrado

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA ls_connection  TYPE /dmo/connection.
DATA lo_reader      TYPE REF TO lcl_connection_reader.
DATA lv_count       TYPE i.
DATA lv_avg_dist    TYPE /dmo/flight_distance.

lo_reader = NEW #( ).

" Buscar vuelos largos desde Frankfurt
lt_connections = lo_reader->get_connections_with_multiple_filters(
  iv_airport_from_id = 'FRA'
  iv_distance_min    = 9000
).

lv_count = lines( lt_connections ).

IF lv_count > 0.
  
  WRITE: / |Vuelos de larga distancia desde FRA: { lv_count }|.
  WRITE: / |-------------------------------------------------|.
  
  LOOP AT lt_connections INTO ls_connection.
    
    WRITE: / |{ sy-tabix }. { ls_connection-carrier_id } - |,
             |{ ls_connection-airport_to_id }: |,
             |{ ls_connection-distance } { ls_connection-distance_unit }|.
    
    " Acumular para promedio
    lv_avg_dist = lv_avg_dist + ls_connection-distance.
    
  ENDLOOP.
  
  " Calcular promedio
  lv_avg_dist = lv_avg_dist / lv_count.
  
  WRITE: / |-------------------------------------------------|.
  WRITE: / |Distancia promedio: { lv_avg_dist } KM|.
  
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `iv_airport_from_id = 'FRA'`
- `iv_distance_min = 9000`

**Output en Consola**:
```
--- MÉTODO 3: SELECT con MÚLTIPLES filtros ---
Buscar: Desde 'FRA' con distancia >= 9000 KM
 
✓ Conexiones encontradas: 4
  (Ordenadas por distancia - mayor a menor)
 
  1. LH-2403: FRA → BUE (11845 KM)
  2. LH-2402: FRA → GRU (9883 KM)
  3. LH-0402: FRA → LAX (9481 KM)
  4. LH-0401: FRA → SFO (9090 KM)
```

**Si no hay resultados**:
```
--- MÉTODO 3: SELECT con MÚLTIPLES filtros ---
Buscar: Desde 'JFK' con distancia >= 15000 KM
 
✗ No se encontraron conexiones con esos criterios
```

---

### 🔍 Caso de Uso Real

**Escenario**: Sistema de búsqueda de vuelos para agencia de viajes.

**Requerimiento**: 
"Mostrar todas las conexiones internacionales largas (>8000 km) que salen de Frankfurt, ordenadas de la más larga a la más corta"

**Solución**:
```abap
lt_long_flights = lo_reader->get_connections_with_multiple_filters(
  iv_airport_from_id = 'FRA'
  iv_distance_min    = 8000
).

" Mostrar en UI o procesar para cotización
LOOP AT lt_long_flights INTO ls_flight.
  " Calcular precio, disponibilidad, etc.
ENDLOOP.
```

---

## Método 4: get_connections_with_operators

### 🎯 Objetivo
Leer conexiones usando **DIFERENTES OPERADORES** en WHERE (<>, >, <, IN, BETWEEN) para filtros más complejos.

---

### 📝 Código Completo - Versión 4

En esta cuarta versión, agregamos el método `get_connections_with_operators` que demuestra el uso de operadores avanzados.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 3: Leer con MÚLTIPLES filtros
    METHODS get_connections_with_multiple_filters
      IMPORTING
        iv_airport_from_id TYPE /dmo/airport_from_id
        iv_distance_min    TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 4: Leer con OPERADORES avanzados
    METHODS get_connections_with_operators
      IMPORTING
        it_carrier_ids TYPE STANDARD TABLE OF /dmo/carrier_id
        iv_distance_max TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_multiple_filters.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE airport_from_id = @iv_airport_from_id
        AND distance        >= @iv_distance_min
      ORDER BY distance DESCENDING
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_operators.
    
    " Usar operadores: IN, <>, <
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    IN @it_carrier_ids
        AND distance      <  @iv_distance_max
        AND distance_unit <> 'MI'
      ORDER BY carrier_id, distance
      INTO TABLE @rt_connections.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE`

```abap
CLASS zcl_##_db_practice DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_db_practice IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA lo_reader               TYPE REF TO lcl_connection_reader.
    DATA ls_single_connection    TYPE /dmo/connection.
    DATA lt_carrier_connections  TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_filtered_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_operator_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_carrier_ids          TYPE STANDARD TABLE OF /dmo/carrier_id.
    DATA lv_connection_count     TYPE i.
    DATA ls_connection           TYPE /dmo/connection.
    DATA lv_carrier_id           TYPE /dmo/carrier_id.
    
    " Instanciar clase local
    "**************************
    lo_reader = NEW #( ).
    
    
    " Método 1: Leer una conexión específica
    "**************************
    out->write( |--- MÉTODO 1: SELECT SINGLE ---| ).
    out->write( |Buscar: Carrier='AA', Connection='0017'| ).
    out->write( | | ).
    
    ls_single_connection = lo_reader->get_single_connection(
      iv_carrier_id    = 'AA'
      iv_connection_id = '0017'
    ).
    
    IF ls_single_connection IS NOT INITIAL.
      out->write( '✓ Conexión encontrada:' ).
      out->write( ls_single_connection ).
    ELSE.
      out->write( '✗ No se encontró la conexión' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 2: Leer múltiples conexiones por aerolínea
    "**************************
    out->write( |--- MÉTODO 2: SELECT con WHERE simple ---| ).
    out->write( |Buscar: Todas las conexiones de Carrier='LH'| ).
    out->write( | | ).
    
    lt_carrier_connections = lo_reader->get_connections_by_carrier(
      iv_carrier_id = 'LH'
    ).
    
    lv_connection_count = lines( lt_carrier_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( | | ).
      
      LOOP AT lt_carrier_connections INTO ls_connection.
        out->write( |  { ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 3: Leer con múltiples filtros
    "**************************
    out->write( |--- MÉTODO 3: SELECT con MÚLTIPLES filtros ---| ).
    out->write( |Buscar: Desde 'FRA' con distancia >= 9000 KM| ).
    out->write( | | ).
    
    lt_filtered_connections = lo_reader->get_connections_with_multiple_filters(
      iv_airport_from_id = 'FRA'
      iv_distance_min    = '9000'
    ).
    
    lv_connection_count = lines( lt_filtered_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( |  (Ordenadas por distancia - mayor a menor)| ).
      out->write( | | ).
      
      LOOP AT lt_filtered_connections INTO ls_connection.
        out->write( |  { sy-tabix }. { ls_connection-carrier_id }-{ ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones con esos criterios' ).
    ENDIF.
    
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    
    
    " Método 4: Leer con operadores avanzados
    "**************************
    out->write( |--- MÉTODO 4: SELECT con OPERADORES avanzados ---| ).
    
    " Preparar lista de carriers
    lv_carrier_id = 'AA'.
    APPEND lv_carrier_id TO lt_carrier_ids.
    lv_carrier_id = 'UA'.
    APPEND lv_carrier_id TO lt_carrier_ids.
    lv_carrier_id = 'DL'.
    APPEND lv_carrier_id TO lt_carrier_ids.
    
    out->write( |Buscar: Carriers IN ('AA','UA','DL'), distancia < 5000 KM, unidad <> 'MI'| ).
    out->write( | | ).
    
    lt_operator_connections = lo_reader->get_connections_with_operators(
      it_carrier_ids  = lt_carrier_ids
      iv_distance_max = '5000'
    ).
    
    lv_connection_count = lines( lt_operator_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( |  (Ordenadas por carrier y distancia)| ).
      out->write( | | ).
      
      LOOP AT lt_operator_connections INTO ls_connection.
        out->write( |  { sy-tabix }. { ls_connection-carrier_id }-{ ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } { ls_connection-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones con esos criterios' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### Operador IN
```abap
WHERE carrier_id IN @it_carrier_ids
```

**Características**:
- Verifica si el valor está **dentro de una lista**
- Equivalente a múltiples OR: `carrier_id = 'AA' OR carrier_id = 'UA' OR carrier_id = 'DL'`
- Más eficiente y legible que múltiples OR
- Acepta una **internal table** como parámetro

**Declaración de la tabla**:
```abap
DATA lt_carrier_ids TYPE STANDARD TABLE OF /dmo/carrier_id.
```

**Llenado de la tabla**:
```abap
DATA lv_carrier TYPE /dmo/carrier_id.

lv_carrier = 'AA'.
APPEND lv_carrier TO lt_carrier_ids.

lv_carrier = 'LH'.
APPEND lv_carrier TO lt_carrier_ids.
```

#### Operador <> (Diferente)
```abap
WHERE distance_unit <> 'MI'
```

**Características**:
- Excluye registros con ese valor
- Equivalente a: `!= 'MI'` (no recomendado en ABAP)
- Útil para filtrar datos no deseados
- Se puede combinar con otros operadores

**Alternativa**:
```abap
WHERE distance_unit = 'KM'  " Solo los que son KM
```

#### Operador < (Menor que)
```abap
WHERE distance < @iv_distance_max
```

**Operadores de comparación disponibles**:

| Operador | Significado | Ejemplo | Resultado |
|----------|-------------|---------|-----------|
| `=` | Igual a | `distance = 5000` | Exactamente 5000 |
| `<>` | Diferente de | `carrier <> 'LH'` | Todos excepto LH |
| `>` | Mayor que | `distance > 5000` | Más de 5000 |
| `<` | Menor que | `distance < 5000` | Menos de 5000 |
| `>=` | Mayor o igual | `distance >= 5000` | 5000 o más |
| `<=` | Menor o igual | `distance <= 5000` | 5000 o menos |

#### Combinación de Operadores
```abap
WHERE carrier_id    IN @it_carrier_ids
  AND distance      <  @iv_distance_max
  AND distance_unit <> 'MI'
```

**Características**:
- Se pueden combinar diferentes tipos de operadores
- Todas las condiciones deben cumplirse (AND)
- Filtros más específicos y potentes
- Cada condición se evalúa independientemente

#### ORDER BY con Múltiples Campos
```abap
ORDER BY carrier_id, distance
```

**Características**:
- Ordena primero por `carrier_id` (alfabéticamente)
- Dentro de cada carrier, ordena por `distance` (ascendente)
- Resultado: Agrupado por carrier y ordenado por distancia

**Equivalente**:
```abap
ORDER BY carrier_id ASCENDING, distance ASCENDING
```

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_carriers    TYPE STANDARD TABLE OF /dmo/carrier_id.
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA ls_connection  TYPE /dmo/connection.
DATA lo_reader      TYPE REF TO lcl_connection_reader.
DATA lv_carrier     TYPE /dmo/carrier_id.
DATA lv_count       TYPE i.

" Preparar lista de aerolíneas americanas
lv_carrier = 'AA'.
APPEND lv_carrier TO lt_carriers.
lv_carrier = 'UA'.
APPEND lv_carrier TO lt_carriers.
lv_carrier = 'DL'.
APPEND lv_carrier TO lt_carriers.

" Crear lector
lo_reader = NEW #( ).

" Buscar vuelos cortos de aerolíneas americanas
lt_connections = lo_reader->get_connections_with_operators(
  it_carrier_ids  = lt_carriers
  iv_distance_max = 4000
).

lv_count = lines( lt_connections ).

IF lv_count > 0.
  
  WRITE: / |Vuelos cortos (<4000 KM) de aerolíneas USA: { lv_count }|.
  WRITE: / |------------------------------------------------------|.
  
  LOOP AT lt_connections INTO ls_connection.
    
    WRITE: / |{ ls_connection-carrier_id } | &&
             |{ ls_connection-connection_id }: | &&
             |{ ls_connection-airport_from_id } → | &&
             |{ ls_connection-airport_to_id } | &&
             |({ ls_connection-distance } { ls_connection-distance_unit })|.
    
  ENDLOOP.
  
ELSE  
  WRITE: / 'No se encontraron vuelos con esos criterios'.
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `it_carrier_ids = ['AA', 'UA', 'DL']`
- `iv_distance_max = 5000`
- Excluir: `distance_unit = 'MI'`

**Output en Consola**:
```
--- MÉTODO 4: SELECT con OPERADORES avanzados ---
Buscar: Carriers IN ('AA','UA','DL'), distancia < 5000 KM, unidad <> 'MI'
 
✓ Conexiones encontradas: 6
  (Ordenadas por carrier y distancia)
 
  1. AA-0017: JFK → SFO (4135 KM)
  2. AA-0064: SFO → JFK (4135 KM)
  3. DL-0106: ATL → FRA (7330 KM)
  4. UA-0900: SFO → FRA (9090 KM)
  5. UA-0941: FRA → SFO (9090 KM)
```

---

### 🔍 Comparación de Operadores

| Método | Operadores Usados | Propósito |
|--------|-------------------|-----------|
| **Método 1** | `=` | Búsqueda exacta por clave |
| **Método 2** | `=` | Filtro simple por un campo |
| **Método 3** | `=`, `>=` | Filtros múltiples con comparación |
| **Método 4** | `IN`, `<`, `<>` | Filtros avanzados con listas y exclusiones |

---

### 🎯 Casos de Uso Real

**Escenario 1: Búsqueda de Vuelos Regionales**
```abap
" Aerolíneas europeas, distancias cortas
lt_euro_carriers = VALUE #( ( 'LH' ) ( 'AF' ) ( 'BA' ) ).

lt_regional = lo_reader->get_connections_with_operators(
  it_carrier_ids  = lt_euro_carriers
  iv_distance_max = 2000  " Vuelos cortos
).
```

**Escenario 2: Excluir Ciertos Carriers**
```abap
" Todas las aerolíneas EXCEPTO low-cost
WHERE carrier_id NOT IN ('RY', 'W6', 'U2')  " Ryanair, Wizz, easyJet
```

**Escenario 3: Rangos de Distancia**
```abap
" Vuelos de distancia media (3000-7000 km)
WHERE distance >= 3000
  AND distance <= 7000
```

---

## Método 5: get_all_connections

### 🎯 Objetivo
Leer **TODOS** los registros de la tabla **SIN FILTROS** (sin cláusula WHERE).

---

### 📝 Código Completo - Versión 5

En esta quinta versión, agregamos el método `get_all_connections` que lee toda la tabla sin restricciones.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 3: Leer con MÚLTIPLES filtros
    METHODS get_connections_with_multiple_filters
      IMPORTING
        iv_airport_from_id TYPE /dmo/airport_from_id
        iv_distance_min    TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 4: Leer con OPERADORES avanzados
    METHODS get_connections_with_operators
      IMPORTING
        it_carrier_ids TYPE STANDARD TABLE OF /dmo/carrier_id
        iv_distance_max TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 5: Leer TODOS los registros
    METHODS get_all_connections
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_multiple_filters.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE airport_from_id = @iv_airport_from_id
        AND distance        >= @iv_distance_min
      ORDER BY distance DESCENDING
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_operators.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    IN @it_carrier_ids
        AND distance      <  @iv_distance_max
        AND distance_unit <> 'MI'
      ORDER BY carrier_id, distance
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_all_connections.
    
    " Leer TODA la tabla sin filtros
    SELECT
      FROM /dmo/connection
      FIELDS carrier_id, connection_id, airport_from_id, airport_to_id, distance
      ORDER BY carrier_id, connection_id
      INTO CORRESPONDING FIELDS OF TABLE @rt_connections.
    
    " Nota: Se omiten campos innecesarios para optimizar rendimiento
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE` (parcial - solo nuevo código)

```abap
" ... (código anterior de métodos 1-4)

    " Método 5: Leer TODOS los registros
    "**************************
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    out->write( |--- MÉTODO 5: SELECT sin WHERE (TODA la tabla) ---| ).
    out->write( | | ).
    
    DATA lt_all_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lv_total_distance  TYPE /dmo/flight_distance.
    
    lt_all_connections = lo_reader->get_all_connections( ).
    
    lv_connection_count = lines( lt_all_connections ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Total de conexiones en la BD: { lv_connection_count }| ).
      out->write( | | ).
      
      " Mostrar solo las primeras 10 para no saturar la consola
      out->write( |  Primeras 10 conexiones:| ).
      
      LOOP AT lt_all_connections INTO ls_connection TO 10.
        out->write( |  { sy-tabix }. { ls_connection-carrier_id }-{ ls_connection-connection_id }: |
                 && |{ ls_connection-airport_from_id } → |
                 && |{ ls_connection-airport_to_id } |
                 && |({ ls_connection-distance } KM)| ).
      ENDLOOP.
      
      " Calcular estadísticas
      LOOP AT lt_all_connections INTO ls_connection.
        lv_total_distance = lv_total_distance + ls_connection-distance.
      ENDLOOP.
      
      out->write( | | ).
      out->write( |  ESTADÍSTICAS:| ).
      out->write( |  - Total conexiones: { lv_connection_count }| ).
      out->write( |  - Distancia total: { lv_total_distance } KM| ).
      out->write( |  - Distancia promedio: { lv_total_distance / lv_connection_count } KM| ).
      
    ELSE.
      out->write( '✗ La tabla está vacía' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### SELECT sin WHERE
```abap
SELECT
  FROM /dmo/connection
  FIELDS carrier_id, connection_id, airport_from_id, airport_to_id, distance
  INTO CORRESPONDING FIELDS OF TABLE @rt_connections.
```

**Características**:
- **NO hay cláusula WHERE** = Lee TODOS los registros
- Lee la **tabla completa** de la base de datos
- ⚠️ **PELIGRO**: En tablas grandes puede ser muy lento
- Solo usar cuando realmente necesitas todos los datos

**¿Cuándo usar?**:
- Tablas pequeñas de configuración
- Cargar datos para análisis completo
- Sincronización de datos
- Reportes de toda la información

**¿Cuándo NO usar?**:
- Tablas transaccionales grandes (millones de registros)
- Cuando solo necesitas un subconjunto
- En producción sin autorización

#### FIELDS Específicos (Optimización)
```abap
FIELDS carrier_id, connection_id, airport_from_id, airport_to_id, distance
```

**Ventajas vs FIELDS ***:
- **Mejor rendimiento**: Menos datos transferidos de BD
- **Menor uso de memoria**: Solo campos necesarios
- **Código más claro**: Se ve qué campos se usan
- **Optimización de red**: Menos tráfico entre BD y app

**Comparación**:

| Aspecto | FIELDS * | FIELDS específicos |
|---------|----------|-------------------|
| Rendimiento | Más lento | Más rápido |
| Memoria | Más consumo | Menos consumo |
| Mantenibilidad | Menos claro | Más claro |
| Uso recomendado | Solo en desarrollo/pruebas | Siempre en producción |

#### INTO CORRESPONDING FIELDS OF
```abap
INTO CORRESPONDING FIELDS OF TABLE @rt_connections
```

**Funcionalidad**:
- Mapea campos **por nombre**, no por posición
- Solo asigna campos que existen en ambos lados
- Ignora campos extra en SELECT o en tabla destino
- Útil cuando no lees todos los campos de la estructura

**Diferencia con INTO TABLE**:
```abap
" INTO TABLE normal - debe coincidir estructura exacta
INTO TABLE @rt_connections

" INTO CORRESPONDING FIELDS - mapea por nombre
INTO CORRESPONDING FIELDS OF TABLE @rt_connections
```

#### ORDER BY en Lecturas Completas
```abap
ORDER BY carrier_id, connection_id
```

**Importancia**:
- Sin ORDER BY, el orden es **impredecible**
- Cada ejecución puede dar orden diferente
- BD retorna en orden de almacenamiento interno
- **Siempre usar ORDER BY** para resultados consistentes

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_all_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA ls_connection      TYPE /dmo/connection.
DATA lo_reader          TYPE REF TO lcl_connection_reader.
DATA lv_count           TYPE i.
DATA lv_total_km        TYPE /dmo/flight_distance.
DATA lv_avg_km          TYPE /dmo/flight_distance.
DATA lv_max_distance    TYPE /dmo/flight_distance.
DATA lv_min_distance    TYPE /dmo/flight_distance VALUE 999999.

" Crear lector
lo_reader = NEW #( ).

" Leer TODA la tabla
lt_all_connections = lo_reader->get_all_connections( ).

lv_count = lines( lt_all_connections ).

IF lv_count > 0.
  
  WRITE: / |=== ANÁLISIS COMPLETO DE CONEXIONES ===|.
  WRITE: / | |.
  
  " Calcular estadísticas
  LOOP AT lt_all_connections INTO ls_connection.
    
    " Acumular distancia total
    lv_total_km = lv_total_km + ls_connection-distance.
    
    " Encontrar máxima distancia
    IF ls_connection-distance > lv_max_distance.
      lv_max_distance = ls_connection-distance.
    ENDIF.
    
    " Encontrar mínima distancia
    IF ls_connection-distance < lv_min_distance.
      lv_min_distance = ls_connection-distance.
    ENDIF.
    
  ENDLOOP.
  
  " Calcular promedio
  lv_avg_km = lv_total_km / lv_count.
  
  " Mostrar resultados
  WRITE: / |Total de conexiones: { lv_count }|.
  WRITE: / |Distancia total: { lv_total_km } KM|.
  WRITE: / |Distancia promedio: { lv_avg_km } KM|.
  WRITE: / |Distancia máxima: { lv_max_distance } KM|.
  WRITE: / |Distancia mínima: { lv_min_distance } KM|.
  
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Output en Consola**:
```
--- MÉTODO 5: SELECT sin WHERE (TODA la tabla) ---
 
✓ Total de conexiones en la BD: 123
 
  Primeras 10 conexiones:
  1. AA-0017: JFK → SFO (4135 KM)
  2. AA-0064: SFO → JFK (4135 KM)
  3. AF-0023: CDG → JFK (5836 KM)
  4. AZ-0555: FCO → JFK (6900 KM)
  5. BA-0001: LHR → JFK (5541 KM)
  6. DL-0106: ATL → FRA (7330 KM)
  7. LH-0400: FRA → JFK (6162 KM)
  8. LH-0401: FRA → SFO (9090 KM)
  9. LH-0402: FRA → LAX (9481 KM)
  10. LH-2402: FRA → GRU (9883 KM)
 
  ESTADÍSTICAS:
  - Total conexiones: 123
  - Distancia total: 745238 KM
  - Distancia promedio: 6058 KM
```

---

### ⚠️ Advertencias y Buenas Prácticas

#### 1. Rendimiento en Tablas Grandes

**❌ MAL - Sin límite**:
```abap
SELECT * FROM large_table INTO TABLE @lt_data.
" Si la tabla tiene 10 millones de registros = Crash
```

**✅ BIEN - Con límite**:
```abap
SELECT * FROM large_table 
  INTO TABLE @lt_data
  UP TO 1000 ROWS.
" Solo lee primeros 1000 registros
```

#### 2. Campos Específicos vs *

**❌ MAL en producción**:
```abap
SELECT * FROM /dmo/connection INTO TABLE @lt_data.
" Lee TODO, incluso campos no usados
```

**✅ BIEN en producción**:
```abap
SELECT carrier_id, connection_id, airport_from_id, airport_to_id
  FROM /dmo/connection INTO TABLE @lt_data.
" Solo campos necesarios
```

#### 3. Usar WHERE Siempre que sea Posible

**❌ MAL - Filtrar en ABAP**:
```abap
" Leer todo y filtrar en código
lt_all = lo_reader->get_all_connections( ).
LOOP AT lt_all INTO ls_conn WHERE carrier_id = 'LH'.
  " Procesar solo LH
ENDLOOP.
" Ineficiente: Lee TODO de BD, filtra en app
```

**✅ BIEN - Filtrar en BD**:
```abap
" Filtrar en la base de datos
lt_lh = lo_reader->get_connections_by_carrier( iv_carrier_id = 'LH' ).
" Eficiente: BD solo envía datos filtrados
```

#### 4. Ordenamiento

**❌ MAL - Sin ORDER BY**:
```abap
SELECT * FROM /dmo/connection INTO TABLE @lt_data.
" Orden impredecible
```

**✅ BIEN - Con ORDER BY**:
```abap
SELECT * FROM /dmo/connection 
  ORDER BY carrier_id, connection_id
  INTO TABLE @lt_data.
" Orden consistente y predecible
```

---

### 🔍 Comparación: Todos los Métodos (1-5)

| Método | WHERE | Parámetros | Registros | Uso Típico |
|--------|-------|------------|-----------|------------|
| **1** | Clave completa (2 campos) | 2 | 0 o 1 | Buscar 1 registro específico |
| **2** | 1 condición simple | 1 | 0 a N | Filtrar por 1 criterio |
| **3** | Múltiples condiciones (AND) | 2+ | 0 a N | Filtros combinados |
| **4** | Operadores avanzados (IN, <>, <) | 2+ | 0 a N | Búsquedas complejas |
| **5** | Sin WHERE | 0 | Todos | Análisis completo, reportes |

---

### 🎯 Caso de Uso Real

**Escenario**: Dashboard de análisis de red de rutas

**Requerimiento**: 
"Generar un reporte con estadísticas generales de todas las conexiones disponibles"

**Solución**:
```abap
" Cargar todas las conexiones
lt_all = lo_reader->get_all_connections( ).

" Analizar datos
lv_total_routes = lines( lt_all ).
lv_total_distance = SUM( lt_all-distance ).
lv_avg_distance = lv_total_distance / lv_total_routes.

" Generar gráficos
lo_chart->add_data(
  title = 'Conexiones Totales'
  value = lv_total_routes
).

lo_chart->add_data(
  title = 'Distancia Promedio'
  value = lv_avg_distance
).
```

---

**Continuará con Métodos 6-7 (con JOIN) en la siguiente sección...**

## Método 6: get_connections_with_carrier_name

### 🎯 Objetivo
Leer conexiones combinando datos de **DOS TABLAS** usando **INNER JOIN** para obtener el nombre de la aerolínea.

---

### 📝 Código Completo - Versión 6

En esta sexta versión, agregamos el método `get_connections_with_carrier_name` que utiliza INNER JOIN para combinar `/dmo/connection` con `/dmo/carrier`.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Tipo para resultado con nombre de carrier
    TYPES: BEGIN OF ty_connection_with_carrier,
             carrier_id      TYPE /dmo/carrier_id,
             carrier_name    TYPE /dmo/carrier_name,
             connection_id   TYPE /dmo/connection_id,
             airport_from_id TYPE /dmo/airport_from_id,
             airport_to_id   TYPE /dmo/airport_to_id,
             distance        TYPE /dmo/flight_distance,
             distance_unit   TYPE /dmo/distance_unit,
           END OF ty_connection_with_carrier.
    
    TYPES tt_connection_with_carrier TYPE STANDARD TABLE OF ty_connection_with_carrier.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 3: Leer con MÚLTIPLES filtros
    METHODS get_connections_with_multiple_filters
      IMPORTING
        iv_airport_from_id TYPE /dmo/airport_from_id
        iv_distance_min    TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 4: Leer con OPERADORES avanzados
    METHODS get_connections_with_operators
      IMPORTING
        it_carrier_ids TYPE STANDARD TABLE OF /dmo/carrier_id
        iv_distance_max TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 5: Leer TODOS los registros
    METHODS get_all_connections
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 6: Leer con INNER JOIN (nombre de carrier)
    METHODS get_connections_with_carrier_name
      IMPORTING
        iv_carrier_id TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_result) TYPE tt_connection_with_carrier.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_multiple_filters.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE airport_from_id = @iv_airport_from_id
        AND distance        >= @iv_distance_min
      ORDER BY distance DESCENDING
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_operators.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    IN @it_carrier_ids
        AND distance      <  @iv_distance_max
        AND distance_unit <> 'MI'
      ORDER BY carrier_id, distance
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_all_connections.
    
    SELECT
      FROM /dmo/connection
      FIELDS carrier_id, connection_id, airport_from_id, airport_to_id, distance
      ORDER BY carrier_id, connection_id
      INTO CORRESPONDING FIELDS OF TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_carrier_name.
    
    " INNER JOIN con tabla de carriers
    SELECT
      FROM /dmo/connection AS conn
      INNER JOIN /dmo/carrier AS car
        ON conn~carrier_id = car~carrier_id
      FIELDS conn~carrier_id,
             car~name AS carrier_name,
             conn~connection_id,
             conn~airport_from_id,
             conn~airport_to_id,
             conn~distance,
             conn~distance_unit
      WHERE conn~carrier_id = @iv_carrier_id
      ORDER BY conn~connection_id
      INTO TABLE @rt_result.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE` (parcial - solo nuevo código)

```abap
" ... (código anterior de métodos 1-5)

    " Método 6: Leer con INNER JOIN - Nombre de carrier
    "**************************
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    out->write( |--- MÉTODO 6: SELECT con INNER JOIN ---| ).
    out->write( |Buscar: Conexiones de 'LH' con nombre de aerolínea| ).
    out->write( | | ).
    
    DATA lt_conn_with_carrier TYPE lcl_connection_reader=>tt_connection_with_carrier.
    DATA ls_conn_with_carrier TYPE lcl_connection_reader=>ty_connection_with_carrier.
    
    lt_conn_with_carrier = lo_reader->get_connections_with_carrier_name(
      iv_carrier_id = 'LH'
    ).
    
    lv_connection_count = lines( lt_conn_with_carrier ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( | | ).
      
      " Mostrar con nombre de aerolínea
      LOOP AT lt_conn_with_carrier INTO ls_conn_with_carrier.
        out->write( |  { ls_conn_with_carrier-connection_id }: |
                 && |{ ls_conn_with_carrier-carrier_name } ({ ls_conn_with_carrier-carrier_id }) - |
                 && |{ ls_conn_with_carrier-airport_from_id } → |
                 && |{ ls_conn_with_carrier-airport_to_id } |
                 && |({ ls_conn_with_carrier-distance } { ls_conn_with_carrier-distance_unit })| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones' ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### INNER JOIN
```abap
FROM /dmo/connection AS conn
INNER JOIN /dmo/carrier AS car
  ON conn~carrier_id = car~carrier_id
```

**Características**:
- Combina datos de **DOS o más tablas**
- Solo retorna registros que tienen **coincidencia en ambas tablas**
- Usa cláusula `ON` para definir la relación
- Cada tabla tiene un **alias** (conn, car) para referenciar campos

**¿Qué hace INNER JOIN?**
- Busca registros en tabla A
- Para cada registro, busca coincidencias en tabla B
- Solo retorna si hay coincidencia en AMBAS

**Analogía**:
- Como cruzar dos listas de Excel por una columna común
- Solo se muestran filas que existen en ambas listas

#### Alias de Tablas
```abap
FROM /dmo/connection AS conn
INNER JOIN /dmo/carrier AS car
```

**Propósito**:
- Nombres cortos para tablas
- Obligatorio cuando hay campos con mismo nombre en ambas tablas
- Mejora legibilidad del código

**Uso del alias**:
```abap
conn~carrier_id      " Campo de tabla connection
car~name             " Campo de tabla carrier
```

**Sin alias (ERROR)**:
```abap
carrier_id           " ¿De qué tabla?
```

#### Cláusula ON
```abap
ON conn~carrier_id = car~carrier_id
```

**Propósito**:
- Define el **campo de unión** entre tablas
- Especifica cómo relacionar los registros
- Similar al WHERE pero para JOIN

**Equivalente conceptual**:
```sql
WHERE connection.carrier_id = carrier.carrier_id
```

#### FIELDS con JOIN
```abap
FIELDS conn~carrier_id,
       car~name AS carrier_name,
       conn~connection_id,
       conn~airport_from_id
```

**Características**:
- Debe especificarse tabla de origen: `conn~campo`
- Puede usar alias con `AS`: `car~name AS carrier_name`
- Combina campos de ambas tablas en el resultado

#### Tipo Personalizado para Resultado
```abap
TYPES: BEGIN OF ty_connection_with_carrier,
         carrier_id      TYPE /dmo/carrier_id,
         carrier_name    TYPE /dmo/carrier_name,
         connection_id   TYPE /dmo/connection_id,
         ...
       END OF ty_connection_with_carrier.
```

**¿Por qué necesario?**:
- El resultado combina campos de DOS tablas
- No existe un tipo estándar que los contenga
- Debemos definir estructura personalizada

**Declaración de tabla de este tipo**:
```abap
TYPES tt_connection_with_carrier TYPE STANDARD TABLE OF ty_connection_with_carrier.
```

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_conn_details TYPE lcl_connection_reader=>tt_connection_with_carrier.
DATA ls_conn_detail  TYPE lcl_connection_reader=>ty_connection_with_carrier.
DATA lo_reader       TYPE REF TO lcl_connection_reader.
DATA lv_count        TYPE i.

" Crear lector
lo_reader = NEW #( ).

" Obtener conexiones con nombre de aerolínea
lt_conn_details = lo_reader->get_connections_with_carrier_name(
  iv_carrier_id = 'LH'
).

lv_count = lines( lt_conn_details ).

IF lv_count > 0.
  
  WRITE: / |=== CONEXIONES DE LUFTHANSA ===|.
  WRITE: / | |.
  
  LOOP AT lt_conn_details INTO ls_conn_detail.
    
    WRITE: / |Vuelo: { ls_conn_detail-connection_id }|.
    WRITE: / |  Aerolínea: { ls_conn_detail-carrier_name } ({ ls_conn_detail-carrier_id })|.
    WRITE: / |  Ruta: { ls_conn_detail-airport_from_id } → { ls_conn_detail-airport_to_id }|.
    WRITE: / |  Distancia: { ls_conn_detail-distance } { ls_conn_detail-distance_unit }|.
    WRITE: / |----------------------------------------|.
    
  ENDLOOP.
  
  WRITE: / |Total: { lv_count } conexiones|.
  
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `iv_carrier_id = 'LH'`

**Output en Consola**:
```
--- MÉTODO 6: SELECT con INNER JOIN ---
Buscar: Conexiones de 'LH' con nombre de aerolínea
 
✓ Conexiones encontradas: 5
 
  0400: Lufthansa (LH) - FRA → JFK (6162 KM)
  0401: Lufthansa (LH) - FRA → SFO (9090 KM)
  0402: Lufthansa (LH) - FRA → LAX (9481 KM)
  2402: Lufthansa (LH) - FRA → GRU (9883 KM)
  2403: Lufthansa (LH) - FRA → BUE (11845 KM)
```

---

### 🔍 Comparación: Sin JOIN vs Con JOIN

**SIN JOIN (Método 2)**:
```abap
SELECT FROM /dmo/connection
  FIELDS carrier_id, connection_id, airport_from_id
  WHERE carrier_id = 'LH'
  INTO TABLE @lt_connections.
```
**Resultado**:
- Solo datos de `/dmo/connection`
- No tiene nombre de aerolínea
- Una sola consulta

**CON JOIN (Método 6)**:
```abap
SELECT FROM /dmo/connection AS conn
  INNER JOIN /dmo/carrier AS car
    ON conn~carrier_id = car~carrier_id
  FIELDS conn~carrier_id, car~name, conn~connection_id
  WHERE conn~carrier_id = 'LH'
  INTO TABLE @lt_result.
```
**Resultado**:
- Datos de ambas tablas combinados
- Incluye nombre de aerolínea
- Una sola consulta (más eficiente que dos separadas)

---

### 🎯 Caso de Uso Real

**Escenario**: Sistema de reservas - Mostrar información completa de vuelos

**Sin JOIN (Ineficiente)**:
```abap
" 1. Obtener conexiones
SELECT * FROM /dmo/connection WHERE carrier_id = 'LH' INTO TABLE @lt_conn.

" 2. Para cada conexión, obtener nombre de carrier
LOOP AT lt_conn INTO ls_conn.
  SELECT SINGLE name FROM /dmo/carrier 
    WHERE carrier_id = @ls_conn-carrier_id
    INTO @lv_carrier_name.
  " Mostrar ls_conn + lv_carrier_name
ENDLOOP.
" Problema: N+1 queries (1 inicial + 1 por cada conexión)
```

**Con JOIN (Eficiente)**:
```abap
" Una sola query obtiene todo
lt_details = lo_reader->get_connections_with_carrier_name(
  iv_carrier_id = 'LH'
).

" Datos completos en una sola consulta
LOOP AT lt_details INTO ls_detail.
  " Ya tiene carrier_name sin consulta adicional
  WRITE: / ls_detail-carrier_name, ls_detail-connection_id.
ENDLOOP.
" Ventaja: Solo 1 query a la base de datos
```

---

### ⚠️ Notas Importantes

#### INNER JOIN vs LEFT JOIN

**INNER JOIN**:
- Solo retorna registros con coincidencia en **AMBAS** tablas
- Si no hay carrier para una connection, esa connection NO aparece

**LEFT JOIN** (no usado aquí):
- Retorna TODOS los registros de la tabla izquierda
- Aunque no tengan coincidencia en la derecha
- Campos de tabla derecha quedan en blanco si no hay match

**Ejemplo**:
```abap
" Si hay una connection con carrier_id = 'XX' que no existe en /dmo/carrier:

" INNER JOIN: Esa connection NO aparece en resultado
" LEFT JOIN: Esa connection SÍ aparece, pero carrier_name está vacío
```

#### Rendimiento

**Ventajas del JOIN**:
- Una sola consulta a BD (vs múltiples)
- Menos tráfico de red
- BD optimiza el JOIN automáticamente

**Cuándo evitar JOIN**:
- Tablas muy grandes (millones de registros)
- Si solo necesitas datos de una tabla
- Si el JOIN produce demasiados resultados

---

## Método 7: get_connections_with_airport_names

### 🎯 Objetivo
Leer conexiones combinando datos de **TRES TABLAS** usando **DOBLE INNER JOIN** para obtener nombres de aeropuertos de origen y destino.

---

### 📝 Código Completo - Versión 7 (FINAL)

En esta séptima y última versión, agregamos el método `get_connections_with_airport_names` que utiliza doble INNER JOIN para combinar conexiones con información de aeropuertos.

#### Clase Local: `lcl_connection_reader` (Tab: Local Types)

```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection_reader DEFINITION.

  PUBLIC SECTION.
    
    " Tipo para resultado con nombre de carrier
    TYPES: BEGIN OF ty_connection_with_carrier,
             carrier_id      TYPE /dmo/carrier_id,
             carrier_name    TYPE /dmo/carrier_name,
             connection_id   TYPE /dmo/connection_id,
             airport_from_id TYPE /dmo/airport_from_id,
             airport_to_id   TYPE /dmo/airport_to_id,
             distance        TYPE /dmo/flight_distance,
             distance_unit   TYPE /dmo/distance_unit,
           END OF ty_connection_with_carrier.
    
    TYPES tt_connection_with_carrier TYPE STANDARD TABLE OF ty_connection_with_carrier.
    
    " Tipo para resultado con nombres de aeropuertos
    TYPES: BEGIN OF ty_connection_full_details,
             carrier_id        TYPE /dmo/carrier_id,
             connection_id     TYPE /dmo/connection_id,
             airport_from_id   TYPE /dmo/airport_from_id,
             airport_from_name TYPE /dmo/airport_name,
             airport_from_city TYPE /dmo/city,
             airport_to_id     TYPE /dmo/airport_to_id,
             airport_to_name   TYPE /dmo/airport_name,
             airport_to_city   TYPE /dmo/city,
             distance          TYPE /dmo/flight_distance,
             distance_unit     TYPE /dmo/distance_unit,
           END OF ty_connection_full_details.
    
    TYPES tt_connection_full_details TYPE STANDARD TABLE OF ty_connection_full_details.
    
    " Método 1: Leer UNA conexión específica
    METHODS get_single_connection
      IMPORTING
        iv_carrier_id       TYPE /dmo/carrier_id
        iv_connection_id    TYPE /dmo/connection_id
      RETURNING
        VALUE(rs_connection) TYPE /dmo/connection.
    
    " Método 2: Leer MÚLTIPLES conexiones por aerolínea
    METHODS get_connections_by_carrier
      IMPORTING
        iv_carrier_id        TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 3: Leer con MÚLTIPLES filtros
    METHODS get_connections_with_multiple_filters
      IMPORTING
        iv_airport_from_id TYPE /dmo/airport_from_id
        iv_distance_min    TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 4: Leer con OPERADORES avanzados
    METHODS get_connections_with_operators
      IMPORTING
        it_carrier_ids TYPE STANDARD TABLE OF /dmo/carrier_id
        iv_distance_max TYPE /dmo/flight_distance
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 5: Leer TODOS los registros
    METHODS get_all_connections
      RETURNING
        VALUE(rt_connections) TYPE STANDARD TABLE OF /dmo/connection.
    
    " Método 6: Leer con INNER JOIN (nombre de carrier)
    METHODS get_connections_with_carrier_name
      IMPORTING
        iv_carrier_id TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_result) TYPE tt_connection_with_carrier.
    
    " Método 7: Leer con DOBLE INNER JOIN (nombres de aeropuertos)
    METHODS get_connections_with_airport_names
      IMPORTING
        iv_carrier_id TYPE /dmo/carrier_id
      RETURNING
        VALUE(rt_result) TYPE tt_connection_full_details.
    
ENDCLASS.



CLASS lcl_connection_reader IMPLEMENTATION.

  METHOD get_single_connection.
    
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    = @iv_carrier_id
        AND connection_id = @iv_connection_id
      INTO @rs_connection.
    
  ENDMETHOD.

  METHOD get_connections_by_carrier.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id = @iv_carrier_id
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_multiple_filters.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE airport_from_id = @iv_airport_from_id
        AND distance        >= @iv_distance_min
      ORDER BY distance DESCENDING
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_operators.
    
    SELECT
      FROM /dmo/connection
      FIELDS *
      WHERE carrier_id    IN @it_carrier_ids
        AND distance      <  @iv_distance_max
        AND distance_unit <> 'MI'
      ORDER BY carrier_id, distance
      INTO TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_all_connections.
    
    SELECT
      FROM /dmo/connection
      FIELDS carrier_id, connection_id, airport_from_id, airport_to_id, distance
      ORDER BY carrier_id, connection_id
      INTO CORRESPONDING FIELDS OF TABLE @rt_connections.
    
  ENDMETHOD.

  METHOD get_connections_with_carrier_name.
    
    SELECT
      FROM /dmo/connection AS conn
      INNER JOIN /dmo/carrier AS car
        ON conn~carrier_id = car~carrier_id
      FIELDS conn~carrier_id,
             car~name AS carrier_name,
             conn~connection_id,
             conn~airport_from_id,
             conn~airport_to_id,
             conn~distance,
             conn~distance_unit
      WHERE conn~carrier_id = @iv_carrier_id
      ORDER BY conn~connection_id
      INTO TABLE @rt_result.
    
  ENDMETHOD.

  METHOD get_connections_with_airport_names.
    
    " DOBLE INNER JOIN con tabla de aeropuertos
    SELECT
      FROM /dmo/connection AS conn
      INNER JOIN /dmo/airport AS apt_from
        ON conn~airport_from_id = apt_from~airport_id
      INNER JOIN /dmo/airport AS apt_to
        ON conn~airport_to_id = apt_to~airport_id
      FIELDS conn~carrier_id,
             conn~connection_id,
             conn~airport_from_id,
             apt_from~name AS airport_from_name,
             apt_from~city AS airport_from_city,
             conn~airport_to_id,
             apt_to~name AS airport_to_name,
             apt_to~city AS airport_to_city,
             conn~distance,
             conn~distance_unit
      WHERE conn~carrier_id = @iv_carrier_id
      ORDER BY conn~connection_id
      INTO TABLE @rt_result.
    
  ENDMETHOD.
  
ENDCLASS.
```

---

#### Clase Global: `ZCL_##_DB_PRACTICE` (COMPLETO)

```abap
CLASS zcl_##_db_practice DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_db_practice IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA lo_reader               TYPE REF TO lcl_connection_reader.
    DATA ls_single_connection    TYPE /dmo/connection.
    DATA lt_carrier_connections  TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_filtered_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_operator_connections TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_all_connections      TYPE STANDARD TABLE OF /dmo/connection.
    DATA lt_carrier_ids          TYPE STANDARD TABLE OF /dmo/carrier_id.
    DATA lt_conn_with_carrier    TYPE lcl_connection_reader=>tt_connection_with_carrier.
    DATA lt_conn_full_details    TYPE lcl_connection_reader=>tt_connection_full_details.
    DATA lv_connection_count     TYPE i.
    DATA ls_connection           TYPE /dmo/connection.
    DATA lv_carrier_id           TYPE /dmo/carrier_id.
    DATA ls_conn_with_carrier    TYPE lcl_connection_reader=>ty_connection_with_carrier.
    DATA ls_conn_full_detail     TYPE lcl_connection_reader=>ty_connection_full_details.
    DATA lv_total_distance       TYPE /dmo/flight_distance.
    
    " Instanciar clase local
    "**************************
    lo_reader = NEW #( ).
    
    " ... (código de métodos 1-6 aquí - omitido por brevedad)
    
    " Método 7: Leer con DOBLE INNER JOIN - Nombres de aeropuertos
    "**************************
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    out->write( |--- MÉTODO 7: SELECT con DOBLE INNER JOIN ---| ).
    out->write( |Buscar: Conexiones de 'LH' con nombres completos de aeropuertos| ).
    out->write( | | ).
    
    lt_conn_full_details = lo_reader->get_connections_with_airport_names(
      iv_carrier_id = 'LH'
    ).
    
    lv_connection_count = lines( lt_conn_full_details ).
    
    IF lv_connection_count > 0.
      out->write( |✓ Conexiones encontradas: { lv_connection_count }| ).
      out->write( |  (Con información completa de aeropuertos)| ).
      out->write( | | ).
      
      " Mostrar información detallada
      LOOP AT lt_conn_full_details INTO ls_conn_full_detail.
        out->write( |  { sy-tabix }. Vuelo { ls_conn_full_detail-carrier_id }-{ ls_conn_full_detail-connection_id }| ).
        out->write( |     Origen: { ls_conn_full_detail-airport_from_id } - |
                 && |{ ls_conn_full_detail-airport_from_name } ({ ls_conn_full_detail-airport_from_city })| ).
        out->write( |     Destino: { ls_conn_full_detail-airport_to_id } - |
                 && |{ ls_conn_full_detail-airport_to_name } ({ ls_conn_full_detail-airport_to_city })| ).
        out->write( |     Distancia: { ls_conn_full_detail-distance } { ls_conn_full_detail-distance_unit }| ).
        out->write( |  -------------------------------------------------| ).
      ENDLOOP.
    ELSE.
      out->write( '✗ No se encontraron conexiones' ).
    ENDIF.
    
    " Resumen final
    "**************************
    out->write( | | ).
    out->write( |{ cl_abap_char_utilities=>newline }| ).
    out->write( |=== FIN DE EJERCICIOS ===| ).
    out->write( |Total de métodos demostrados: 7| ).
    out->write( |  - 5 métodos SIN JOIN| ).
    out->write( |  - 2 métodos CON JOIN| ).
    
  ENDMETHOD.
  
ENDCLASS.
```

---

### 💡 Conceptos Clave

#### Doble INNER JOIN
```abap
FROM /dmo/connection AS conn
INNER JOIN /dmo/airport AS apt_from
  ON conn~airport_from_id = apt_from~airport_id
INNER JOIN /dmo/airport AS apt_to
  ON conn~airport_to_id = apt_to~airport_id
```

**Características**:
- Combina datos de **TRES tablas**
- Dos JOIN consecutivos, cada uno con su propia condición ON
- Permite acceder a la misma tabla (airport) **DOS VECES** con diferentes alias
- Solo retorna registros con coincidencias en LAS TRES tablas

**Flujo de ejecución**:
1. Toma registros de `/dmo/connection`
2. Para cada connection, busca aeropuerto origen en `/dmo/airport`
3. Para el mismo connection, busca aeropuerto destino en `/dmo/airport`
4. Solo retorna si encuentra AMBOS aeropuertos

#### Alias Múltiples de la Misma Tabla
```abap
INNER JOIN /dmo/airport AS apt_from
  ON conn~airport_from_id = apt_from~airport_id
INNER JOIN /dmo/airport AS apt_to
  ON conn~airport_to_id = apt_to~airport_id
```

**¿Por qué dos alias para /dmo/airport?**
- Necesitamos información de DOS aeropuertos diferentes
- Uno es origen (apt_from)
- Otro es destino (apt_to)
- Sin alias diferentes, no podríamos distinguirlos

**Analogía**:
- Como tener dos instancias de la misma persona: "Juan como remitente" y "Juan como destinatario"

#### FIELDS con Múltiples Tablas
```abap
FIELDS conn~carrier_id,
       conn~connection_id,
       apt_from~name AS airport_from_name,
       apt_from~city AS airport_from_city,
       apt_to~name AS airport_to_name,
       apt_to~city AS airport_to_city
```

**Organización**:
- Campos de connection: `conn~*`
- Campos de aeropuerto origen: `apt_from~*`
- Campos de aeropuerto destino: `apt_to~*`
- Alias obligatorios para evitar ambigüedad

#### Tipo Personalizado Extendido
```abap
TYPES: BEGIN OF ty_connection_full_details,
         carrier_id        TYPE /dmo/carrier_id,
         connection_id     TYPE /dmo/connection_id,
         airport_from_id   TYPE /dmo/airport_from_id,
         airport_from_name TYPE /dmo/airport_name,
         airport_from_city TYPE /dmo/city,
         airport_to_id     TYPE /dmo/airport_to_id,
         airport_to_name   TYPE /dmo/airport_name,
         airport_to_city   TYPE /dmo/city,
         distance          TYPE /dmo/flight_distance,
       END OF ty_connection_full_details.
```

**Estructura**:
- Combina campos de 3 tablas diferentes
- Información completa para mostrar al usuario
- Ideal para reportes y UIs

---

### 📋 Ejemplo de Uso Extendido

```abap
DATA lt_full_details TYPE lcl_connection_reader=>tt_connection_full_details.
DATA ls_detail       TYPE lcl_connection_reader=>ty_connection_full_details.
DATA lo_reader       TYPE REF TO lcl_connection_reader.
DATA lv_count        TYPE i.

" Crear lector
lo_reader = NEW #( ).

" Obtener conexiones con información completa
lt_full_details = lo_reader->get_connections_with_airport_names(
  iv_carrier_id = 'LH'
).

lv_count = lines( lt_full_details ).

IF lv_count > 0.
  
  WRITE: / |=== CONEXIONES LUFTHANSA - DETALLE COMPLETO ===|.
  WRITE: / | |.
  
  LOOP AT lt_full_details INTO ls_detail.
    
    WRITE: / |Vuelo: { ls_detail-carrier_id }-{ ls_detail-connection_id }|.
    WRITE: / | |.
    WRITE: / |  ORIGEN:|.
    WRITE: / |    Aeropuerto: { ls_detail-airport_from_name }|.
    WRITE: / |    Ciudad: { ls_detail-airport_from_city }|.
    WRITE: / |    Código: { ls_detail-airport_from_id }|.
    WRITE: / | |.
    WRITE: / |  DESTINO:|.
    WRITE: / |    Aeropuerto: { ls_detail-airport_to_name }|.
    WRITE: / |    Ciudad: { ls_detail-airport_to_city }|.
    WRITE: / |    Código: { ls_detail-airport_to_id }|.
    WRITE: / | |.
    WRITE: / |  Distancia: { ls_detail-distance } { ls_detail-distance_unit }|.
    WRITE: / |============================================|.
    WRITE: / | |.
    
  ENDLOOP.
  
ENDIF.
```

---

### ✅ Resultado de Ejecución

**Input**:
- `iv_carrier_id = 'LH'`

**Output en Consola**:
```
--- MÉTODO 7: SELECT con DOBLE INNER JOIN ---
Buscar: Conexiones de 'LH' con nombres completos de aeropuertos
 
✓ Conexiones encontradas: 5
  (Con información completa de aeropuertos)
 
  1. Vuelo LH-0400
     Origen: FRA - Frankfurt Airport (Frankfurt)
     Destino: JFK - John F. Kennedy International Airport (New York)
     Distancia: 6162 KM
  -------------------------------------------------
  2. Vuelo LH-0401
     Origen: FRA - Frankfurt Airport (Frankfurt)
     Destino: SFO - San Francisco International Airport (San Francisco)
     Distancia: 9090 KM
  -------------------------------------------------
  3. Vuelo LH-0402
     Origen: FRA - Frankfurt Airport (Frankfurt)
     Destino: LAX - Los Angeles International Airport (Los Angeles)
     Distancia: 9481 KM
  -------------------------------------------------
  4. Vuelo LH-2402
     Origen: FRA - Frankfurt Airport (Frankfurt)
     Destino: GRU - São Paulo-Guarulhos International Airport (São Paulo)
     Distancia: 9883 KM
  -------------------------------------------------
  5. Vuelo LH-2403
     Origen: FRA - Frankfurt Airport (Frankfurt)
     Destino: EZE - Ministro Pistarini International Airport (Buenos Aires)
     Distancia: 11845 KM
  -------------------------------------------------
```

---

### 🔍 Evolución de Complejidad

| Método | Tablas | JOIN | Información Obtenida |
|--------|--------|------|----------------------|
| **Método 1-5** | 1 | No | Solo datos de /dmo/connection |
| **Método 6** | 2 | INNER JOIN | Connection + nombre carrier |
| **Método 7** | 3 | Doble INNER JOIN | Connection + nombres aeropuertos origen/destino |

---

### 🎯 Caso de Uso Real

**Escenario**: Sistema de búsqueda de vuelos para clientes

**Requerimiento**: 
"Mostrar todas las rutas de Lufthansa con nombres legibles de aeropuertos para que los clientes entiendan dónde van"

**Sin JOIN (Muy ineficiente)**:
```abap
" 1. Obtener conexiones
SELECT * FROM /dmo/connection WHERE carrier_id = 'LH' INTO TABLE @lt_conn.

" 2. Para cada conexión, obtener aeropuerto origen
LOOP AT lt_conn INTO ls_conn.
  SELECT SINGLE name, city FROM /dmo/airport 
    WHERE airport_id = @ls_conn-airport_from_id
    INTO (@lv_from_name, @lv_from_city).
    
  " 3. Obtener aeropuerto destino
  SELECT SINGLE name, city FROM /dmo/airport 
    WHERE airport_id = @ls_conn-airport_to_id
    INTO (@lv_to_name, @lv_to_city).
    
  " Mostrar información
ENDLOOP.
" Problema: 1 + (N * 2) queries = 1 + 10 conexiones * 2 = 21 queries!
```

**Con Doble JOIN (Eficiente)**:
```abap
" Una sola query obtiene TODO
lt_details = lo_reader->get_connections_with_airport_names(
  iv_carrier_id = 'LH'
).

" Mostrar información completa
LOOP AT lt_details INTO ls_detail.
  WRITE: / |De { ls_detail-airport_from_name } ({ ls_detail-airport_from_city })|.
  WRITE: / |A { ls_detail-airport_to_name } ({ ls_detail-airport_to_city })|.
ENDLOOP.
" Ventaja: Solo 1 query, información completa
```

---

### 📊 Comparación Final: Todos los Métodos

| # | Método | Tablas | JOIN | WHERE | Orden | Complejidad |
|---|--------|--------|------|-------|-------|-------------|
| 1 | get_single_connection | 1 | No | Clave completa | No | ⭐ Básico |
| 2 | get_connections_by_carrier | 1 | No | 1 condición | No | ⭐ Básico |
| 3 | get_connections_with_multiple_filters | 1 | No | Múltiple AND | Sí | ⭐⭐ Intermedio |
| 4 | get_connections_with_operators | 1 | No | IN, <>, < | Sí | ⭐⭐ Intermedio |
| 5 | get_all_connections | 1 | No | Sin WHERE | Sí | ⭐⭐ Intermedio |
| 6 | get_connections_with_carrier_name | 2 | INNER | 1 condición | Sí | ⭐⭐⭐ Avanzado |
| 7 | get_connections_with_airport_names | 3 | Doble INNER | 1 condición | Sí | ⭐⭐⭐⭐ Experto |

---

### ⚠️ Consideraciones de Rendimiento

#### JOIN vs Múltiples SELECT

**Ventajas del JOIN**:
- ✅ Una sola consulta a BD
- ✅ Menos tráfico de red
- ✅ BD optimiza el JOIN internamente
- ✅ Código más limpio

**Desventajas del JOIN**:
- ❌ Más complejo de escribir
- ❌ Puede ser lento en tablas muy grandes
- ❌ Resultado puede ser muy grande (producto cartesiano si mal usado)

#### Buenas Prácticas con JOIN

1. **Siempre especificar campos**:
```abap
" ❌ MAL
FIELDS *

" ✅ BIEN
FIELDS conn~carrier_id, apt_from~name, apt_to~name
```

2. **Usar WHERE para limitar resultados**:
```abap
" ✅ Filtrar para reducir datos
WHERE conn~carrier_id = @iv_carrier_id
```

3. **Verificar condiciones ON correctas**:
```abap
" ✅ BIEN - une por campos relacionados
ON conn~airport_from_id = apt_from~airport_id

" ❌ MAL - puede generar producto cartesiano
ON 1 = 1  " NUNCA hacer esto
```

---

## 🎓 Resumen del Documento Completo

### Métodos Sin JOIN (1-5)

| Método | Propósito Principal |
|--------|---------------------|
| **1** | Buscar UN registro específico por clave |
| **2** | Filtrar por un campo |
| **3** | Combinar múltiples filtros |
| **4** | Usar operadores avanzados (IN, <>, <) |
| **5** | Leer tabla completa sin filtros |

### Métodos Con JOIN (6-7)

| Método | Propósito Principal |
|--------|---------------------|
| **6** | Enriquecer datos con información de otra tabla (carrier) |
| **7** | Combinar información de tres tablas (connection + 2 aeropuertos) |

### Conceptos Aprendidos

✅ SELECT SINGLE vs SELECT múltiple  
✅ WHERE con diferentes operadores  
✅ ORDER BY para ordenamiento  
✅ INTO vs INTO TABLE  
✅ FIELDS * vs campos específicos  
✅ INNER JOIN simple  
✅ INNER JOIN múltiple (mismo tabla con diferentes alias)  
✅ Tipos personalizados para resultados complejos  
✅ Optimización de consultas  
✅ Buenas prácticas de rendimiento  

---

## 📚 Ejercicios Sugeridos para Estudiantes

1. **Modificar Método 3**: Agregar un filtro adicional por `distance_unit`
2. **Extender Método 6**: Incluir también la moneda del carrier (`currency_code`)
3. **Crear Método 8**: Triple JOIN incluyendo carrier, aeropuerto origen y destino
4. **Optimizar Método 5**: Agregar un parámetro para limitar registros (UP TO n ROWS)
5. **Nuevo Método**: Buscar conexiones entre dos ciudades específicas (requiere doble JOIN con aeropuertos)

---

## ✅ Checklist de Aprendizaje

- [ ] Entiendo la diferencia entre SELECT SINGLE y SELECT
- [ ] Sé cuándo usar INTO vs INTO TABLE
- [ ] Puedo escribir WHERE con múltiples condiciones (AND)
- [ ] Conozco operadores: =, <>, <, >, <=, >=, IN
- [ ] Entiendo cómo funciona ORDER BY
- [ ] Sé qué es un INNER JOIN
- [ ] Puedo escribir un JOIN simple
- [ ] Puedo escribir un JOIN múltiple
- [ ] Entiendo el concepto de alias de tablas
- [ ] Sé crear tipos personalizados para resultados
- [ ] Conozco buenas prácticas de rendimiento

---

**🎉 FIN DEL DOCUMENTO - Unit 4: Database Reading - Práctica Avanzada**

---

**Información del Documento**:
- **Total de Métodos**: 7 (5 sin JOIN + 2 con JOIN)
- **Líneas de Código**: ~2500
- **Nivel**: Principiante → Intermedio → Avanzado
- **Última actualización**: Diciembre 2024
