<!-- 
╔══════════════════════════════════════════════════════════════════════════════╗
║                    🎓 PRESENTACIÓN SAP RAP PARA ESTUDIANTES                  ║
║                         Estilo Diapositivas Interactivas                     ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

---

# 🚀 SLIDE 1: PORTADA

```
    ╔═══════════════════════════════════════════════════════════════════════╗
    ║                                                                       ║
    ║      ███████╗ █████╗ ██████╗     ██████╗  █████╗ ██████╗              ║
    ║      ██╔════╝██╔══██╗██╔══██╗    ██╔══██╗██╔══██╗██╔══██╗             ║
    ║      ███████╗███████║██████╔╝    ██████╔╝███████║██████╔╝             ║
    ║      ╚════██║██╔══██║██╔═══╝     ██╔══██╗██╔══██║██╔═══╝              ║
    ║      ███████║██║  ██║██║         ██║  ██║██║  ██║██║                  ║
    ║      ╚══════╝╚═╝  ╚═╝╚═╝         ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝                  ║
    ║                                                                       ║
    ║           RESTful Application Programming Model                       ║
    ║                                                                       ║
    ║                    🎯 Guía para Principiantes 🎯                       ║
    ║                                                                       ║
    ╚═══════════════════════════════════════════════════════════════════════╝
```

### 📚 Proyecto: Gestión de Proveedores (Vendors)
### 👨‍🎓 Nivel: Principiantes
### ⏱️ Duración estimada: 45 minutos

---

# 🎯 SLIDE 2: ¿QUÉ ES SAP RAP?

## 🤔 Imagina que quieres construir una casa...

```
    🏠 APLICACIÓN SAP
    ┌─────────────────────────────────────────────────────────────┐
    │                                                             │
    │   🧱 Necesitas:                                             │
    │      • Cimientos (Base de Datos)                            │
    │      • Estructura (CDS Views)                               │
    │      • Reglas de la casa (Behavior Definition)              │
    │      • Puerta de entrada (Service Definition)               │
    │      • Llave de la puerta (Service Binding)                 │
    │                                                             │
    └─────────────────────────────────────────────────────────────┘
```

## 📖 Definición Formal

> **SAP RAP** es el modelo de programación estándar de SAP para crear 
> aplicaciones **Fiori** y servicios **OData** de forma eficiente y moderna.

### ✨ Beneficios Clave:
| Beneficio | Descripción |
|-----------|-------------|
| 🚀 Rapidez | Desarrollo acelerado con patrones predefinidos |
| 🔒 Seguridad | Control de acceso integrado |
| 🎨 UI Moderna | Interfaces Fiori automáticas |
| 🔄 Reutilización | Componentes modulares |

---

# 🏗️ SLIDE 3: ARQUITECTURA RAP

## 📊 El Stack Completo

```
╔════════════════════════════════════════════════════════════════════════════╗
║                           🌐 USUARIO FINAL                                 ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │                    📱 APLICACIÓN FIORI                               │  ║
║  │                    (Interfaz de Usuario)                             │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           🔌 SERVICE BINDING (OData V2/V4)                           │  ║
║  │           "La llave que abre la puerta"                              │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           📋 SERVICE DEFINITION                                      │  ║
║  │           "Define qué exponemos al mundo"                            │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           📊 PROJECTION VIEW (Consumption)                           │  ║
║  │           "Vista adaptada para consumo"                              │  ║
║  │           + Metadata Extension (UI Annotations)                      │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           🧠 BEHAVIOR DEFINITION + IMPLEMENTATION                    │  ║
║  │           "Las reglas del negocio (CRUD + Validaciones)"             │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           👁️ CDS VIEW ENTITY (Interface View)                        │  ║
║  │           "Vista raíz - El corazón del modelo"                       │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                  │                                         ║
║                                  ▼                                         ║
║  ┌──────────────────────────────────────────────────────────────────────┐  ║
║  │           💾 DATABASE TABLE                                          │  ║
║  │           "Donde viven los datos"                                    │  ║
║  └──────────────────────────────────────────────────────────────────────┘  ║
║                                                                            ║
╚════════════════════════════════════════════════════════════════════════════╝
```

---

# 💾 SLIDE 4: LA BASE DE DATOS

## 🗄️ Tabla: `zds_table_1`

### 📝 Concepto
> La tabla es donde **almacenamos físicamente** los datos de nuestros proveedores.
> Es como un **Excel gigante** dentro de SAP.

### 💻 Código Completo

```abap
@EndUserText.label : 'TABLE FOR TESTING'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #RESTRICTED

define table zds_table_1 {

  key client      : abap.clnt not null;      -- 🔑 Mandante SAP
  key vendor_uuid : sysuuid_x16 not null;    -- 🔑 UUID único del vendor
  lifnr           : lifnr;                   -- 📋 Número de proveedor
  name            : name1_a;                 -- 📝 Nombre del proveedor
  land1           : land1;                   -- 🌍 País
  ort01           : ydort01;                 -- 🏙️ Ciudad

}
```

### 🔍 Explicación Campo por Campo

| Campo | Tipo | Descripción | Emoji |
|-------|------|-------------|-------|
| `client` | CLNT | Mandante SAP (siempre requerido) | 🏢 |
| `vendor_uuid` | UUID | Identificador único universal | 🔑 |
| `lifnr` | LIFNR | Número de proveedor tradicional | 📋 |
| `name` | NAME1_A | Nombre del proveedor | 👤 |
| `land1` | LAND1 | Código de país | 🌍 |
| `ort01` | ORT01 | Ciudad | 🏙️ |

### 💡 Tips Importantes

```
┌─────────────────────────────────────────────────────────────────────┐
│  💡 TIP #1: UUID vs ID Secuencial                                   │
│  ─────────────────────────────────────────────────────────────────  │
│  El UUID (sysuuid_x16) es preferido en RAP porque:                  │
│  • Es único globalmente 🌍                                          │
│  • Se puede generar automáticamente 🤖                              │
│  • No hay conflictos en replicación 🔄                              │
└─────────────────────────────────────────────────────────────────────┘
```

---

# 👁️ SLIDE 5: CDS VIEW ENTITY (Vista Raíz)

## 🎯 Vista de Interfaz: `ZDS_I_VENDOR_1`

### 📝 Concepto
> Es la **vista principal** que lee los datos de la tabla y los expone
> con nombres más amigables. Es como ponerle **etiquetas bonitas** 
> a las columnas de tu Excel.

### 💻 Código Completo

```abap
@AccessControl.authorizationCheck: #NOT_REQUIRED
define root view entity ZDS_I_VENDOR_1 
  as select from zds_table_1
{
  key vendor_uuid as VendorUuid,    -- 🔑 Clave primaria
      lifnr       as Vendor,        -- 📋 Alias: Vendor
      name        as Vendor_Name,   -- 📝 Alias: Vendor_Name
      land1       as Country,       -- 🌍 Alias: Country  
      ort01       as city           -- 🏙️ Alias: city
}
```

### 🔍 Anatomía de la Vista

```
┌────────────────────────────────────────────────────────────────────────────┐
│                                                                            │
│  @AccessControl.authorizationCheck: #NOT_REQUIRED                          │
│  ▲                                                                         │
│  └── 🔓 Sin chequeo de autorización (para demo)                            │
│                                                                            │
│  define root view entity ZDS_I_VENDOR_1                                    │
│          ▲                ▲                                                │
│          │                └── 📛 Nombre de la vista                        │
│          └── 🌳 "root" = Es la entidad principal                           │
│                                                                            │
│  as select from zds_table_1                                                │
│                 ▲                                                          │
│                 └── 💾 Tabla fuente de datos                               │
│                                                                            │
│  { key vendor_uuid as VendorUuid, ... }                                    │
│    ▲               ▲                                                       │
│    │               └── 📝 Alias (nombre amigable)                          │
│    └── 🔑 Marca el campo como clave                                        │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### 🎨 Convención de Nombres

```
    📋 TABLA (técnico)     →     👁️ VISTA (amigable)
    ─────────────────────────────────────────────────
    vendor_uuid            →     VendorUuid
    lifnr                  →     Vendor
    name                   →     Vendor_Name
    land1                  →     Country
    ort01                  →     city
```

---

# 📊 SLIDE 6: CONSUMPTION ENTITY (Proyección)

## 🎯 Vista de Consumo: `ZDS_C_VENDOR_1`

### 📝 Concepto
> Es una **proyección** de la vista de interfaz, optimizada para
> ser consumida por la UI. Piensa en ella como el **menú del restaurante**
> que muestra solo lo que el cliente puede pedir.

### 💻 Código Completo

```abap
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Conumption entity'
@Metadata.ignorePropagatedAnnotations: true
@Metadata.allowExtensions: true

define root view entity ZDS_C_VENDOR_1 
  provider contract transactional_query    -- 🔄 Contrato transaccional
  as projection on ZDS_I_VENDOR_1          -- 👁️ Proyecta sobre la vista I
{
    key VendorUuid,
        Vendor,
        Vendor_Name, 
        Country,
        city
}
```

### 🔍 Puntos Clave

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  📌 ANOTACIÓN                         🎯 PROPÓSITO                       │
│  ────────────────────────────────────────────────────────────────────    │
│                                                                          │
│  @Metadata.allowExtensions: true      Permite crear Metadata Extension   │
│  ▲                                                                       │
│  └── 🎨 ¡Importante para las anotaciones UI!                             │
│                                                                          │
│  provider contract transactional_query                                   │
│  ▲                                                                       │
│  └── 🔄 Define que esta vista soporta operaciones transaccionales        │
│                                                                          │
│  as projection on ZDS_I_VENDOR_1                                         │
│  ▲                                                                       │
│  └── 👁️ Indica que es una proyección (no select from)                    │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

### 🆚 ¿Por qué dos vistas?

```
┌─────────────────────────────┐     ┌─────────────────────────────┐
│     VISTA I (Interface)     │     │    VISTA C (Consumption)    │
├─────────────────────────────┤     ├─────────────────────────────┤
│ • Lógica de negocio         │     │ • Optimizada para UI        │
│ • Cálculos                  │ ──► │ • Proyección simple         │
│ • Joins complejos           │     │ • Anotaciones de UI         │
│ • Reutilizable              │     │ • Específica para escenario │
└─────────────────────────────┘     └─────────────────────────────┘
        🏭 FÁBRICA                          🍽️ RESTAURANTE
```

---

# 🎨 SLIDE 7: METADATA EXTENSION

## 🖼️ Anotaciones UI

### 📝 Concepto
> Las **Metadata Extensions** definen cómo se verá la aplicación Fiori.
> Es como el **diseñador de interiores** de tu aplicación.

### 💻 Código Completo

```abap
@Metadata.layer: #CORE

annotate view ZDS_C_VENDOR_1 with
{
  -- 📋 Definición de Facets (secciones en la pantalla de detalle)
  @UI.facet:[{ 
    id: 'idIdentification',
    purpose: #STANDARD,
    type: #IDENTIFICATION_REFERENCE,
    position: 10  
  }]

  -- 🔑 Campo: VendorUuid
  @UI: { 
    lineItem:       [{ position: 10 }],  -- 📊 Columna 1 en la lista
    identification: [{ position: 10 }]   -- 📝 Campo 1 en detalle
  }
  VendorUuid;

  -- 📋 Campo: Vendor (con filtro de búsqueda)
  @UI: { 
    lineItem:       [{ position: 20 }],
    identification: [{ position: 20 }],
    selectionField: [{ position: 10 }]   -- 🔍 ¡Aparece como filtro!
  }
  Vendor;

  -- 📝 Campo: Vendor_Name
  @UI: { 
    lineItem:       [{ position: 30 }],
    identification: [{ position: 30 }]
  }
  Vendor_Name;

  -- 🌍 Campo: Country
  @UI: { 
    lineItem:       [{ position: 40 }],
    identification: [{ position: 40 }]
  }
  Country;

  -- 🏙️ Campo: city
  @UI: { 
    lineItem:       [{ position: 50 }],
    identification: [{ position: 50 }]
  }
  city;
}
```

### 🖥️ Resultado Visual en Fiori

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  📱 APLICACIÓN FIORI: Gestión de Proveedores                                 │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  🔍 FILTROS (selectionField)                                                 │
│  ┌────────────────────────────────────────────────────────────────────────┐  │
│  │  Vendor: [________________] 🔎                                         │  │
│  └────────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
│  📊 LISTA (lineItem)                                                         │
│  ┌────────────┬──────────┬──────────────┬─────────┬────────┐                 │
│  │ VendorUuid │ Vendor   │ Vendor_Name  │ Country │ City   │                 │
│  ├────────────┼──────────┼──────────────┼─────────┼────────┤                 │
│  │ ABC123...  │ V001     │ Proveedor 1  │ CO      │ Bogotá │                 │
│  │ DEF456...  │ V002     │ Proveedor 2  │ MX      │ CDMX   │                 │
│  └────────────┴──────────┴──────────────┴─────────┴────────┘                 │
│                                                                              │
│  📝 DETALLE (identification) - Al hacer clic en una fila                     │
│  ┌────────────────────────────────────────────────────────────────────────┐  │
│  │  VendorUuid:   ABC123-DEF456-GHI789                                    │  │
│  │  Vendor:       V001                                                    │  │
│  │  Vendor_Name:  Proveedor 1                                             │  │
│  │  Country:      CO                                                      │  │
│  │  City:         Bogotá                                                  │  │
│  └────────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 📋 Resumen de Anotaciones UI

| Anotación | Ubicación | Descripción |
|-----------|-----------|-------------|
| `@UI.lineItem` | Lista | Define columnas en la tabla |
| `@UI.identification` | Detalle | Define campos en vista detalle |
| `@UI.selectionField` | Filtros | Define campos de búsqueda |
| `@UI.facet` | Estructura | Define secciones/pestañas |

---

# 🧠 SLIDE 8: BEHAVIOR DEFINITION

## ⚙️ El Cerebro de RAP

### 📝 Concepto
> El **Behavior Definition** define QUÉ operaciones están permitidas
> (crear, leer, actualizar, eliminar) y CÓMO se comportan los datos.

### 💻 Código Completo

```abap
managed implementation in class zbp_ds_i_vendor_1 unique;
strict ( 2 );

define behavior for ZDS_I_VENDOR_1
  persistent table zds_table_1        -- 💾 Tabla donde se guardan datos
  lock master                         -- 🔒 Control de bloqueos
  authorization master ( instance )   -- 🔐 Control de autorizaciones

{
  -- 🔒 Campo de solo lectura
  field ( readonly ) VendorUuid;

  -- 🔢 Numeración automática del UUID
  field ( numbering : managed ) VendorUuid;

  -- 📝 Operaciones CRUD
  create;   -- ➕ Crear
  update;   -- ✏️ Actualizar
  delete;   -- 🗑️ Eliminar

  -- 🔗 Mapeo entre vista y tabla
  mapping for zds_table_1
  {
    VendorUuid  = vendor_uuid;
    Vendor      = lifnr;
    Vendor_Name = name;
    Country     = land1;
    city        = ort01;
  }
}
```

### 🔍 Anatomía del Behavior

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                                                                              │
│  managed implementation in class zbp_ds_i_vendor_1 unique;                   │
│  ▲       ▲                        ▲                                          │
│  │       │                        └── 📦 Clase de implementación             │
│  │       └── 🤖 RAP maneja automáticamente las operaciones básicas           │
│  └── Tipo de implementación                                                  │
│                                                                              │
│  strict ( 2 );                                                               │
│  ▲                                                                           │
│  └── ⚠️ Modo estricto nivel 2 (más validaciones)                             │
│                                                                              │
│  persistent table zds_table_1                                                │
│  ▲                                                                           │
│  └── 💾 Los datos se guardan en esta tabla                                   │
│                                                                              │
│  field ( numbering : managed ) VendorUuid;                                   │
│  ▲                                                                           │
│  └── 🔢 SAP genera el UUID automáticamente                                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 🏭 Clase de Implementación

```abap
CLASS lhc_ZDS_I_VENDOR_1 DEFINITION INHERITING FROM cl_abap_behavior_handler.
  PRIVATE SECTION.

    METHODS get_instance_authorizations FOR INSTANCE AUTHORIZATION
      IMPORTING keys REQUEST requested_authorizations 
      FOR zds_i_vendor_1 RESULT result.

ENDCLASS.

CLASS lhc_ZDS_I_VENDOR_1 IMPLEMENTATION.

  METHOD get_instance_authorizations.
    " 🔐 Aquí implementamos la lógica de autorización
    " Por ahora está vacío (sin restricciones)
  ENDMETHOD.

ENDCLASS.
```

### 📊 Tipos de Implementation

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│  🤖 MANAGED                          📝 UNMANAGED                           │
│  ─────────────────                   ─────────────────                      │
│  • RAP hace todo automático          • Tú controlas todo                    │
│  • Ideal para casos simples          • Para lógica compleja                 │
│  • Menos código                      • Más flexibilidad                     │
│                                                                             │
│              ✅ NUESTRO PROYECTO USA MANAGED                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

# 📊 SLIDE 9: BEHAVIOR PROJECTION

## 🎭 Proyección del Comportamiento

### 📝 Concepto
> La **Behavior Projection** expone las operaciones de la vista I
> a través de la vista C. Es como el **menú de acciones** disponibles.

### 💻 Código Completo

```abap
projection;
strict ( 2 );

define behavior for ZDS_C_VENDOR_1 alias vendor
{
  use create;   -- ➕ Permitir crear
  use update;   -- ✏️ Permitir actualizar
  use delete;   -- 🗑️ Permitir eliminar
}
```

### 🔍 Explicación

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                                                                              │
│  projection;                                                                 │
│  ▲                                                                           │
│  └── 📋 Indica que es una proyección de behavior                             │
│                                                                              │
│  define behavior for ZDS_C_VENDOR_1 alias vendor                             │
│                      ▲               ▲                                       │
│                      │               └── 🏷️ Alias corto para usar en código  │
│                      └── 📊 Vista de consumo                                 │
│                                                                              │
│  use create;                                                                 │
│  ▲                                                                           │
│  └── 🔗 "Usa" la operación create definida en la vista I                     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 🔄 Flujo de Operaciones

```
    ┌─────────────────┐
    │   👤 USUARIO    │
    │  (Clic en +)    │
    └────────┬────────┘
             │
             ▼
    ┌─────────────────┐
    │ Behavior Proj.  │     "use create"
    │ ZDS_C_VENDOR_1  │─────────────────────┐
    └────────┬────────┘                     │
             │                              │
             ▼                              │
    ┌─────────────────┐                     │
    │ Behavior Def.   │◄────────────────────┘
    │ ZDS_I_VENDOR_1  │     Ejecuta "create"
    └────────┬────────┘
             │
             ▼
    ┌─────────────────┐
    │  💾 TABLA       │
    │ zds_table_1     │     Nuevo registro
    └─────────────────┘
```

---

# 🌐 SLIDE 10: SERVICE DEFINITION & BINDING

## 🚪 Exponiendo al Mundo

### 📝 Service Definition
> Define QUÉ entidades exponer como servicio OData.

```abap
@EndUserText.label: 'Service Def for CDS ENtity'

define service ZDS_UI_VENDOR_1 {
  expose ZDS_C_VENDOR_1;   -- 📤 Expone la vista de consumo
}
```

### 🔑 Service Binding
> Es la **activación** del servicio. Sin esto, el servicio no funciona.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                                                                              │
│  📋 SERVICE BINDING                                                          │
│  ──────────────────                                                          │
│                                                                              │
│  • Se crea en ADT (Eclipse) gráficamente                                     │
│  • Seleccionas OData V2 o V4                                                 │
│  • Activas el servicio                                                       │
│  • Obtienes una URL para consumir                                            │
│                                                                              │
│  🌐 Ejemplo de URL generada:                                                 │
│  https://servidor:puerto/sap/opu/odata/sap/ZDS_UI_VENDOR_1                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 🔄 Flujo Completo del Servicio

```
┌─────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ 📱 FIORI    │───►│ 🔑 SERVICE      │───►│ 📋 SERVICE      │
│    APP      │    │    BINDING      │    │    DEFINITION   │
│             │◄───│    (OData V2)   │◄───│                 │
└─────────────┘    └─────────────────┘    └────────┬────────┘
                                                   │
                                                   ▼
                   ┌─────────────────┐    ┌─────────────────┐
                   │ 🧠 BEHAVIOR     │◄───│ 📊 CONSUMPTION  │
                   │    DEFINITION   │    │    VIEW (C)     │
                   │                 │───►│                 │
                   └────────┬────────┘    └─────────────────┘
                            │
                            ▼
                   ┌─────────────────┐    ┌─────────────────┐
                   │ 👁️ INTERFACE    │───►│ 💾 DATABASE     │
                   │    VIEW (I)     │◄───│    TABLE        │
                   └─────────────────┘    └─────────────────┘
```

---

# 🎯 SLIDE 11: RESUMEN VISUAL COMPLETO

## 📊 El Proyecto Completo en Una Imagen

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                        🎯 PROYECTO SAP RAP COMPLETO                          ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║   1️⃣  💾 DATABASE TABLE: zds_table_1                                         ║
║       └── Almacena: vendor_uuid, lifnr, name, land1, ort01                   ║
║                              │                                               ║
║                              ▼                                               ║
║   2️⃣  👁️ CDS VIEW ENTITY: ZDS_I_VENDOR_1                                     ║
║       └── Expone datos con alias amigables                                   ║
║       └── Define la estructura base                                          ║
║                              │                                               ║
║           ┌──────────────────┴──────────────────┐                            ║
║           ▼                                     ▼                            ║
║   3️⃣  🧠 BEHAVIOR DEF                    4️⃣  📊 CONSUMPTION VIEW              ║
║       zbp_ds_i_vendor_1                      ZDS_C_VENDOR_1                  ║
║       └── managed                            └── projection on I            ║
║       └── create, update, delete             └── provider contract          ║
║       └── mapping                                      │                     ║
║           │                                            ▼                     ║
║           │                              5️⃣  🎨 METADATA EXTENSION            ║
║           │                                  └── @UI.lineItem               ║
║           │                                  └── @UI.identification         ║
║           │                                  └── @UI.selectionField         ║
║           │                                            │                     ║
║           └─────────┬───────────────────┬──────────────┘                     ║
║                     ▼                   ▼                                    ║
║   6️⃣  🎭 BEHAVIOR PROJECTION      7️⃣  📋 SERVICE DEFINITION                  ║
║       └── use create                   ZDS_UI_VENDOR_1                       ║
║       └── use update                   └── expose ZDS_C_VENDOR_1            ║
║       └── use delete                             │                           ║
║                                                  ▼                           ║
║                                    8️⃣  🔑 SERVICE BINDING                    ║
║                                        └── OData V2                          ║
║                                        └── URL activa                        ║
║                                                  │                           ║
║                                                  ▼                           ║
║                                    📱 APLICACIÓN FIORI                        ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

# 💡 SLIDE 12: TIPS Y MEJORES PRÁCTICAS

## 🏆 Consejos de Oro para RAP

### 📛 Convenciones de Nombres

```
┌─────────────────────────────────────────────────────────────────────┐
│  TIPO                 │  PREFIJO    │  EJEMPLO                      │
├───────────────────────┼─────────────┼───────────────────────────────┤
│  Tabla                │  Z + DS     │  zds_table_1                  │
│  Vista Interface      │  Z + DS_I   │  ZDS_I_VENDOR_1               │
│  Vista Consumption    │  Z + DS_C   │  ZDS_C_VENDOR_1               │
│  Behavior Class       │  ZBP_       │  zbp_ds_i_vendor_1            │
│  Service Definition   │  ZDS_UI     │  ZDS_UI_VENDOR_1              │
└───────────────────────┴─────────────┴───────────────────────────────┘
```

### ✅ DO's (Hacer)

```
✅ Usar UUID como clave primaria
✅ Separar vista I (interfaz) de vista C (consumo)
✅ Usar Metadata Extensions para UI
✅ Documentar con @EndUserText.label
✅ Empezar con 'managed' implementation
✅ Usar mapeos explícitos
```

### ❌ DON'Ts (No Hacer)

```
❌ Poner lógica de UI en vista I
❌ Mezclar concerns en una sola vista
❌ Olvidar el Service Binding
❌ Usar claves secuenciales (usar UUID)
❌ Hardcodear textos (usar i18n)
```

### 🐛 Errores Comunes

| Error | Causa | Solución |
|-------|-------|----------|
| "Service not found" | Binding no activado | Activar Service Binding |
| "Field not editable" | Campo readonly | Revisar Behavior Definition |
| "No data" | Mapping incorrecto | Verificar mapping de campos |
| "UI no muestra campos" | Falta Metadata Extension | Crear anotaciones @UI |

---

# 📚 SLIDE 13: RECURSOS Y PRÓXIMOS PASOS

## 🎓 Para Seguir Aprendiendo

### 📖 Documentación Oficial
- [SAP RAP Documentation](https://help.sap.com/docs/BTP/923180ddb98240829d935862025004d6/289477a81eec4d4e84c0302fb6835035.html)
- [ABAP RESTful Application Programming Model](https://help.sap.com/docs/ABAP_PLATFORM_NEW/fc4c71aa50014fd1b43721701471913d/289477a81eec4d4e84c0302fb6835035.html)

### 🎥 Tutoriales Recomendados
```
📺 SAP Learning Journey: RAP
📺 openSAP: Building Applications with RAP
📺 SAP Community: RAP Tutorials
```

### 🚀 Próximos Temas a Explorar

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│  📈 NIVEL INTERMEDIO                                                │
│  • Validaciones personalizadas                                      │
│  • Determinaciones (campos calculados)                              │
│  • Actions y Functions                                              │
│  • Draft handling                                                   │
│                                                                     │
│  🏆 NIVEL AVANZADO                                                  │
│  • Composición (entidades hijas)                                    │
│  • Authorization Control                                            │
│  • Feature Control                                                  │
│  • Side Effects                                                     │
│  • Integration con BAPIs                                            │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

# 🎉 SLIDE 14: ¡FELICITACIONES!

```
    ╔═══════════════════════════════════════════════════════════════════╗
    ║                                                                   ║
    ║                    🎊 ¡LO LOGRASTE! 🎊                            ║
    ║                                                                   ║
    ║     Ahora conoces los componentes básicos de SAP RAP:             ║
    ║                                                                   ║
    ║     ✅ Database Table                                             ║
    ║     ✅ CDS View Entity (Interface)                                ║
    ║     ✅ Consumption View (Projection)                              ║
    ║     ✅ Metadata Extension                                         ║
    ║     ✅ Behavior Definition                                        ║
    ║     ✅ Behavior Projection                                        ║
    ║     ✅ Service Definition                                         ║
    ║     ✅ Service Binding                                            ║
    ║                                                                   ║
    ║              🚀 ¡A CREAR TU PRIMERA APP RAP! 🚀                   ║
    ║                                                                   ║
    ╚═══════════════════════════════════════════════════════════════════╝
```

## 🤔 Preguntas de Repaso

1. ¿Cuál es la diferencia entre una vista I y una vista C?
2. ¿Para qué sirve el Behavior Definition?
3. ¿Qué anotación usamos para crear un filtro en Fiori?
4. ¿Por qué preferimos UUID sobre ID secuencial?
5. ¿Qué hace el Service Binding?

---

## 📝 Notas del Instructor

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  💡 SUGERENCIAS PARA LA CLASE                                               │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                             │
│  • Tiempo sugerido: 45-60 minutos                                           │
│  • Hacer pausas después de cada componente                                  │
│  • Mostrar el código en ADT mientras explicas                               │
│  • Dejar que los estudiantes repliquen el proyecto                          │
│  • Usar la app Fiori generada para demostrar el resultado                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

*📅 Creado para estudiantes principiantes de SAP RAP*
*🔄 Versión: 1.0*
*👨‍💻 Basado en el proyecto: Gestión de Proveedores (Vendors)*