# 📚 Programa ABAP Modularizado: Report con ALV e INCLUDEs

![SAP](https://img.shields.io/badge/SAP-0FAAFF?style=for-the-badge&logo=sap&logoColor=white)
![ABAP](https://img.shields.io/badge/ABAP-0FAAFF?style=for-the-badge&logo=sap&logoColor=white)
![NetWeaver](https://img.shields.io/badge/NetWeaver-7.40-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-Educational-blue?style=for-the-badge)
![Best Practices](https://img.shields.io/badge/Best_Practices-Modular-orange?style=for-the-badge)

> 🎓 **Material educativo para estudiantes que están aprendiendo ABAP desde cero**
> 
> Este documento te enseña a crear programas ABAP **profesionales y modularizados** usando INCLUDEs, tal como se hace en empresas reales. Incluye parámetros de entrada, consultas a base de datos y visualización ALV.

---

## 📑 Tabla de Contenidos

- [¿Qué es un Programa ABAP?](#-qué-es-un-programa-abap)
- [¿Para qué se usa un Programa ABAP?](#-para-qué-se-usa-un-programa-abap)
- [Tipos de Programas ABAP](#-tipos-de-programas-abap)
- [Estructura de un Programa ABAP](#%EF%B8%8F-estructura-de-un-programa-abap)
- [Eventos del Programa](#-eventos-del-programa)
- [Código Modularizado con INCLUDEs](#-código-modularizado-con-includes)
  - [¿Por qué modularizar?](#%EF%B8%8F-por-qué-modularizar-con-includes)
  - [Estructura del Programa](#-estructura-del-programa-modularizado)
  - [Programa Principal](#-programa-principal-z_basic_alv_demo)
  - [INCLUDE _TOP (Declaraciones)](#-include-z_basic_alv_demo_top-declaraciones)
  - [INCLUDE _SEL (Pantalla de Selección)](#-include-z_basic_alv_demo_sel-pantalla-de-selección)
  - [INCLUDE _EVT (Eventos)](#-include-z_basic_alv_demo_evt-eventos)
  - [INCLUDE _F01 (Subrutinas)](#-include-z_basic_alv_demo_f01-subrutinas)
  - [Comparativa: Monolítico vs Modularizado](#-comparativa-monolítico-vs-modularizado)
  - [Mejores Prácticas](#-mejores-prácticas-de-modularización)
- [Cómo Ejecutarlo](#%EF%B8%8F-cómo-ejecutarlo)
- [Resultado Esperado](#-resultado-esperado)
- [Conceptos Clave](#-conceptos-clave)
- [Ejercicios Adicionales](#-ejercicios-adicionales)
- [Recursos Adicionales](#-recursos-adicionales)
- [Preguntas Frecuentes (FAQ)](#-preguntas-frecuentes-faq)

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

## 💻 Código Modularizado con INCLUDEs

### 🏗️ ¿Por qué modularizar con INCLUDEs?

La **modularización con INCLUDEs** es una **mejor práctica estándar de SAP** que ofrece:

- ✅ **Organización**: Código separado por responsabilidades
- ✅ **Mantenibilidad**: Más fácil encontrar y modificar código
- ✅ **Trabajo en equipo**: Varios desarrolladores pueden trabajar en paralelo
- ✅ **Reutilización**: Los INCLUDEs pueden ser compartidos
- ✅ **Profesionalismo**: Así se estructura el código en empresas reales

### 📦 Estructura del Programa Modularizado

```
┌────────────────────────────────────────────────────────────────┐
│  Z_BASIC_ALV_DEMO (Programa Principal)                        │
│                                                                │
│  REPORT z_basic_alv_demo.                                     │
│                                                                │
│  INCLUDE z_basic_alv_demo_top.  ← Declaraciones globales     │
│  INCLUDE z_basic_alv_demo_sel.  ← Pantalla de selección      │
│  INCLUDE z_basic_alv_demo_evt.  ← Eventos (INITIALIZATION...) │
│  INCLUDE z_basic_alv_demo_f01.  ← Subrutinas (FORMs)         │
└────────────────────────────────────────────────────────────────┘
         │              │              │              │
         ▼              ▼              ▼              ▼
    ┌────────┐    ┌────────┐    ┌────────┐    ┌────────┐
    │  _TOP  │    │  _SEL  │    │  _EVT  │    │  _F01  │
    │TABLES  │    │PARAMS  │    │ INIT   │    │ FORMS  │
    │DATA    │    │SELECT- │    │AT SEL  │    │SUBs    │
    │TYPES   │    │OPTIONS │    │START-OF│    │        │
    │        │    │        │    │END-OF  │    │        │
    └────────┘    └────────┘    └────────┘    └────────┘
```

---

### 📄 PROGRAMA PRINCIPAL: `Z_BASIC_ALV_DEMO`

```abap
*&---------------------------------------------------------------------*
*& Report Z_BASIC_ALV_DEMO
*&---------------------------------------------------------------------*
*& Programa educativo: Introducción a Reports ABAP con ALV
*& Objetivo: Mostrar estructura modularizada con INCLUDEs
*& Tabla: SFLIGHT (Datos de vuelos - tabla estándar de demo)
*&---------------------------------------------------------------------*
*& ESTRUCTURA DEL PROGRAMA:
*&   - Z_BASIC_ALV_DEMO_TOP : Declaraciones globales
*&   - Z_BASIC_ALV_DEMO_SEL : Pantalla de selección
*&   - Z_BASIC_ALV_DEMO_EVT : Eventos del programa
*&   - Z_BASIC_ALV_DEMO_F01 : Subrutinas (FORMs)
*&---------------------------------------------------------------------*

REPORT z_basic_alv_demo.

*----------------------------------------------------------------------*
* INCLUDES - Modularización del programa
*----------------------------------------------------------------------*
INCLUDE z_basic_alv_demo_top.  " Declaraciones globales
INCLUDE z_basic_alv_demo_sel.  " Pantalla de selección
INCLUDE z_basic_alv_demo_evt.  " Eventos del programa
INCLUDE z_basic_alv_demo_f01.  " Subrutinas
```

---

### 📄 INCLUDE `Z_BASIC_ALV_DEMO_TOP` (Declaraciones)

**Contenido:** TABLES, DATA, TYPES, CONSTANTS

```abap
*&---------------------------------------------------------------------*
*& Include Z_BASIC_ALV_DEMO_TOP
*&---------------------------------------------------------------------*
*& Declaraciones globales del programa
*& - Tablas de base de datos
*& - Variables globales
*& - Tipos de datos custom
*& - Constantes
*&---------------------------------------------------------------------*

*----------------------------------------------------------------------*
* DECLARACIÓN DE TABLAS
*----------------------------------------------------------------------*
TABLES: sflight.  " Tabla de base de datos: información de vuelos

*----------------------------------------------------------------------*
* TIPOS DE DATOS CUSTOM (si se necesitan)
*----------------------------------------------------------------------*
" Ejemplo: si quisieras extender la estructura de SFLIGHT
" TYPES: BEGIN OF ty_flight_ext,
"          carrid     TYPE sflight-carrid,
"          connid     TYPE sflight-connid,
"          fldate     TYPE sflight-fldate,
"          price      TYPE sflight-price,
"          percentage TYPE p DECIMALS 2,
"        END OF ty_flight_ext.

*----------------------------------------------------------------------*
* DECLARACIÓN DE DATOS GLOBALES
*----------------------------------------------------------------------*
DATA: gt_flights TYPE TABLE OF sflight,   " Tabla interna: vuelos
      gs_flight  TYPE sflight,            " Estructura de trabajo
      gt_fcat    TYPE slis_t_fieldcat_alv," Catálogo de campos ALV
      gv_lines   TYPE i.                  " Contador de registros

*----------------------------------------------------------------------*
* CONSTANTES (si se necesitan)
*----------------------------------------------------------------------*
" CONSTANTS: gc_precio_min TYPE p DECIMALS 2 VALUE '100.00'.
```

---

### 📄 INCLUDE `Z_BASIC_ALV_DEMO_SEL` (Pantalla de Selección)

**Contenido:** PARAMETERS, SELECT-OPTIONS, SELECTION-SCREEN

```abap
*&---------------------------------------------------------------------*
*& Include Z_BASIC_ALV_DEMO_SEL
*&---------------------------------------------------------------------*
*& Pantalla de selección del programa
*& - Parámetros de entrada
*& - Rangos de selección
*& - Layout de la pantalla
*&---------------------------------------------------------------------*

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
* TEXT-001: 'Parámetros de Selección de Vuelos'
* 
* Para crear los textos:
* 1. Ir a SE38 → Pasar a → Elementos de texto → Textos de selección
* 2. Asignar el texto "Parámetros de Selección de Vuelos" a TEXT-001
```

---

### 📄 INCLUDE `Z_BASIC_ALV_DEMO_EVT` (Eventos)

**Contenido:** INITIALIZATION, AT SELECTION-SCREEN, START-OF-SELECTION, END-OF-SELECTION

```abap
*&---------------------------------------------------------------------*
*& Include Z_BASIC_ALV_DEMO_EVT
*&---------------------------------------------------------------------*
*& Eventos del programa
*& - INITIALIZATION: Valores por defecto
*& - AT SELECTION-SCREEN: Validaciones de entrada
*& - START-OF-SELECTION: Lógica principal
*& - END-OF-SELECTION: Presentación de resultados
*&---------------------------------------------------------------------*

*----------------------------------------------------------------------*
* EVENTO 1: INITIALIZATION
* Se ejecuta UNA SOLA VEZ al cargar el programa
* Propósito: Establecer valores por defecto en la pantalla de selección
*----------------------------------------------------------------------*
INITIALIZATION.
  " Establecer fecha de hoy como valor por defecto en el rango
  s_fldate-sign   = 'I'.          " I = Include (incluir)
  s_fldate-option = 'BT'.         " BT = Between (entre)
  s_fldate-low    = sy-datum.     " Fecha de hoy
  s_fldate-high   = sy-datum + 30." +30 días desde hoy
  APPEND s_fldate.

  " Mensaje informativo (opcional - para demostración)
  WRITE: / '🎬 INITIALIZATION ejecutado: Valores por defecto establecidos'.
  SKIP 1.

*----------------------------------------------------------------------*
* EVENTO 2: AT SELECTION-SCREEN
* Se ejecuta al presionar F8 o botón Ejecutar
* Propósito: Validar las entradas del usuario ANTES de procesar
*----------------------------------------------------------------------*
AT SELECTION-SCREEN.
  " Validación 1: El precio mínimo debe ser mayor a cero
  IF p_price <= 0.
    MESSAGE 'El precio mínimo debe ser mayor a 0' TYPE 'E'.
  ENDIF.

  " Validación 2: Al menos una aerolínea debe estar especificada
  IF s_carrid[] IS INITIAL.
    MESSAGE 'Debe especificar al menos una aerolínea' TYPE 'W'.
  ENDIF.

  " Mensaje informativo (opcional - para demostración)
  WRITE: / '✅ AT SELECTION-SCREEN ejecutado: Validaciones OK'.
  SKIP 1.

*----------------------------------------------------------------------*
* EVENTO 3: START-OF-SELECTION
* Aquí va la LÓGICA PRINCIPAL del programa
* Propósito: Consultar datos, procesarlos, hacer cálculos
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
    STOP.  " Detener ejecución del programa
  ELSE.
    WRITE: / '✅ Se encontraron', gv_lines, 'vuelos.'.
    SKIP 1.
  ENDIF.

*----------------------------------------------------------------------*
* EVENTO 4: END-OF-SELECTION
* Se ejecuta DESPUÉS de START-OF-SELECTION
* Propósito: Presentar los resultados al usuario (display, output)
*----------------------------------------------------------------------*
END-OF-SELECTION.
  WRITE: / '🎨 END-OF-SELECTION: Preparando visualización ALV...'.
  SKIP 1.

  " Llamar a subrutinas para preparar y mostrar el ALV
  " Nota: Las subrutinas están en el INCLUDE Z_BASIC_ALV_DEMO_F01

  " Paso 1: Construir el catálogo de campos
  PERFORM build_field_catalog CHANGING gt_fcat.

  " Paso 2: Mostrar los datos en formato ALV Grid
  PERFORM display_alv USING gt_flights
                            gt_fcat.
```

---

### 📄 INCLUDE `Z_BASIC_ALV_DEMO_F01` (Subrutinas)

**Contenido:** FORMs (subrutinas reutilizables)

```abap
*&---------------------------------------------------------------------*
*& Include Z_BASIC_ALV_DEMO_F01
*&---------------------------------------------------------------------*
*& Subrutinas del programa
*& - FORMs para procesamiento y presentación de datos
*& - Lógica modular y reutilizable
*&---------------------------------------------------------------------*

*----------------------------------------------------------------------*
* SUBRUTINA: BUILD_FIELD_CATALOG
* Construye el catálogo de campos que define las columnas del ALV
*----------------------------------------------------------------------*
* Propósito:
*   Define qué campos mostrar, en qué orden, con qué títulos, etc.
*
* Parámetros:
*   CHANGING ct_fcat - Catálogo de campos (tabla a llenar)
*----------------------------------------------------------------------*
FORM build_field_catalog CHANGING ct_fcat TYPE slis_t_fieldcat_alv.

  DATA: ls_fcat TYPE slis_fieldcat_alv.  " Estructura local de trabajo

  " Campo 1: CARRID (Aerolínea)
  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CARRID'.      " Nombre del campo en la tabla interna
  ls_fcat-seltext_l = 'Aerolínea'.   " Título de la columna (largo)
  ls_fcat-col_pos   = 1.             " Posición de la columna
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
  ls_fcat-do_sum    = 'X'.           " Activar suma automática para este campo
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
* Propósito:
*   Llamar a la función estándar de SAP para mostrar datos en ALV
*
* Parámetros:
*   USING it_flights - Tabla con los datos a mostrar
*   USING it_fcat    - Catálogo de campos del ALV
*----------------------------------------------------------------------*
FORM display_alv USING it_flights TYPE STANDARD TABLE
                       it_fcat    TYPE slis_t_fieldcat_alv.

  " Llamar a la función estándar de ALV
  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program = sy-repid    " Nombre del programa actual
      it_fieldcat        = it_fcat     " Catálogo de campos (parámetro)
      i_grid_title       = 'Listado de Vuelos (SFLIGHT)'  " Título del ALV
    TABLES
      t_outtab           = it_flights  " Tabla de datos a mostrar (parámetro)
    EXCEPTIONS
      program_error      = 1
      OTHERS             = 2.

  " Verificar si hubo errores al mostrar el ALV
  IF sy-subrc <> 0.
    MESSAGE 'Error al mostrar ALV' TYPE 'E'.
  ENDIF.

ENDFORM.
```

---

### 📊 Comparativa: Monolítico vs Modularizado

| Aspecto | Programa Monolítico | Programa Modularizado |
|---------|---------------------|----------------------|
| **Tamaño de archivo** | 1 archivo grande (200-500+ líneas) | 5 archivos pequeños (50-150 líneas c/u) |
| **Búsqueda de código** | Buscar en todo el archivo | Ir directo al INCLUDE correspondiente |
| **Trabajo en equipo** | ❌ Solo 1 persona puede editar | ✅ Varios desarrolladores en paralelo |
| **Mantenimiento** | ❌ Difícil encontrar código específico | ✅ Fácil localizar por responsabilidad |
| **Reutilización** | ❌ Difícil reutilizar partes | ✅ INCLUDEs compartibles entre programas |
| **Organización** | ❌ Todo mezclado | ✅ Separado por tipo de código |
| **Profesionalismo** | Para programas pequeños/demos | ✅ Estándar en producción empresarial |

---

### ✅ Mejores Prácticas de Modularización

<details>
<summary>📏 <b>¿Cuándo usar INCLUDEs?</b></summary>

<br>

| Tamaño del Programa | Recomendación |
|---------------------|---------------|
| **< 200 líneas** | Programa monolítico está bien (para aprendizaje/prototipos) |
| **200-500 líneas** | Considera usar INCLUDEs para mejor organización |
| **> 500 líneas** | **Obligatorio usar INCLUDEs** (estándar empresarial) |
| **Proyectos reales** | **Siempre usar INCLUDEs** desde el inicio |

**Regla de oro:** 
> "Si el programa será usado en producción o mantenido por un equipo, usa INCLUDEs desde el principio."

</details>

<details>
<summary>🎯 <b>Convención de nombres SAP</b></summary>

<br>

SAP tiene convenciones estándar para nombres de INCLUDEs:

```
Programa:          Z[EMPRESA]_[MODULO]_[FUNCION]
                   └─── Ejemplo: ZACME_MM_INVENTORY_REPORT

INCLUDEs:          Z[EMPRESA]_[MODULO]_[FUNCION]_[SUFIJO]
                   └─── Ejemplo: ZACME_MM_INVENTORY_REPORT_TOP
```

**Sufijos estándar:**

| Sufijo | Tipo | Descripción | Ejemplo |
|--------|------|-------------|---------|
| `_TOP` | Declaraciones | Tablas, datos, tipos | `ZPROG_TOP` |
| `_SEL` | Selección | Pantalla de selección | `ZPROG_SEL` |
| `_F01` | Subrutinas | FORMs principales | `ZPROG_F01` |
| `_F02` | Subrutinas | FORMs secundarias | `ZPROG_F02` |
| `_C01` | Clases | Clases locales (OO) | `ZPROG_C01` |
| `_O01` | Output | Eventos de salida | `ZPROG_O01` |
| `_I01` | Input | Procesamiento entrada | `ZPROG_I01` |
| `_PBO` | Dynpro | Process Before Output | `ZPROG_PBO` |
| `_PAI` | Dynpro | Process After Input | `ZPROG_PAI` |

</details>

<details>
<summary>⚠️ <b>Errores comunes al modularizar</b></summary>

<br>

#### ❌ Error 1: Dependencias circulares
```abap
" MALO - No hacer esto
INCLUDE zprog_f01.  " Usa variables de _TOP
INCLUDE zprog_top.  " Declaradas después ❌
```
**Solución:** Siempre incluir `_TOP` primero.

#### ❌ Error 2: Datos en INCLUDEs equivocados
```abap
" MALO - No declarar variables en _F01
FORM mi_subrutina.
  DATA: lv_global TYPE i.  " ❌ Debería estar en _TOP si es global
ENDFORM.
```
**Solución:** Variables globales en `_TOP`, variables locales dentro de FORMs.

#### ❌ Error 3: Código de eventos en _F01
```abap
" MALO - No poner eventos en include de subrutinas
" En Z_PROG_F01:
START-OF-SELECTION.  " ❌ Debería estar en _EVT
  PERFORM procesar.
ENDFORM.
```
**Solución:** Eventos van en `_EVT`, subrutinas en `_F01`.

#### ❌ Error 4: No comentar propósito de INCLUDEs
```abap
" MALO
INCLUDE zprog_top.
INCLUDE zprog_f01.
```

```abap
" BUENO ✅
INCLUDE zprog_top.  " Declaraciones globales: tablas, datos, tipos
INCLUDE zprog_f01.  " Subrutinas de procesamiento
```

</details>

<details>
<summary>🚀 <b>Ventajas en equipos de desarrollo</b></summary>

<br>

### Escenario Real: Equipo de 3 Desarrolladores

**Sin modularización:**
```
Desarrollador 1: Editando líneas 1-300
Desarrollador 2: ⏳ Esperando... (no puede editar)
Desarrollador 3: ⏳ Esperando... (no puede editar)
```

**Con modularización:**
```
Desarrollador 1: Editando Z_PROG_TOP (declaraciones)
Desarrollador 2: Editando Z_PROG_F01 (subrutinas) ✅
Desarrollador 3: Editando Z_PROG_EVT (eventos) ✅
```

**Beneficios:**
- ✅ **3x más productivo**: Trabajo en paralelo
- ✅ **Menos conflictos**: Cada uno en su INCLUDE
- ✅ **Merge más fácil**: Cambios en archivos separados
- ✅ **Code review claro**: Se revisa por responsabilidad

</details>

---

### 🎯 ¿Qué va en cada INCLUDE?

| INCLUDE | Sufijo | Contenido | ¿Cuándo usarlo? |
|---------|--------|-----------|-----------------|
| **_TOP** | TOP | `TABLES`, `DATA`, `TYPES`, `CONSTANTS` | Siempre - declaraciones globales |
| **_SEL** | SEL | `PARAMETERS`, `SELECT-OPTIONS`, `SELECTION-SCREEN` | Si el programa tiene pantalla de selección |
| **_F01** | F01 | `FORM ... ENDFORM` | Si tienes subrutinas (FORMs) |
| **_O01** | O01 | Eventos de output (listas) | Si generas listas clásicas |
| **_I01** | I01 | Subrutinas de input | Para validaciones complejas |
| **_C01** | C01 | Clases locales (`CLASS ... ENDCLASS`) | Si usas ABAP OO en el programa |

> 💡 **Convención de nombres:**
> - Programa: `Z_[NOMBRE]`
> - INCLUDEs: `Z_[NOMBRE]_[SUFIJO]`
> 
> El sistema SAP propone automáticamente estos nombres al crear INCLUDEs.

---

## ▶️ Cómo Ejecutarlo

### 🎯 Opción A: Crear Programa Modularizado con INCLUDEs (RECOMENDADO)

Esta es la forma **profesional** usada en empresas. Crearás 5 archivos separados.

#### Paso 1️⃣: Crear el Programa Principal

1. Ejecuta la transacción **SE38** (ABAP Editor)
2. En el campo "Programa", ingresa: `Z_BASIC_ALV_DEMO`
3. Click en **"Crear"** (o F5)

#### Paso 2️⃣: Configurar Atributos

| Campo | Valor |
|-------|-------|
| **Título** | `Programa Demo: ALV Modularizado con INCLUDEs` |
| **Tipo** | `Programa ejecutable` |
| **Estado** | `Programa de prueba o demo` |

Click en **"Guardar"** → Selecciona **"Objeto local"**

#### Paso 3️⃣: Ingresar Código del Programa Principal

Copia **solo** el código del "PROGRAMA PRINCIPAL" (el que tiene los INCLUDEs):

```abap
REPORT z_basic_alv_demo.

INCLUDE z_basic_alv_demo_top.
INCLUDE z_basic_alv_demo_sel.
INCLUDE z_basic_alv_demo_evt.
INCLUDE z_basic_alv_demo_f01.
```

**✅ Verificar sintaxis** (Ctrl+F2) - Dará warnings porque los INCLUDEs no existen aún.

#### Paso 4️⃣: Crear los INCLUDEs Automáticamente

SAP te ayuda a crear los INCLUDEs:

1. **Doble click** en la línea `INCLUDE z_basic_alv_demo_top.`
2. Aparece popup: **"Objeto Z_BASIC_ALV_DEMO_TOP no existe. ¿Crear?"**
3. Click en **"Sí"**
4. Configurar:
   - **Tipo**: `Include`
   - **Título**: `Declaraciones globales`
5. Click **"Guardar"** → "Objeto local"
6. Copia el código correspondiente del INCLUDE `_TOP`
7. **Activar** (Ctrl+F3)

**Repite el Paso 4 para cada INCLUDE:**
- `z_basic_alv_demo_sel` → "Pantalla de selección"
- `z_basic_alv_demo_evt` → "Eventos del programa"
- `z_basic_alv_demo_f01` → "Subrutinas"

#### Paso 5️⃣: Activar el Programa Principal

1. Regresa al programa principal (SE38 → Z_BASIC_ALV_DEMO)
2. **Verificar** (Ctrl+F2) → Ahora no debe haber errores
3. **Activar** (Ctrl+F3)

#### Paso 6️⃣: Ejecutar

1. Click en **"Ejecutar"** (F8)
2. Pantalla de selección aparecerá
3. Ajusta parámetros si deseas
4. **F8** nuevamente para ver resultados

---

### 🔧 Opción B: Crear Programa Monolítico (Para Aprendizaje Rápido)

Si quieres probar rápidamente sin modularizar:

<details>
<summary>📝 <b>Click para ver código monolítico completo</b></summary>

<br>

```abap
*&---------------------------------------------------------------------*
*& Report Z_BASIC_ALV_DEMO_MONO
*&---------------------------------------------------------------------*
REPORT z_basic_alv_demo_mono.

*----------------------------------------------------------------------*
* DECLARACIONES
*----------------------------------------------------------------------*
TABLES: sflight.
DATA: gt_flights TYPE TABLE OF sflight,
      gs_flight  TYPE sflight,
      gt_fcat    TYPE slis_t_fieldcat_alv,
      gv_lines   TYPE i.

*----------------------------------------------------------------------*
* PANTALLA DE SELECCIÓN
*----------------------------------------------------------------------*
SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.
  SELECT-OPTIONS: s_carrid FOR sflight-carrid,
                  s_connid FOR sflight-connid,
                  s_fldate FOR sflight-fldate.
  PARAMETERS: p_price TYPE sflight-price DEFAULT 500.
SELECTION-SCREEN END OF BLOCK b1.

*----------------------------------------------------------------------*
* EVENTOS
*----------------------------------------------------------------------*
INITIALIZATION.
  s_fldate-sign   = 'I'.
  s_fldate-option = 'BT'.
  s_fldate-low    = sy-datum.
  s_fldate-high   = sy-datum + 30.
  APPEND s_fldate.

AT SELECTION-SCREEN.
  IF p_price <= 0.
    MESSAGE 'El precio mínimo debe ser mayor a 0' TYPE 'E'.
  ENDIF.

START-OF-SELECTION.
  SELECT * FROM sflight INTO TABLE gt_flights
    WHERE carrid IN s_carrid
      AND connid IN s_connid
      AND fldate IN s_fldate
      AND price  >= p_price.

  DESCRIBE TABLE gt_flights LINES gv_lines.
  IF gv_lines = 0.
    MESSAGE 'No se encontraron vuelos' TYPE 'I'.
    STOP.
  ENDIF.

END-OF-SELECTION.
  PERFORM build_field_catalog CHANGING gt_fcat.
  PERFORM display_alv USING gt_flights gt_fcat.

*----------------------------------------------------------------------*
* SUBRUTINAS
*----------------------------------------------------------------------*
FORM build_field_catalog CHANGING ct_fcat TYPE slis_t_fieldcat_alv.
  DATA: ls_fcat TYPE slis_fieldcat_alv.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CARRID'.
  ls_fcat-seltext_l = 'Aerolínea'.
  ls_fcat-col_pos   = 1.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CONNID'.
  ls_fcat-seltext_l = 'Conexión'.
  ls_fcat-col_pos   = 2.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'FLDATE'.
  ls_fcat-seltext_l = 'Fecha Vuelo'.
  ls_fcat-col_pos   = 3.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'PRICE'.
  ls_fcat-seltext_l = 'Precio'.
  ls_fcat-col_pos   = 4.
  ls_fcat-do_sum    = 'X'.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'CURRENCY'.
  ls_fcat-seltext_l = 'Moneda'.
  ls_fcat-col_pos   = 5.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'PLANETYPE'.
  ls_fcat-seltext_l = 'Tipo Avión'.
  ls_fcat-col_pos   = 6.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'SEATSMAX'.
  ls_fcat-seltext_l = 'Asientos Max'.
  ls_fcat-col_pos   = 7.
  APPEND ls_fcat TO ct_fcat.

  CLEAR ls_fcat.
  ls_fcat-fieldname = 'SEATSOCC'.
  ls_fcat-seltext_l = 'Asientos Ocup'.
  ls_fcat-col_pos   = 8.
  APPEND ls_fcat TO ct_fcat.
ENDFORM.

FORM display_alv USING it_flights TYPE STANDARD TABLE
                       it_fcat    TYPE slis_t_fieldcat_alv.
  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program = sy-repid
      it_fieldcat        = it_fcat
      i_grid_title       = 'Listado de Vuelos (SFLIGHT)'
    TABLES
      t_outtab           = it_flights
    EXCEPTIONS
      program_error      = 1
      OTHERS             = 2.

  IF sy-subrc <> 0.
    MESSAGE 'Error al mostrar ALV' TYPE 'E'.
  ENDIF.
ENDFORM.
```

Crea este programa en SE38 como `Z_BASIC_ALV_DEMO_MONO` y ejecuta con F8.

</details>

---

### 📁 Navegando entre INCLUDEs en SE38

Una vez creados los INCLUDEs, puedes navegar fácilmente:

1. **Doble click** en cualquier línea `INCLUDE ...` para abrir ese archivo
2. **F3** (Atrás) para regresar al programa principal
3. **SE80** (Object Navigator) te muestra todos los INCLUDEs en árbol:

```
📁 Z_BASIC_ALV_DEMO
├── 📄 Z_BASIC_ALV_DEMO (Principal)
├── 📄 Z_BASIC_ALV_DEMO_TOP
├── 📄 Z_BASIC_ALV_DEMO_SEL
├── 📄 Z_BASIC_ALV_DEMO_EVT
└── 📄 Z_BASIC_ALV_DEMO_F01
```

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

Has completado tu primer programa ABAP **profesional y modularizado**. Ahora entiendes:

- ✅ Qué es un programa ABAP y para qué sirve
- ✅ La estructura de un programa ejecutable
- ✅ Los eventos principales y su orden de ejecución
- ✅ Cómo crear pantallas de selección
- ✅ Cómo consultar la base de datos con SELECT
- ✅ Cómo mostrar datos en formato ALV
- ✅ **Cómo modularizar programas con INCLUDEs** (estándar empresarial)
- ✅ **Mejores prácticas de organización de código**
- ✅ **Trabajo en equipo con código modular**

### 🚀 Próximos Pasos

Ahora que dominas la estructura básica, puedes avanzar a:

1. **ABAP Orientado a Objetos**: Clases, métodos, herencia
2. **CDS Views**: Vistas de datos en HANA
3. **SAP Fiori**: Interfaces modernas con UI5
4. **RAP (RESTful ABAP Programming)**: Framework moderno de SAP
5. **Debugging avanzado**: Breakpoints condicionales, watchpoints

**Recuerda:** La modularización con INCLUDEs es tu primer paso hacia el desarrollo profesional de SAP. ¡Úsala siempre en proyectos reales!

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

<details>
<summary>❓ ¿Debo usar siempre INCLUDEs incluso para programas pequeños?</summary>

<br>

**Para aprendizaje/prototipos:**
- Programas < 200 líneas → Monolítico está bien
- Te permite enfocarte en aprender la lógica sin preocuparte por la estructura

**Para producción/trabajo real:**
- **Siempre usa INCLUDEs desde el inicio**, incluso si el programa es pequeño
- Es más fácil empezar modularizado que refactorizar después
- Los programas pequeños tienden a crecer con el tiempo

**Ventaja de aprender con INCLUDEs:**
- Te acostumbras a pensar de forma modular
- Desarrollas hábitos profesionales desde el principio
- Tu código será mejor valorado en entrevistas/code reviews

**Regla práctica:**
> "Si el código será visto por otros desarrolladores o usado en producción, usa INCLUDEs."

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
