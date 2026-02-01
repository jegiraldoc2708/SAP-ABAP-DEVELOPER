# 🚀 Guía de ABAP Cloud para Desarrolladores ABAP Clásico

> **Objetivo:** Entender qué es ABAP Cloud, por qué existe y cómo se diferencia del modelo de programación ABAP clásico que ya conoces.

---

## 📋 Tabla de Contenidos

1. [¿Qué es ABAP Cloud?](#1-qué-es-abap-cloud)
2. [¿Por qué necesitamos ABAP Cloud?](#2-por-qué-necesitamos-abap-cloud)
3. [ABAP Clásico vs ABAP Cloud - Comparativa](#3-abap-clásico-vs-abap-cloud---comparativa)
4. [Conceptos Clave de ABAP Cloud](#4-conceptos-clave-de-abap-cloud)
5. [Arquitectura de ABAP Cloud](#5-arquitectura-de-abap-cloud)
6. [Escenarios de Desarrollo](#6-escenarios-de-desarrollo)
7. [¿Por dónde empezar?](#7-por-dónde-empezar)

---

## 1. ¿Qué es ABAP Cloud?

**ABAP Cloud es el modelo de desarrollo ABAP para construir aplicaciones, servicios y extensiones listas para la nube.**

### Definición según SAP:

> *"ABAP Cloud is the ABAP development model used to build cloud-ready business apps, services, and extensions."*
> 
> — SAP ABAP Cloud Landing Page

### En palabras simples:

ABAP Cloud **no es un lenguaje nuevo**. Es una **forma estandarizada de programar en ABAP** que funciona tanto en la nube pública como en sistemas on-premise. Piénsalo como "las reglas del juego modernas" para desarrollar en ABAP.

### ¿Por qué se creó?

ABAP fue diseñado originalmente para aplicaciones empresariales. Con el tiempo, se añadieron nuevos conceptos, tecnologías y sentencias, pero **no todas están preparadas para la tecnología cloud**. Por eso, SAP necesitaba definir claramente qué tecnologías y elementos del lenguaje pueden soportar todas las características necesarias de la nube.

---

## 2. ¿Por qué necesitamos ABAP Cloud?

### El problema del ABAP clásico

En el modelo clásico, los desarrolladores tenían acceso a **todo**: tablas del sistema, código estándar de SAP, transacciones internas... Esto generaba:

| Problema | Consecuencia |
|----------|--------------|
| Acceso directo a tablas estándar SAP | Actualizaciones del sistema pueden romper desarrollos propios |
| Uso de módulos de función obsoletos | Código difícil de mantener y migrar |
| Dependencias no controladas | Imposibilidad de garantizar estabilidad en upgrades |
| Sin separación clara de capas | Dificultad para exponer servicios de forma estándar |

### La solución: ABAP Cloud

ABAP Cloud proporciona un **ecosistema estable** para desarrollar aplicaciones empresariales complejas que involucran múltiples partes y diversas capas de extensiones.

### Beneficio clave para ti como desarrollador

> **Una vez que sabes desarrollar con ABAP Cloud, puedes aplicar ese conocimiento tanto para proyectos en nube pública como para proyectos on-premise.**

Las tecnologías, herramientas y conceptos detrás de ABAP Cloud son **casi todos aplicables para todas las opciones de despliegue**, lo que reduce significativamente la inversión de aprendizaje necesaria.

---

## 3. ABAP Clásico vs ABAP Cloud - Comparativa

### Comparativa General

| Aspecto | ABAP Clásico | ABAP Cloud |
|---------|--------------|------------|
| **Herramienta de desarrollo** | SE80, SE38, SE24 (SAP GUI) | ABAP Development Tools for Eclipse (ADT) |
| **Interfaz de usuario** | Dynpros, Selection Screens | SAP Fiori (OData + UI5) |
| **Modelo de datos** | Tablas transparentes, vistas SE11 | CDS Views (Core Data Services) |
| **Lógica de negocio** | Módulos de función, BAPIs, clases | RAP (RESTful Application Programming Model) |
| **Acceso a datos** | Open SQL directo a cualquier tabla | Solo APIs liberadas (Released APIs) |
| **Extensibilidad** | Modificaciones, User Exits, BADIs | Extensiones vía puntos definidos por SAP |

### Lo que cambia en tu día a día

| En ABAP Clásico hacías... | En ABAP Cloud harás... |
|---------------------------|------------------------|
| `SELECT * FROM MARA` | Usar CDS Views liberadas o crear las tuyas |
| Crear dynpros con Screen Painter | Definir UI con anotaciones en CDS + SAP Fiori Elements |
| Módulos de función RFC | Servicios OData con RAP |
| `CALL FUNCTION 'BAPI_...'` | Consumir APIs liberadas vía EML |
| Transaction codes (SE38, SM30...) | Apps Fiori en el Launchpad |

### ¿Qué permanece igual?

- El lenguaje ABAP en su esencia (variables, loops, estructuras, clases)
- La sintaxis básica de Open SQL (con restricciones)
- Los conceptos de programación orientada a objetos
- El debugging (aunque ahora en Eclipse)

---

## 4. Conceptos Clave de ABAP Cloud

### 4.1 ABAP Cloud Language Version

ABAP Cloud introduce el concepto de **versiones del lenguaje ABAP**. Esto define qué sentencias y objetos puedes usar.

```
┌─────────────────────────────────────────────────────────┐
│                    ABAP Language                        │
├─────────────────────────────────────────────────────────┤
│  ABAP Cloud         │  ABAP Standard (Clásico)         │
│  ─────────────      │  ────────────────────────        │
│  • Subconjunto      │  • Todo el lenguaje              │
│    optimizado       │  • Acceso a todo el sistema      │
│  • Solo APIs        │  • Sin restricciones             │
│    liberadas        │                                  │
└─────────────────────────────────────────────────────────┘
```

### 4.2 Released APIs (APIs Liberadas)

En ABAP Cloud, **solo puedes usar objetos que SAP ha liberado explícitamente**. Esto garantiza:

- ✅ **Estabilidad**: SAP garantiza que no cambiarán de forma incompatible
- ✅ **Upgrades seguros**: Tu código no se romperá con actualizaciones
- ✅ **Portabilidad**: Funciona igual en cloud y on-premise

### 4.3 Core Data Services (CDS)

CDS es la forma moderna de definir modelos de datos en ABAP Cloud. Reemplaza las vistas clásicas de SE11.

**Ejemplo conceptual:**

```
En ABAP Clásico:          En ABAP Cloud:
─────────────────         ─────────────────
Vista SE11                CDS View Entity
    ↓                         ↓
Dynpro/ALV               Anotaciones UI
    ↓                         ↓
Programa ABAP            SAP Fiori Elements
```

### 4.4 RAP - RESTful Application Programming Model

RAP es el modelo de programación para crear aplicaciones transaccionales en ABAP Cloud. Define cómo estructurar:

- El **modelo de datos** (con CDS)
- El **comportamiento** (Behavior Definition)
- La **lógica de negocio** (Behavior Implementation con ABAP)

---

## 5. Arquitectura de ABAP Cloud

### 5.1 Arquitectura General (Tres Capas)

La arquitectura de ABAP Cloud sigue un modelo de tres capas que separa claramente las responsabilidades:

```
┌─────────────────────────────────────────────────────────────────┐
│                           APP                                    │
│                    ┌─────────────────┐                          │
│                    │  SAP FIORI APPS │                          │
│                    │  ANALYTICAL APPS│                          │
│                    └─────────────────┘                          │
├─────────────────────────────────────────────────────────────────┤
│                  BUSINESS SERVICE EXPOSURE                       │
│    ┌────────────────────────┐    ┌────────────────────────┐     │
│    │      UI SERVICES       │    │  INTEGRATION SERVICES  │     │
│    │   (OData and InA)      │    │ (OData, HTTP, SOAP,    │     │
│    │                        │    │  RFC, SQL, Events)     │     │
│    └────────────────────────┘    └────────────────────────┘     │
├─────────────────────────────────────────────────────────────────┤
│               DOMAIN-SPECIFIC IMPLEMENTATION                     │
│    ┌────────────────────────────────────────────────────┐       │
│    │           DOMAIN-SPECIFIC MODELS                    │       │
│    │     (CDS entity, RAP Business Object,              │       │
│    │      CDS analytical provider)                       │       │
│    └────────────────────────────────────────────────────┘       │
│    ┌────────────────────────────────────────────────────┐       │
│    │           DOMAIN-SPECIFIC LOGIC                     │       │
│    │                 (ABAP, CDS)                         │       │
│    └────────────────────────────────────────────────────┘       │
├─────────────────────────────────────────────────────────────────┤
│                         DATABASE                                 │
│    ┌──────────────────┐    ┌─────────────────────────────┐      │
│    │     SAP HANA     │    │   BUSINESS SERVICE          │      │
│    │ (SQL, SQLScript) │    │   CONSUMPTION               │      │
│    └──────────────────┘    └─────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

**Fuente:** Diagrama basado en "Get Started with ABAP Cloud" - SAP Documentation

### 5.2 ¿Qué significa cada capa?

| Capa | Descripción | Equivalente en ABAP Clásico |
|------|-------------|----------------------------|
| **APP** | La aplicación visible para el usuario final | Transacción SAP GUI |
| **Business Service Exposure** | Cómo se expone el servicio (protocolo) | RFC, BAPI |
| **Domain-Specific Models** | Estructura de los datos | Tablas + Vistas SE11 |
| **Domain-Specific Logic** | Lógica de negocio | Código en includes, módulos de función |
| **Database** | Almacenamiento de datos | SAP HANA / Base de datos |

---

## 6. Escenarios de Desarrollo

ABAP Cloud soporta tres escenarios principales de desarrollo:

### 6.1 Transactional Apps (Aplicaciones Transaccionales)

**¿Para qué sirven?** Para crear aplicaciones que realizan operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre datos de negocio.

**Se implementan con:** ABAP RESTful Application Programming Model (RAP)

#### Arquitectura de Transactional Apps

```
┌─────────────────────────────────────────────────────────────────┐
│  APP                         SAP FIORI APPS                     │
├─────────────────────────────────────────────────────────────────┤
│  BUSINESS        ┌─────────────────┬─────────────────────┐      │
│  SERVICE         │   UI SERVICES   │ INTEGRATION SERVICES│      │
│  EXPOSURE        │   (OData)       │ (OData Web API,     │      │
│                  │                 │  business events)   │      │
│                  ├─────────────────┴─────────────────────┤      │
│                  │          SERVICE BINDING              │      │
│                  │  (Service Definition, Service         │      │
│                  │   Projection, Event Binding)          │      │
│                  └───────────────────────────────────────┘      │
├─────────────────────────────────────────────────────────────────┤
│  DOMAIN-SPECIFIC │       DOMAIN-SPECIFIC MODELS          │      │
│  IMPLEMENTATION  │   (CDS entity, RAP Business Object)   │      │
│                  ├───────────────────────────────────────┤      │
│                  │       DOMAIN-SPECIFIC LOGIC           │      │
│                  │           (ABAP, CDS)                 │      │
├─────────────────────────────────────────────────────────────────┤
│  DATABASE        │           SAP HANA                    │      │
│                  │       (SQL and SQLScript)             │      │
└─────────────────────────────────────────────────────────────────┘
```

**Fuente:** Diagrama de "Transactional Apps" - SAP Documentation

#### ¿Qué es un RAP Business Object?

Un Business Object (BO) representa un artefacto del mundo real como un **producto** o una **orden de venta**. Contiene:

- **Modelo de datos jerárquico**: Un nodo raíz y varios nodos hijos
- **Comportamiento**: Definido en un Behavior Definition
- **Implementación runtime**: Con ABAP y Entity Manipulation Language (EML) en un Behavior Pool

#### Cualidades de las Transactional Apps

Según la documentación de SAP, las aplicaciones transaccionales en ABAP Cloud tienen estas cualidades:

- Desarrollar apps **stateless** (sin estado)
- Usar **servicios OData** para interoperabilidad y escalabilidad
- Desarrollar UIs dirigidas por **metadatos con anotaciones UI** y SAP Fiori elements
- Crear servicios **optimizados para SAP HANA**
- Crear apps y servicios **lifecycle-stable** que pueden extenderse sin modificaciones
- **Localizar e internacionalizar** las apps

#### Patrones Comunes de Desarrollo

| Patrón | Descripción |
|--------|-------------|
| **List Report + Object Page** | El caso de uso principal: lista filtrable + página de detalle del objeto |
| **Draft** | Versión intermedia que no se ha guardado como versión activa |
| **Treeview** | Mostrar datos jerárquicos en la UI |
| **UI Reuse Services** | Integrar funcionalidad estándar como documentos de cambio o notas |

---

### 6.2 Analytical Apps (Aplicaciones Analíticas)

**¿Para qué sirven?** Para evaluar y analizar datos de negocio con modelos multidimensionales.

**Se implementan con:** ABAP Core Data Services (CDS)

#### Dos escenarios de Analytics

| Escenario | Descripción |
|-----------|-------------|
| **Embedded Analytics** | El motor analítico opera sobre los **mismos datos** que las apps transaccionales. Sin replicación a un data warehouse externo. |
| **Side-by-Side Analytics** | Los datos se **replican** desde el sistema ABAP a otros clientes analíticos como SAP Datasphere. |

#### Arquitectura de Analytical Apps

```
┌─────────────────────────────────────────────────────────────────┐
│  APP                      ANALYTICAL APPS                       │
├─────────────────────────────────────────────────────────────────┤
│  BUSINESS        ┌───────────────────────────────────────┐      │
│  SERVICE         │            UI SERVICES                │      │
│  EXPOSURE        │   UI services for analytical clients  │      │
│                  │              (InA)                    │      │
│                  ├───────────────────────────────────────┤      │
│                  │          SERVICE BINDING              │      │
│                  │  (Service Definition, Service         │      │
│                  │   Projection)                         │      │
│                  └───────────────────────────────────────┘      │
├─────────────────────────────────────────────────────────────────┤
│  DOMAIN-SPECIFIC │    DOMAIN-SPECIFIC DATA MODELING      │      │
│  IMPLEMENTATION  │     (CDS analytical provider)         │      │
│                  ├───────────────────────────────────────┤      │
│                  │       DOMAIN-SPECIFIC LOGIC           │      │
│                  │           (ABAP, CDS)                 │      │
├─────────────────────────────────────────────────────────────────┤
│  DATABASE        │           SAP HANA                    │      │
│                  │       (SQL and SQLScript)             │      │
└─────────────────────────────────────────────────────────────────┘

                    ¹ Information Access (InA)
                    ² Core Data Services
```

**Fuente:** Diagrama de "Analytical Apps" - SAP Documentation

#### Componentes del Modelo Multidimensional

El **Analytical Provider** está compuesto por:

```
                    ┌─────────────┐
                    │   QUERY     │  ← Define filtros, cálculos,
                    │ (Consulta)  │    layout inicial
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
        ┌───────────┤    CUBE     ├───────────┐
        │           │   (Cubo)    │           │
        │           └──────┬──────┘           │
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │DIMENSION│       │ DIMENSION │      │DIMENSION│
   │ (Región)│       │ (Tiempo)  │      │(Producto)│
   └────┬────┘       └─────┬─────┘      └────┬────┘
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │  TEXT   │       │ HIERARCHY │      │  TEXT   │
   │  VIEW   │       │   VIEW    │      │  VIEW   │
   └─────────┘       └───────────┘      └─────────┘
```

#### Cualidades de las Analytical Apps

- Definir modelos multidimensionales complejos nativamente con CDS
- **Reutilizar** objetos de desarrollo entre casos transaccionales y analíticos
- Crear servicios optimizados para SAP HANA
- Crear modelos multidimensionales **lifecycle-stable** extensibles sin modificaciones
- Desarrollar UIs SAP Fiori dirigidas por metadatos con anotaciones de analytics

---

### 6.3 Integration Services (Servicios de Integración)

**¿Para qué sirven?** Para exponer y consumir servicios que permiten la integración entre sistemas.

#### Dos tipos de integración

| Tipo | Descripción | Protocolos |
|------|-------------|------------|
| **Process Integration** | Comunicación a nivel de app, siguiendo un proceso de negocio predefinido (ej: order-to-cash). Bidireccional. | OData, SOAP, Business Events, RFC |
| **Data Integration** | Intercambio de datos sin relación con un proceso de negocio específico. Unidireccional. | SQL |

#### Comparativa Process vs Data Integration

| Dimensión | Process Integration | Data Integration |
|-----------|--------------------|--------------------|
| **Alcance** | Integra apps siguiendo un proceso de negocio | Integra partners sin relación a proceso específico |
| **Lógica de dominio** | Se considera para todas las operaciones | Se bypasea (solo READ se considera) |
| **Comunicación** | Bidireccional | Unidireccional |
| **Representación de datos** | Convertido a formato externo (ej: ISO Currencies) | Mantiene tipos fuente (ej: fechas ABAP) |

#### Protocolos disponibles para Process Integration

| Protocolo | Cuándo usar | Disponible Inbound | Disponible Outbound |
|-----------|-------------|-------------------|---------------------|
| **OData** | Integración síncrona con sistemas ABAP modernos | ✅ | ✅ |
| **SOAP** | Integración con APIs existentes | ❌ | ✅ |
| **RFC** | Integración con sistemas ABAP antiguos o alto rendimiento | ✅ | ✅ |
| **HTTP** | Flexibilidad total del protocolo HTTP | ✅ | ✅ |
| **Business Events** | Integración asíncrona, arquitecturas event-driven | ✅ | ✅ |
| **SQL** | Data federation y replicación | ✅ | ❌ |

**Fuente:** Tabla de "Integration Services" - SAP Documentation

#### Arquitectura de Integration Services

```
┌─────────────────────────────────────────────────────────────────┐
│  BUSINESS        │        INTEGRATION SERVICES           │      │
│  SERVICE         │  for process and data integration     │      │
│  EXPOSURE        ├───────────────────┬───────────────────┤      │
│                  │ OData, business   │   HTTP, SOAP,     │      │
│                  │ events, SQL       │   RFC             │      │
├─────────────────────────────────────────────────────────────────┤
│  DOMAIN-SPECIFIC │       DOMAIN-SPECIFIC MODELS          │      │
│  IMPLEMENTATION  │   (CDS entity, RAP Business Object)   │      │
│                  ├───────────────────────────────────────┤      │
│                  │       DOMAIN-SPECIFIC LOGIC           │      │
│                  │           (ABAP, CDS)                 │      │
├─────────────────────────────────────────────────────────────────┤
│  DATABASE        ┌──────────────┬────────────────────────┐      │
│                  │  SAP HANA    │  BUSINESS SERVICE      │      │
│                  │              │  CONSUMPTION           │      │
│                  │              │  (consume external     │      │
│                  │              │   services)            │      │
│                  └──────────────┴────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

**Fuente:** Diagrama de "Integration Services" - SAP Documentation

---

## 7. ¿Por dónde empezar?

### Según tu perfil (de la documentación SAP):

| Si eres... | Empieza por... |
|------------|----------------|
| **Principiante en ABAP y ABAP Cloud** | La sección "Get Started" para lecturas recomendadas y recursos de onboarding |
| **Experto en ABAP Cloud** | La sección "News" para conocer las últimas características |
| **Desarrollador ABAP Clásico** | La sección "Get Started" para obtener una visión general de ABAP Cloud |

### Recursos recomendados por SAP

#### Para aprender ABAP desde cero:
- **Learning Journey:** "Learning the Basics of ABAP Programming on SAP BTP"

#### Para aprender CDS:
- Capítulo de introducción a ABAP Core Data Services en el ABAP Data Models guide
- Tutorial: "SAP BTP ABAP Environment: Create and Expose a CDS-Based Data Model"

#### Para conocer las herramientas:
- **Basic Tutorial** de ABAP Development Tools for Eclipse

#### Tutoriales prácticos para Transactional Apps:

| Tutorial | Descripción |
|----------|-------------|
| Create Database Table and Generate UI Service | Crear tabla y generar servicio UI |
| Enhance the Business Object Behavior With Determinations | Añadir determinaciones |
| Enhance the Business Object Behavior With Validations | Añadir validaciones |
| Enhance the Business Object Behavior With Instance Action | Añadir acciones de instancia |
| Write an ABAP Unit Test for the RAP Business Object | Escribir tests unitarios |

**Fuente:** Lista de tutoriales de "Find Available Tutorials" - SAP Documentation

> 🔎 **¿Dónde encontrar todos los tutoriales?**
> 
> Puedes explorar y buscar todos los tutoriales disponibles de SAP en el **SAP Tutorial Navigator**:
> 
> 👉 [https://developers.sap.com/tutorial-navigator.html](https://developers.sap.com/tutorial-navigator.html)
> 
> Allí puedes filtrar por tema (ABAP, RAP, Fiori, BTP), nivel de experiencia y tipo de contenido.

### Estructura de la documentación ABAP Cloud

```
                    ┌─────────────────────────────────────┐
                    │        ABAP Cloud Guide             │
                    └─────────────────────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
┌───────────────┐          ┌───────────────┐          ┌───────────────┐
│  SAP Fiori    │          │     RAP       │          │    ABAP       │
│     App       │          │    Guide      │          │  Analytics    │
│ Development   │          │               │          │    Guide      │
└───────────────┘          └───────────────┘          └───────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
┌───────────────┐          ┌───────────────┐          ┌───────────────┐
│    ABAP       │          │  ABAP Data    │          │    ABAP       │
│  Concepts     │          │   Models      │          │   Keyword     │
│    Guide      │          │    Guide      │          │Documentation  │
└───────────────┘          └───────────────┘          └───────────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    ▼                               ▼
            ┌───────────────┐              ┌───────────────┐
            │  SAP HANA     │              │    ABAP       │
            │  SQLScript    │              │ Integration & │
            │  Reference    │              │ Connectivity  │
            └───────────────┘              └───────────────┘
```

**Fuente:** Diagrama de "Documentation Overview" - SAP Documentation

---

## 📌 Resumen Final

| Concepto | Qué debes recordar |
|----------|-------------------|
| **ABAP Cloud** | Modelo de desarrollo para apps cloud-ready, aplicable en nube y on-premise |
| **Released APIs** | Solo puedes usar objetos liberados por SAP = código estable y portable |
| **CDS** | La forma moderna de definir modelos de datos (reemplaza vistas SE11) |
| **RAP** | El modelo para crear apps transaccionales (reemplaza dynpros + módulos de función) |
| **Transactional Apps** | Apps CRUD con RAP, expuestas via OData, UI con SAP Fiori Elements |
| **Analytical Apps** | Modelos multidimensionales con CDS, expuestos via InA |
| **Integration Services** | Servicios para integrar sistemas (OData, SOAP, RFC, Events, SQL) |
| **ADT** | Tu nueva herramienta de desarrollo (Eclipse, no SE80) |

---

## 🔗 Referencias

Toda la información de este documento proviene de la documentación oficial de SAP:

- ABAP Cloud Landing Page
- Transactional Apps
- Analytical Apps  
- Integration Services
- Get Started
- Get Started with ABAP Cloud
- Documentation Overview
- Find Available Tutorials

---

> **Siguiente paso sugerido:** Instala ABAP Development Tools for Eclipse y sigue el tutorial "Create Database Table and Generate UI Service" para crear tu primera app RAP.

---

*Documento creado para estudiantes de ABAP en transición del modelo clásico a ABAP Cloud.*
