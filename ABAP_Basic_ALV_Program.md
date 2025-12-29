# 📚 Programa ABAP Básico: Introducción a Reports con ALV

![SAP](https://img.shields.io/badge/SAP-0FAAFF?style=for-the-badge&logo=sap&logoColor=white)
![ABAP](https://img.shields.io/badge/ABAP-0FAAFF?style=for-the-badge&logo=sap&logoColor=white)
![NetWeaver](https://img.shields.io/badge/NetWeaver-7.40-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-Educational-blue?style=for-the-badge)

> 🎓 **Material educativo para estudiantes que están aprendiendo ABAP desde cero**
> 
> Este documento te guiará paso a paso para crear tu primer programa ABAP ejecutable con parámetros de entrada, consultas a base de datos y visualización en formato ALV.

---

## 📑 Tabla de Contenidos

- [¿Qué es un Programa ABAP?](#-qué-es-un-programa-abap)
- [¿Para qué se usa un Programa ABAP?](#-para-qué-se-usa-un-programa-abap)
- [Tipos de Programas ABAP](#-tipos-de-programas-abap)
- [Estructura de un Programa ABAP](#%EF%B8%8F-estructura-de-un-programa-abap)
- [Eventos del Programa](#-eventos-del-programa)
- [Código Completo](#-código-completo)
- [Cómo Ejecutarlo](#%EF%B8%8F-cómo-ejecutarlo)
- [Resultado Esperado](#-resultado-esperado)
- [Conceptos Clave](#-conceptos-clave)
- [Ejercicios Adicionales](#-ejercicios-adicionales)

---

## 🤔 ¿Qué es un Programa ABAP?

Un **Programa ABAP** (también llamado **Report**) es una unidad de código ejecutable que se crea en el sistema SAP para realizar tareas específicas como:

- 📊 Generar reportes y listados
- 🔍 Consultar datos de la base de datos
- ✏️ Procesar y modificar información
- 📤 Exportar datos a archivos externos
- 🎨 Presentar información en diferentes formatos (listas, ALV, formularios)

### 🍕 Analogía del Mundo Real

Piensa en un programa ABAP como una **receta de cocina digital**:

| Componente | Analogía | En ABAP |
|------------|----------|---------|
| 🧾 **Receta** | Instrucciones paso a paso | El código del programa |
| 🥘 **Ingredientes** | Datos necesarios | Parámetros de entrada |
| 👨‍🍳 **Cocinero** | Quien ejecuta | El usuario que corre el programa |
| 🍽️ **Plato final** | Resultado | El reporte o salida ALV |

---

## 🎯 ¿Para qué se usa un Programa ABAP?

Los programas ABAP tienen múltiples usos en el día a día de SAP:

<details>
<summary>📊 <b>Generación de Reportes</b> (Click para expandir)</summary>

<br>

Crear listados de información para análisis:
- 💰 Reportes financieros (ventas, costos, ingresos)
- 📦 Inventarios de materiales
- 👥 Listas de empleados
- 📈 Análisis de datos operacionales

**Ejemplo:** Un reporte de ventas mensuales por región que los gerentes pueden consultar cada fin de mes.

</details>

<details>
<summary>🔧 <b>Procesamiento de Datos</b> (Click para expandir)</summary>

<br>

Manipular grandes volúmenes de información:
- 🔄 Actualización masiva de registros
- 🧹 Limpieza de datos duplicados
- 📊 Cálculos complejos y agregaciones
- 🔀 Migración de datos entre sistemas

**Ejemplo:** Un programa que actualiza los precios de 10,000 productos aplicando un descuento del 15%.

</details>

<details>
<summary>🎨 <b>Interfaces de Usuario</b> (Click para expandir)</summary>

<br>

Crear pantallas para que los usuarios interactúen:
- 📝 Pantallas de selección con filtros
- ✅ Validaciones de datos
- 🎛️ Parámetros configurables
- 📋 Visualización en formato ALV (tabla Excel-like)

**Ejemplo:** Una pantalla donde el usuario selecciona fecha inicial, fecha final y centro de trabajo, y el programa muestra las órdenes de ese período.

</details>

<details>
<summary>🔗 <b>Integración de Sistemas</b> (Click para expandir)</summary>

<br>

Conectar SAP con otros sistemas:
- 📤 Exportar datos a archivos CSV/Excel
- 📥 Importar datos desde archivos externos
- 🌐 Consumir/exponer servicios web
- 🔌 Interfaces con aplicaciones legadas

**Ejemplo:** Un programa que genera un archivo Excel con datos de facturación para enviarlo al sistema contable externo.

</details>

---

## 📂 Tipos de Programas ABAP

SAP maneja diferentes tipos de programas según su propósito:

| Tipo | Código | Descripción | Ejemplo de Uso |
|------|--------|-------------|----------------|
| 🟢 **Ejecutable** | `1` | Report que se ejecuta directamente (F8) | Reportes, listados, procesos batch |
| 🔵 **Module Pool** | `M` | Programa con pantallas (Dynpro) | Transacciones personalizadas con UI |
| 🟡 **Include** | `I` | Fragmento de código reutilizable | Librerías de funciones compartidas |
| 🟣 **Subrutina** | `S` | Pool de subrutinas (FORM) | Colección de procedimientos |
| 🟠 **Function Group** | `F` | Grupo de módulos de función | APIs internas de SAP |
| 🔴 **Interface Pool** | `J` | Definición de interfaces (OO) | Interfaces de objetos |
| ⚫ **Class Pool** | `K` | Definición de clases (OO) | Clases globales ABAP OO |

> 💡 **Para este tutorial usaremos un programa tipo "Ejecutable" (tipo 1)**, el más común para crear reportes y listados.

---

## 🏗️ Estructura de un Programa ABAP

Un programa ABAP sigue una estructura lógica predefinida:

```
┌─────────────────────────────────────────┐
│  📋 REPORT [nombre_programa]            │  ← Declaración del programa
├─────────────────────────────────────────┤
│  📦 DECLARACIÓN DE DATOS                │
│     - TABLES                            │  ← Tablas de BD usadas
│     - DATA                              │  ← Variables internas
│     - TYPES                             │  ← Tipos de datos custom
├─────────────────────────────────────────┤
│  🎛️ PANTALLA DE SELECCIÓN               │
│     - PARAMETERS                        │  ← Campos simples
│     - SELECT-OPTIONS                    │  ← Rangos de valores
├─────────────────────────────────────────┤
│  ⚡ EVENTOS DEL PROGRAMA                │
│     - INITIALIZATION                    │  ← Setup inicial
│     - AT SELECTION-SCREEN               │  ← Validaciones
│     - START-OF-SELECTION                │  ← Lógica principal
│     - END-OF-SELECTION                  │  ← Presentación final
├─────────────────────────────────────────┤
│  🔧 SUBRUTINAS (FORMS)                  │
│     - FORM [nombre] USING/CHANGING      │  ← Procedimientos con parámetros
│     - ENDFORM                           │
└─────────────────────────────────────────┘
```

### 💡 Buena Práctica: Subrutinas con Parámetros

Las subrutinas deben recibir parámetros explícitos para ser más modulares:

```
┌──────────────────────────────────────────────┐
│  PROGRAMA PRINCIPAL                          │
│                                              │
│  DATA: gt_flights TYPE TABLE OF sflight,    │
│        gt_fcat    TYPE slis_t_fieldcat_alv. │
│                                              │
│  " Llamar subrutinas pasando datos          │
│  PERFORM build_catalog CHANGING gt_fcat.    │
│         │                     ▲              │
│         └─────────────────────┘              │
│         Pasa gt_fcat como parámetro          │
│                                              │
│  PERFORM display_alv USING gt_flights        │
│                            gt_fcat.          │
│         │                   ▲                │
│         └───────────────────┴────────────    │
│         Pasa ambos como parámetros           │
└──────────────────────────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────┐
│  SUBRUTINAS                                  │
│                                              │
│  FORM build_catalog CHANGING ct_fcat.        │
│    " Trabaja con ct_fcat (parámetro local)  │
│    DATA: ls_fcat TYPE ...                   │
│    ls_fcat-fieldname = 'CARRID'.            │
│    APPEND ls_fcat TO ct_fcat.               │
│  ENDFORM.                                    │
│                                              │
│  FORM display_alv USING it_flights           │
│                         it_fcat.             │
│    " Usa los parámetros recibidos           │
│    CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'   │
│      EXPORTING it_fieldcat = it_fcat        │
│      TABLES t_outtab = it_flights.          │
│  ENDFORM.                                    │
└──────────────────────────────────────────────┘
```

**Ventajas de este enfoque:**
- ✅ Código más limpio y profesional
- ✅ Subrutinas reutilizables con diferentes datos
- ✅ Fácil de testear y mantener
- ✅ Reduce dependencias de variables globales

---

## 🎭 Eventos del Programa

Los **eventos** son momentos específicos en la ejecución del programa donde puedes escribir código. Piensa en ellos como "puntos de control" en el flujo de ejecución.

### 🎬 Analogía: Eventos como una Película

Imagina que tu programa es una película con diferentes **escenas**:

```
🎬 PELÍCULA: "MI PRIMER REPORTE ABAP"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎞️ ESCENA 1: INITIALIZATION
   "El Prólogo - Preparando el escenario"
   └─ Se ejecuta UNA vez al cargar el programa
   └─ Aquí defines valores por defecto
   └─ Como poner la fecha de hoy en un campo

🎞️ ESCENA 2: AT SELECTION-SCREEN
   "El Control de Calidad - Verificando todo"
   └─ Se ejecuta al presionar F8 o botón Ejecutar
   └─ Aquí validas lo que el usuario ingresó
   └─ Como verificar que fecha final > fecha inicial

🎞️ ESCENA 3: START-OF-SELECTION
   "La Acción Principal - Donde ocurre la magia"
   └─ Aquí va la lógica central del programa
   └─ SELECT a base de datos
   └─ Procesamiento de información
   └─ Cálculos y transformaciones

🎞️ ESCENA 4: END-OF-SELECTION
   "El Gran Final - Mostrando los resultados"
   └─ Se ejecuta DESPUÉS de START-OF-SELECTION
   └─ Aquí presentas la salida final
   └─ Como mostrar un ALV Grid con los datos

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎭 FIN DE LA PELÍCULA
```

### 📊 Comparativa de Eventos

| Evento | ¿Cuándo se ejecuta? | ¿Para qué sirve? | Ejemplo de Uso |
|--------|---------------------|------------------|----------------|
| `INITIALIZATION` | Al cargar el programa | Inicializar valores por defecto | `p_date = sy-datum.` (fecha de hoy) |
| `AT SELECTION-SCREEN` | Al presionar F8/Enter | Validar entradas del usuario | Verificar que fecha_fin >= fecha_ini |
| `START-OF-SELECTION` | Después de validaciones | Lógica principal, SELECTs | Consultar tabla SFLIGHT |
| `END-OF-SELECTION` | Al finalizar la lógica | Presentar resultados | Mostrar ALV Grid |

> ⚠️ **Importante:** Estos eventos se ejecutan en el orden mostrado, no al azar.

---

## 💻 Código Completo

A continuación, el código completo de nuestro programa de ejemplo que consulta vuelos y los muestra en formato ALV:

```abap
*&---------------------------------------------------------------------*
*& Report Z_BASIC_ALV_DEMO
*&---------------------------------------------------------------------*
*& Programa educativo: Introducción a Reports ABAP con ALV
*& Objetivo: Mostrar estructura básica, eventos y display ALV
*& Tabla: SFLIGHT (Datos de vuelos - tabla estándar de demo)
*&---------------------------------------------------------------------*

REPORT z_basic_alv_demo.

*----------------------------------------------------------------------*
* DECLARACIÓN DE TABLAS
*----------------------------------------------------------------------*
TABLES: sflight.  " Tabla de base de datos: información de vuelos

*----------------------------------------------------------------------*
* DECLARACIÓN DE DATOS
*----------------------------------------------------------------------*
DATA: gt_flights TYPE TABLE OF sflight,   " Tabla interna para almacenar vuelos
      gs_flight  TYPE sflight,            " Estructura de trabajo (work area)
      gt_fcat    TYPE slis_t_fieldcat_alv," Catálogo de campos para ALV
      gv_lines   TYPE i.                  " Contador de registros

*----------------------------------------------------------------------*
* PANTALLA DE SELECCIÓN
*----------------------------------------------------------------------*
SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.

  SELECT-OPTIONS: s_carrid FOR sflight-carrid,    " Aerolínea (ej: LH, AA, UA)
                  s_connid FOR sflight-connid,    " Número de conexión
                  s_fldate FOR sflight-fldate.    " Fecha de vuelo

  PARAMETERS: p_price TYPE sflight-price DEFAULT 500.  " Precio mínimo

SELECTION-SCREEN END OF BLOCK b1.

*----------------------------------------------------------------------*
* TEXTOS PARA LA PANTALLA DE SELECCIÓN
*----------------------------------------------------------------------*
* TEXT-001: 'Parámetros de Selección'

*----------------------------------------------------------------------*
* EVENTO 1: INITIALIZATION
* Se ejecuta una sola vez al cargar el programa
*----------------------------------------------------------------------*
INITIALIZATION.
  " Establecer fecha de hoy como valor por defecto en el rango
  s_fldate-sign   = 'I'.      " I = Include (incluir)
  s_fldate-option = 'BT'.     " BT = Between (entre)
  s_fldate-low    = sy-datum. " Fecha de hoy
  s_fldate-high   = sy-datum + 30. " +30 días
  APPEND s_fldate.

  " Mensaje informativo
  WRITE: / '🎬 INITIALIZATION ejecutado: Valores por defecto establecidos'.
  SKIP 1.

*----------------------------------------------------------------------*
* EVENTO 2: AT SELECTION-SCREEN
* Se ejecuta al presionar F8 o botón Ejecutar
* Aquí validamos las entradas del usuario
*----------------------------------------------------------------------*
AT SELECTION-SCREEN.
  " Validación: El precio mínimo debe ser mayor a cero
  IF p_price <= 0.
    MESSAGE 'El precio mínimo debe ser mayor a 0' TYPE 'E'.
  ENDIF.

  " Validación: Al menos una aerolínea debe estar especificada
  IF s_carrid[] IS INITIAL.
    MESSAGE 'Debe especificar al menos una aerolínea' TYPE 'W'.
  ENDIF.

  WRITE: / '✅ AT SELECTION-SCREEN ejecutado: Validaciones OK'.
  SKIP 1.

*----------------------------------------------------------------------*
* EVENTO 3: START-OF-SELECTION
* Aquí va la lógica principal del programa
*----------------------------------------------------------------------*
START-OF-SELECTION.
  WRITE: / '⚡ START-OF-SELECTION: Consultando base de datos...'.
  SKIP 1.

  " Consultar la tabla SFLIGHT con los criterios del usuario
  SELECT *
    FROM sflight
    INTO TABLE gt_flights
    WHERE carrid IN s_carrid    " Aerolínea
      AND connid IN s_connid    " Conexión
      AND fldate IN s_fldate    " Fecha
      AND price  >= p_price.    " Precio mínimo

  " Verificar si se encontraron datos
  DESCRIBE TABLE gt_flights LINES gv_lines.

  IF gv_lines = 0.
    WRITE: / '❌ No se encontraron vuelos con los criterios especificados.'.
    SKIP 1.
    STOP.  " Detener ejecución
  ELSE.
    WRITE: / '✅ Se encontraron', gv_lines, 'vuelos.'.
    SKIP 1.
  ENDIF.

*----------------------------------------------------------------------*
* EVENTO 4: END-OF-SELECTION
* Se ejecuta después de START-OF-SELECTION
* Aquí presentamos los resultados
*----------------------------------------------------------------------*
END-OF-SELECTION.
  WRITE: / '🎨 END-OF-SELECTION: Preparando visualización ALV...'.
  SKIP 1.

  " Preparar el catálogo de campos para el ALV
  PERFORM build_field_catalog CHANGING gt_fcat.

  " Mostrar los datos en formato ALV Grid
  PERFORM display_alv USING gt_flights
                            gt_fcat.

*----------------------------------------------------------------------*
* SUBRUTINA: BUILD_FIELD_CATALOG
* Construye el catálogo de campos que define las columnas del ALV
*----------------------------------------------------------------------*
* Parámetros:
*   CHANGING ct_fcat - Catálogo de campos (tabla a llenar)
*----------------------------------------------------------------------*
FORM build_field_catalog CHANGING ct_fcat TYPE slis_t_fieldcat_alv.

  DATA: ls_fcat TYPE slis_fieldcat_alv.  " Variable local para el catálogo

  " Campo 1: CARRID (Aerolínea)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CARRID'.
  ls_fcat-seltext_l = 'Aerolínea'.
  ls_fcat-col_pos   = 1.
  APPEND ls_fcat TO ct_fcat.

  " Campo 2: CONNID (Número de Conexión)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CONNID'.
  ls_fcat-seltext_l = 'Conexión'.
  ls_fcat-col_pos   = 2.
  APPEND ls_fcat TO ct_fcat.

  " Campo 3: FLDATE (Fecha de Vuelo)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'FLDATE'.
  ls_fcat-seltext_l = 'Fecha Vuelo'.
  ls_fcat-col_pos   = 3.
  APPEND ls_fcat TO ct_fcat.

  " Campo 4: PRICE (Precio)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'PRICE'.
  ls_fcat-seltext_l = 'Precio'.
  ls_fcat-col_pos   = 4.
  ls_fcat-do_sum    = 'X'.  " Activar suma automática
  APPEND ls_fcat TO ct_fcat.

  " Campo 5: CURRENCY (Moneda)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CURRENCY'.
  ls_fcat-seltext_l = 'Moneda'.
  ls_fcat-col_pos   = 5.
  APPEND ls_fcat TO ct_fcat.

  " Campo 6: PLANETYPE (Tipo de Avión)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'PLANETYPE'.
  ls_fcat-seltext_l = 'Tipo Avión'.
  ls_fcat-col_pos   = 6.
  APPEND ls_fcat TO ct_fcat.

  " Campo 7: SEATSMAX (Asientos Máximos)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'SEATSMAX'.
  ls_fcat-seltext_l = 'Asientos Max'.
  ls_fcat-col_pos   = 7.
  APPEND ls_fcat TO ct_fcat.

  " Campo 8: SEATSOCC (Asientos Ocupados)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'SEATSOCC'.
  ls_fcat-seltext_l = 'Asientos Ocup'.
  ls_fcat-col_pos   = 8.
  APPEND ls_fcat TO ct_fcat.

ENDFORM.

*----------------------------------------------------------------------*
* SUBRUTINA: DISPLAY_ALV
* Muestra los datos en formato ALV Grid
*----------------------------------------------------------------------*
* Parámetros:
*   USING it_flights - Tabla con los datos a mostrar
*   USING it_fcat    - Catálogo de campos del ALV
*----------------------------------------------------------------------*
FORM display_alv USING it_flights TYPE STANDARD TABLE
                       it_fcat    TYPE slis_t_fieldcat_alv.

  " Llamar a la función estándar de ALV
  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program = sy-repid           " Nombre del programa actual
      it_fieldcat        = it_fcat            " Catálogo de campos (parámetro)
      i_grid_title       = 'Listado de Vuelos (SFLIGHT)'  " Título del ALV
    TABLES
      t_outtab           = it_flights         " Tabla de datos (parámetro)
    EXCEPTIONS
      program_error      = 1
      OTHERS             = 2.

  IF sy-subrc <> 0.
    MESSAGE 'Error al mostrar ALV' TYPE 'E'.
  ENDIF.

ENDFORM.
```

---

## ▶️ Cómo Ejecutarlo

### Paso 1️⃣: Crear el Programa en SE38

1. Ejecuta la transacción **SE38** (ABAP Editor)
2. En el campo "Programa", ingresa: `Z_BASIC_ALV_DEMO`
3. Click en el botón **"Crear"** (o presiona F5)

### Paso 2️⃣: Configurar Atributos del Programa

Ingresa los siguientes datos:

| Campo | Valor |
|-------|-------|
| **Título** | `Programa Demo: ALV Básico con Vuelos` |
| **Tipo** | `Programa ejecutable` |
| **Estado** | `Programa de prueba o demo` |
| **Aplicación** | (Dejar en blanco o usar tu módulo) |

Click en **"Guardar"** (Ctrl+S)

### Paso 3️⃣: Asignar Paquete

- Selecciona **"Objeto local"** (para programas de prueba)
- O asigna un paquete de desarrollo si aplica

### Paso 4️⃣: Copiar el Código

1. Copia todo el código mostrado arriba
2. Pégalo en el editor ABAP
3. Click en **"Verificar"** (Ctrl+F2) para verificar sintaxis
4. Click en **"Activar"** (Ctrl+F3) para activar el programa

### Paso 5️⃣: Ejecutar el Programa

1. Click en **"Ejecutar"** (F8)
2. Aparecerá la **pantalla de selección** con los siguientes campos:

```
┌────────────────────────────────────────────┐
│  Parámetros de Selección                   │
├────────────────────────────────────────────┤
│                                            │
│  Aerolínea:     [AA] hasta [ZZ]           │
│  Conexión:      [____] hasta [____]       │
│  Fecha vuelo:   [29.12.2025] hasta [____] │
│  Precio mínimo: [500]                      │
│                                            │
│  [ Ejecutar (F8) ]  [ Cancelar ]          │
└────────────────────────────────────────────┘
```

3. Modifica los parámetros si deseas:
   - **Aerolínea**: Deja en blanco para ver todas, o ingresa `AA`, `LH`, `UA`, etc.
   - **Precio mínimo**: Cambia el valor si quieres filtrar vuelos más caros

4. Presiona **F8** nuevamente para ejecutar

---

## 🎨 Resultado Esperado

Al ejecutar el programa, verás una pantalla ALV Grid similar a esta:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│  Listado de Vuelos (SFLIGHT)                                                    │
├──────────┬──────────┬──────────────┬───────────┬─────────┬───────────┬──────────┤
│ Aerolínea│ Conexión │ Fecha Vuelo  │  Precio   │ Moneda  │ Tipo Avión│ Asientos │
├──────────┼──────────┼──────────────┼───────────┼─────────┼───────────┼──────────┤
│ AA       │ 0017     │ 30.12.2025   │   580.00  │ USD     │ 747-400   │ 385/400  │
│ AA       │ 0017     │ 31.12.2025   │   625.00  │ USD     │ 747-400   │ 395/400  │
│ LH       │ 0400     │ 29.12.2025   │   720.00  │ EUR     │ A340-600  │ 298/330  │
│ LH       │ 0400     │ 30.12.2025   │   750.00  │ EUR     │ A340-600  │ 315/330  │
│ UA       │ 0900     │ 29.12.2025   │   889.00  │ USD     │ 777-200   │ 262/280  │
└──────────┴──────────┴──────────────┴───────────┴─────────┴───────────┴──────────┘
                                           Σ TOTAL: 3,564.00
```

### ✨ Funcionalidades del ALV

El ALV Grid te permite:

- 🔍 **Buscar** datos (Ctrl+F)
- 📊 **Ordenar** columnas (click en encabezado)
- 🔽 **Filtrar** datos (botón de filtro)
- 📁 **Exportar** a Excel/PDF (Menú → Lista → Exportar)
- 📐 **Sumar** columnas numéricas (automático)
- 🎨 **Personalizar** layout (ancho de columnas, orden)

---

## 📚 Conceptos Clave

<details>
<summary>🎯 <b>¿Por qué usar parámetros en las subrutinas?</b></summary>

<br>

Las subrutinas (FORM) pueden acceder a variables de dos formas:
1. **Variables globales** (declaradas fuera de la subrutina)
2. **Parámetros** (pasados explícitamente)

### ❌ Forma INCORRECTA (sin parámetros):
```abap
DATA: gt_data TYPE TABLE OF sflight.

FORM procesar_datos.
  " Usa gt_data directamente (variable global)
  LOOP AT gt_data INTO DATA(ls_data).
    " Procesar...
  ENDLOOP.
ENDFORM.
```

**Problemas:**
- 🔴 Dependencia oculta de variables globales
- 🔴 Difícil de testear aisladamente
- 🔴 No se puede reutilizar con otros datos
- 🔴 Poco claro qué variables usa la subrutina

### ✅ Forma CORRECTA (con parámetros):
```abap
DATA: gt_data TYPE TABLE OF sflight.

PERFORM procesar_datos USING gt_data.

FORM procesar_datos USING it_data TYPE STANDARD TABLE.
  " Usa it_data (parámetro explícito)
  LOOP AT it_data INTO DATA(ls_data).
    " Procesar...
  ENDLOOP.
ENDFORM.
```

**Ventajas:**
- ✅ **Modularidad**: La subrutina es independiente
- ✅ **Reusabilidad**: Se puede llamar con diferentes datos
- ✅ **Claridad**: Se ve explícitamente qué necesita
- ✅ **Testeable**: Fácil de probar con datos de prueba
- ✅ **Mantenibilidad**: Cambios internos no afectan el exterior

### 📖 Tipos de parámetros:

| Tipo | Palabra Clave | Uso | Ejemplo |
|------|--------------|-----|---------|
| **Entrada** | `USING` | Solo lectura, no se modifica | Pasar datos para procesar |
| **Salida** | `CHANGING` | Se modifica y devuelve | Llenar una tabla, actualizar variable |
| **Entrada/Salida** | `CHANGING` | Se lee y modifica | Actualizar valores existentes |

**Ejemplo completo:**
```abap
" Entrada: it_vuelos (USING) - solo lectura
" Salida: et_resultados (CHANGING) - se llena en la subrutina
" Entrada/Salida: cv_contador (CHANGING) - se lee y actualiza

PERFORM calcular_totales USING    it_vuelos
                         CHANGING et_resultados
                                  cv_contador.

FORM calcular_totales USING    it_vuelos    TYPE ty_t_flights
                      CHANGING et_resultados TYPE ty_t_resultados
                               cv_contador   TYPE i.
  " Lógica aquí...
ENDFORM.
```

### 🎯 Regla de oro:
> **"Si una subrutina necesita datos, pásalos como parámetros. No uses variables globales dentro de las subrutinas."**

Esto hace tu código más profesional y mantenible. 🚀

</details>

<details>
<summary>🎯 <b>¿Qué es un SELECT?</b></summary>

<br>

El comando `SELECT` es la forma en que ABAP lee datos de la base de datos SAP.

**Sintaxis básica:**
```abap
SELECT campos
  FROM tabla
  INTO destino
  WHERE condiciones.
```

**Ejemplo:**
```abap
SELECT *
  FROM sflight
  INTO TABLE gt_flights
  WHERE carrid = 'AA'
    AND price >= 500.
```

**Traducción:** "Selecciona todos los campos (*) de la tabla SFLIGHT, guárdalos en la tabla interna gt_flights, donde la aerolínea sea 'AA' y el precio sea mayor o igual a 500."

</details>

<details>
<summary>📋 <b>¿Qué es un ALV?</b></summary>

<br>

**ALV** = **ABAP List Viewer**

Es una herramienta estándar de SAP para mostrar datos en formato tabla, similar a Excel.

**Ventajas:**
- ✅ Funcionalidades incorporadas (filtros, búsqueda, suma, exportar)
- ✅ Aspecto profesional y consistente
- ✅ Fácil de implementar
- ✅ Los usuarios ya lo conocen (usado en todo SAP)

**Tipos de ALV:**
- **ALV Grid** (el más común) - formato tabla
- **ALV List** - formato lista clásica
- **ALV Tree** - formato jerárquico

</details>

<details>
<summary>🎛️ <b>¿Qué son PARAMETERS y SELECT-OPTIONS?</b></summary>

<br>

Son los controles de entrada en la pantalla de selección:

### PARAMETERS
Campo simple con un solo valor:
```abap
PARAMETERS: p_price TYPE i.
```
**Resultado:** `[___]` (un campo de entrada)

### SELECT-OPTIONS
Rango de valores (desde-hasta):
```abap
SELECT-OPTIONS: s_carrid FOR sflight-carrid.
```
**Resultado:** `[___] hasta [___]` (dos campos)

**Analogía:**
- **PARAMETERS** = Pregunta simple: "¿Cuál es tu edad?" → `25`
- **SELECT-OPTIONS** = Pregunta de rango: "¿Entre qué edades?" → `20 hasta 30`

</details>

<details>
<summary>📦 <b>¿Qué son las Tablas Internas?</b></summary>

<br>

Una **tabla interna** es como un Array o Lista en otros lenguajes, pero específico para ABAP.

**Declaración:**
```abap
DATA: gt_flights TYPE TABLE OF sflight.
```

**Analogía:** Imagina una hoja de Excel en memoria:
- Cada fila = un registro de vuelo
- Columnas = campos (CARRID, CONNID, PRICE, etc.)
- Puedes agregar, eliminar, buscar, ordenar filas

**Operaciones comunes:**
```abap
APPEND gs_flight TO gt_flights.  " Agregar fila
DELETE gt_flights WHERE price < 100.  " Eliminar filas
SORT gt_flights BY carrid.  " Ordenar
READ TABLE gt_flights INDEX 1 INTO gs_flight.  " Leer fila
```

</details>

<details>
<summary>🏷️ <b>¿Qué es el Field Catalog?</b></summary>

<br>

El **Field Catalog** (catálogo de campos) es una tabla que define las **características de cada columna** en el ALV.

**Propósito:** Decirle al ALV:
- Qué campos mostrar
- En qué orden
- Qué título poner
- Si se puede sumar, ordenar, etc.

**Estructura básica:**
```abap
gs_fcat-fieldname = 'CARRID'.        " Nombre del campo en la tabla interna
gs_fcat-seltext_l = 'Aerolínea'.     " Título de la columna
gs_fcat-col_pos   = 1.               " Posición (orden)
gs_fcat-do_sum    = 'X'.             " Activar suma (para campos numéricos)
APPEND gs_fcat TO gt_fcat.
```

**Analogía:** Es como el "encabezado de columnas" en Excel, pero con esteroides (defines formato, comportamiento, etc.)

</details>

---

## 🚀 Ejercicios Adicionales

Una vez que domines este programa básico, intenta los siguientes desafíos:

### 🥉 Nivel Principiante

<details>
<summary>1️⃣ Agregar más filtros</summary>

<br>

Añade un nuevo parámetro para filtrar por tipo de avión:
```abap
PARAMETERS: p_plane TYPE sflight-planetype.
```

Modifica el SELECT:
```abap
SELECT *
  FROM sflight
  INTO TABLE gt_flights
  WHERE carrid    IN s_carrid
    AND connid    IN s_connid
    AND fldate    IN s_fldate
    AND price     >= p_price
    AND planetype =  p_plane.  " Nueva condición
```

</details>

<details>
<summary>2️⃣ Cambiar el título del ALV dinámicamente</summary>

<br>

Modifica la subrutina `display_alv` para que el título muestre la cantidad de registros:
```abap
DATA: lv_title TYPE lvc_title.

CONCATENATE 'Listado de Vuelos ('
            gv_lines
            'registros encontrados)'
       INTO lv_title.

CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
  EXPORTING
    i_callback_program = sy-repid
    it_fieldcat        = gt_fcat
    i_grid_title       = lv_title  " Título dinámico
  TABLES
    t_outtab           = gt_flights
  ...
```

</details>

### 🥈 Nivel Intermedio

<details>
<summary>3️⃣ Agregar columna calculada: "% Ocupación"</summary>

<br>

1. Agrega un nuevo campo a tu tabla interna:
```abap
TYPES: BEGIN OF ty_flight_ext,
         carrid     TYPE sflight-carrid,
         connid     TYPE sflight-connid,
         fldate     TYPE sflight-fldate,
         price      TYPE sflight-price,
         currency   TYPE sflight-currency,
         planetype  TYPE sflight-planetype,
         seatsmax   TYPE sflight-seatsmax,
         seatsocc   TYPE sflight-seatsocc,
         percentage TYPE p DECIMALS 2,  " Nuevo campo
       END OF ty_flight_ext.

DATA: gt_flights_ext TYPE TABLE OF ty_flight_ext.
```

2. Calcula el porcentaje:
```abap
LOOP AT gt_flights INTO gs_flight.
  gs_flight_ext-percentage = ( gs_flight-seatsocc / gs_flight-seatsmax ) * 100.
  " Copiar otros campos...
  APPEND gs_flight_ext TO gt_flights_ext.
ENDLOOP.
```

3. Agrega al Field Catalog:
```abap
gs_fcat-fieldname = 'PERCENTAGE'.
gs_fcat-seltext_l = '% Ocupación'.
gs_fcat-col_pos   = 9.
APPEND gs_fcat TO gt_fcat.
```

</details>

<details>
<summary>4️⃣ Agregar colores según condición</summary>

<br>

Colorea las filas según el porcentaje de ocupación:
- 🔴 Rojo: Más del 90% ocupado
- 🟡 Amarillo: Entre 70% y 90%
- 🟢 Verde: Menos del 70%

Agrega un campo de color a tu estructura:
```abap
TYPES: BEGIN OF ty_flight_ext,
         ...
         row_color TYPE lvc_t_scol,  " Campo de color
       END OF ty_flight_ext.
```

Calcula el color:
```abap
DATA: ls_color TYPE lvc_s_scol.

IF gs_flight_ext-percentage >= 90.
  ls_color-color-col = 6.  " Rojo
ELSEIF gs_flight_ext-percentage >= 70.
  ls_color-color-col = 3.  " Amarillo
ELSE.
  ls_color-color-col = 5.  " Verde
ENDIF.

ls_color-color-int = 1.
ls_color-color-inv = 0.
APPEND ls_color TO gs_flight_ext-row_color.
```

</details>

### 🥇 Nivel Avanzado

<details>
<summary>5️⃣ Crear un botón custom en el ALV</summary>

<br>

Agrega un botón "Calcular Ingresos" que multiplique precio × asientos ocupados.

1. Define el layout con botones:
```abap
DATA: gs_layout TYPE slis_layout_alv.

gs_layout-cwidth_opt = 'X'.  " Optimizar ancho de columnas
gs_layout-zebra      = 'X'.  " Efecto zebra (rayas)

CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
  EXPORTING
    i_callback_program      = sy-repid
    i_callback_user_command = 'USER_COMMAND'  " Callback para botones
    is_layout               = gs_layout
    it_fieldcat             = gt_fcat
  ...
```

2. Crea la subrutina que maneja el click:
```abap
FORM user_command USING r_ucomm     TYPE sy-ucomm
                        rs_selfield TYPE slis_selfield.

  CASE r_ucomm.
    WHEN '&IC1'.  " Doble click en fila
      " Código para manejar doble click
    WHEN 'CALC'.  " Botón custom
      " Calcular ingresos
      DATA: lv_ingreso TYPE p DECIMALS 2.
      READ TABLE gt_flights_ext INDEX rs_selfield-tabindex INTO gs_flight_ext.
      lv_ingreso = gs_flight_ext-price * gs_flight_ext-seatsocc.
      MESSAGE lv_ingreso TYPE 'I'.
  ENDCASE.

ENDFORM.
```

</details>

<details>
<summary>6️⃣ Exportar a un archivo Excel local</summary>

<br>

Agrega funcionalidad para exportar el resultado a Excel:

```abap
FORM export_to_excel.
  DATA: lv_filename TYPE string,
        lv_fullpath TYPE string.

  " Definir nombre del archivo
  lv_filename = 'Vuelos_Export.xlsx'.

  " Llamar a función de descarga
  CALL FUNCTION 'GUI_DOWNLOAD'
    EXPORTING
      filename              = lv_filename
      filetype              = 'ASC'
      write_field_separator = 'X'
    TABLES
      data_tab              = gt_flights
    EXCEPTIONS
      OTHERS                = 1.

  IF sy-subrc = 0.
    MESSAGE 'Archivo exportado exitosamente' TYPE 'S'.
  ENDIF.

ENDFORM.
```

Llama a esta subrutina en `END-OF-SELECTION`.

</details>

---

## 📖 Recursos Adicionales

### 🌐 Documentación Oficial SAP

- [ABAP Keyword Documentation](https://help.sap.com/doc/abapdocu_latest_index_htm/latest/en-US/index.htm)
- [ALV Grid Control](https://help.sap.com/docs/ABAP_PLATFORM/bas/alvs.html)
- [ABAP Programming Guidelines](https://help.sap.com/docs/ABAP_PLATFORM)

### 📚 Tablas de Demo en SAP

Para practicar, SAP incluye estas tablas de demostración:

| Tabla | Contenido | Ejemplo de Uso |
|-------|-----------|----------------|
| `SFLIGHT` | Vuelos | Listados de vuelos y precios |
| `SCARR` | Aerolíneas | Maestro de aerolíneas |
| `SPFLI` | Conexiones | Rutas de vuelo |
| `SBOOK` | Reservas | Reservaciones de vuelos |
| `MARA` | Materiales | Datos generales de materiales |
| `MARC` | Mat. por Centro | Materiales por centro de trabajo |

### 🎓 Transacciones Útiles

- **SE38**: ABAP Editor (crear/editar programas)
- **SE11**: ABAP Dictionary (ver estructura de tablas)
- **SE16**: Data Browser (ver contenido de tablas)
- **SE80**: Object Navigator (desarrollo orientado a objetos)
- **SE93**: Crear transacciones custom

---

## 🎉 ¡Felicidades!

Has completado tu primer programa ABAP con ALV. Ahora entiendes:

- ✅ Qué es un programa ABAP y para qué sirve
- ✅ La estructura de un programa ejecutable
- ✅ Los eventos principales y su orden de ejecución
- ✅ Cómo crear pantallas de selección
- ✅ Cómo consultar la base de datos con SELECT
- ✅ Cómo mostrar datos en formato ALV

---

## 🤝 Contribuciones

Si encuentras errores o tienes sugerencias para mejorar este material:

1. Fork este repositorio
2. Crea una rama con tu mejora
3. Envía un Pull Request

---

## 📝 Licencia

Este material es de uso educativo y está basado en estándares y mejores prácticas de ABAP.

---

## 🙋 Preguntas Frecuentes (FAQ)

<details>
<summary>❓ ¿Por qué empezar con la tabla SFLIGHT?</summary>

<br>

`SFLIGHT` es una tabla de **demostración** que viene precargada con datos en todos los sistemas SAP. Es perfecta para aprender porque:
- Tiene datos listos (no necesitas crearlos)
- Es fácil de entender (vuelos, aerolíneas, precios)
- Se usa en toda la documentación oficial de SAP
- Tiene una estructura simple pero completa

</details>

<details>
<summary>❓ ¿Qué pasa si no veo datos al ejecutar?</summary>

<br>

**Posibles causas:**
1. Los filtros están muy restrictivos → Amplía los rangos de fecha
2. La tabla está vacía (poco probable en SFLIGHT) → Verifica con SE16
3. Error en el SELECT → Revisa el log de errores

**Solución rápida:** Deja todos los filtros en blanco excepto el precio mínimo (bájalo a 0).

</details>

<details>
<summary>❓ ¿Puedo usar otra tabla en lugar de SFLIGHT?</summary>

<br>

¡Sí! Simplemente cambia:
1. La declaración: `TABLES: mi_tabla.`
2. El SELECT: `FROM mi_tabla`
3. Los tipos de datos: `TYPE mi_tabla` o `TYPE TABLE OF mi_tabla`
4. El Field Catalog con los campos de tu nueva tabla

**Ejemplo:** Cambiar a `MARA` (materiales):
```abap
TABLES: mara.
DATA: gt_materials TYPE TABLE OF mara.
SELECT * FROM mara INTO TABLE gt_materials WHERE matnr IN s_matnr.
```

</details>

<details>
<summary>❓ ¿Cómo puedo debuggear el programa?</summary>

<br>

**Opción 1:** Breakpoints
- Coloca el cursor en una línea
- Click en el margen izquierdo (aparece un ícono de stop 🔴)
- Ejecuta el programa (F8)
- Se detendrá en ese punto

**Opción 2:** Comando /h
- En la pantalla de selección, escribe `/h` en el campo de comando
- Presiona Enter
- El programa entrará en debug mode

**Opción 3:** BREAK-POINT
- Agrega `BREAK-POINT.` en tu código
- Equivalente a un breakpoint hard-coded

</details>

<details>
<summary>❓ ¿Qué significa sy-subrc?</summary>

<br>

`sy-subrc` = **System Return Code**

Es una variable del sistema que indica el resultado de la última operación:
- `sy-subrc = 0` → ✅ Éxito
- `sy-subrc <> 0` → ❌ Error o no se encontró

**Ejemplo:**
```abap
SELECT * FROM sflight INTO TABLE gt_flights WHERE carrid = 'XX'.
IF sy-subrc = 0.
  MESSAGE 'Datos encontrados' TYPE 'S'.
ELSE.
  MESSAGE 'No se encontraron datos' TYPE 'W'.
ENDIF.
```

</details>

---

<div align="center">

### 🌟 ¡Gracias por usar este material educativo! 🌟

Si te fue útil, no olvides darle una ⭐ a este repositorio

**Creado con ❤️ para estudiantes de ABAP**

</div>

---

**Versión:** 1.0  
**Última actualización:** Diciembre 2025  
**Compatible con:** SAP NetWeaver 7.40+  
**Autor:** Material Educativo para Estudiantes ABAP
