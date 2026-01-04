# Quiz ABAP - Fundamentos de Programación
## Evaluación de Conceptos Básicos - 30 Preguntas

> **Curso**: S4D100 / S4D400 - Fundamentos de Programación ABAP  
> **Nivel**: Básico  
> **Duración estimada**: 45-60 minutos  
> **Instrucciones**: Seleccione la(s) respuesta(s) correcta(s). Algunas preguntas tienen respuesta única, otras tienen respuestas múltiples (se indica en cada pregunta).

---

## 📚 SECCIÓN 1: DICCIONARIO DE DATOS ABAP

### **Pregunta 1: Propósito del ABAP Dictionary**

¿Cuál es la función principal del Diccionario de Datos ABAP (transacción SE11)?

**A)** Almacenar los datos maestros y transaccionales del sistema SAP  
**B)** Administrar definiciones de metadatos y asegurar consistencia de tipos de datos en el sistema  
**C)** Ejecutar programas ABAP y mostrar resultados en consola  
**D)** Compilar y depurar código ABAP en tiempo de ejecución  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
El ABAP Dictionary (SE11) es un repositorio central de metadatos que define objetos como tablas, dominios, elementos de datos, estructuras y tipos tabla. NO almacena datos reales, solo define cómo se estructuran.

</details>

---

### **Pregunta 2: Características del Dominio**

¿Cuáles de las siguientes características se definen en un DOMINIO? (Seleccione 2 respuestas)

**A)** Etiquetas de campo (Short, Medium, Long)  
**B)** Tipo de dato y longitud del campo  
**C)** Rango de valores permitidos (value range)  
**D)** Texto de ayuda F1 (Field Help)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** B, C

**Explicación:**  
El dominio define características TÉCNICAS: tipo de dato, longitud, rango de valores y valores fijos opcionales. Las etiquetas y ayuda F1 son características SEMÁNTICAS del elemento de datos.

</details>

---

### **Pregunta 3: Elemento de Datos**

¿Cuál es la relación correcta entre un Elemento de Datos y un Dominio?

**A)** Un elemento de datos puede referenciar múltiples dominios simultáneamente  
**B)** Un elemento de datos referencia exactamente un dominio y agrega información semántica  
**C)** Un dominio debe referenciar un elemento de datos para ser válido  
**D)** Elemento de datos y dominio son sinónimos en ABAP  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Un elemento de datos referencia UN dominio (para características técnicas) y agrega información semántica como etiquetas, ayuda F1 y search help. Múltiples elementos de datos pueden referenciar el mismo dominio.

</details>

---

### **Pregunta 4: Estructura en el ABAP Dictionary**

¿Cuál de las siguientes afirmaciones sobre ESTRUCTURAS en SE11 es CORRECTA?

**A)** Una estructura almacena múltiples registros de datos en la base de datos  
**B)** Una estructura define un tipo compuesto por múltiples componentes, pero no almacena datos  
**C)** Las estructuras solo pueden tener componentes de tipo elemental (no pueden incluir otras estructuras)  
**D)** Una estructura es lo mismo que una tabla de base de datos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Una estructura del diccionario define un tipo de dato compuesto (múltiples campos) pero NO almacena datos. Puede incluir elementos de datos, tipos predefinidos u otras estructuras (INCLUDE). Solo define la forma/molde.

</details>

---

### **Pregunta 5: Tipo Tabla en SE11**

¿Cuáles de las siguientes propiedades se definen en un TIPO TABLA del ABAP Dictionary? (Seleccione 3 respuestas)

**A)** Tipo de línea (estructura, tipo elemental, etc.)  
**B)** Conexión a servidor de base de datos externo  
**C)** Tipo de tabla (STANDARD, SORTED, HASHED)  
**D)** Definición de clave (campos y UNIQUE/NON-UNIQUE)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, C, D

**Explicación:**  
Un tipo tabla en SE11 define: (1) tipo de línea, (2) tipo de tabla (STANDARD/SORTED/HASHED), (3) definición de clave. NO define conexiones a servidores externos.

</details>

---

### **Pregunta 6: Diferencia Estructura vs Tipo Tabla**

En el contexto del ABAP Dictionary, ¿cuál es la principal diferencia entre una ESTRUCTURA y un TIPO TABLA?

**A)** Una estructura representa UN registro, un tipo tabla representa una colección de registros  
**B)** Las estructuras solo existen en SE11, los tipos tabla solo en código ABAP  
**C)** Una estructura puede tener máximo 10 campos, un tipo tabla no tiene límite  
**D)** No hay diferencia, son sinónimos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
Estructura = define UN registro con múltiples campos. Tipo tabla = define una tabla interna (colección de múltiples registros). Ambos se definen en SE11.

</details>

---

### **Pregunta 7: Reutilización de Dominios**

¿Por qué es una buena práctica reutilizar dominios en múltiples elementos de datos?

**A)** Porque mejora el rendimiento de ejecución del programa  
**B)** Porque asegura consistencia técnica y facilita mantenimiento centralizado  
**C)** Porque es obligatorio según las reglas de sintaxis ABAP  
**D)** Porque reduce el consumo de memoria en el sistema  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Reutilizar dominios asegura consistencia (todos los campos que usan el dominio tienen las mismas características técnicas) y facilita mantenimiento (cambiar el dominio afecta todos los elementos de datos que lo usan).

</details>

---

### **Pregunta 8: Objetos del ABAP Dictionary**

¿Cuáles de los siguientes son objetos que se pueden crear en el ABAP Dictionary (SE11)? (Seleccione 3 respuestas)

**A)** Database Table (Tabla de base de datos)  
**B)** ABAP Class (Clase ABAP)  
**C)** Data Element (Elemento de datos)  
**D)** Domain (Dominio)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, C, D

**Explicación:**  
En SE11 se crean: tablas, vistas, dominios, elementos de datos, estructuras, tipos tabla, search helps. Las clases ABAP se crean en SE24/Eclipse, NO en SE11.

</details>

---

## 💾 SECCIÓN 2: TIPOS DE DATOS ABAP

### **Pregunta 9: Tipos de Datos Completos**

¿Cuáles de los siguientes son tipos de datos COMPLETOS en ABAP? (Seleccione 3 respuestas)

**A)** `i` (integer)  
**B)** `c` (character sin longitud)  
**C)** `string` (cadena de texto)  
**D)** `p` (packed sin especificaciones)  
**E)** `d` (date)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, C, E

**Explicación:**  
Tipos COMPLETOS tienen longitud definida: `i` (4 bytes), `string` (dinámica), `d` (8 dígitos). Tipos INCOMPLETOS requieren LENGTH: `c`, `n`, `p` sin especificaciones.

</details>

---

### **Pregunta 10: Declaración con Tipos Incompletos**

¿Cuál de las siguientes declaraciones es CORRECTA en ABAP?

**A)** `DATA lv_name TYPE c.`  
**B)** `DATA lv_name TYPE c LENGTH 50.`  
**C)** `DATA lv_age TYPE i LENGTH 4.`  
**D)** `DATA lv_price TYPE p.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
`c` es tipo incompleto y requiere LENGTH. `i` es completo (no necesita LENGTH). `p` requiere LENGTH y DECIMALS. Correcto: `TYPE c LENGTH 50` o `TYPE p LENGTH 8 DECIMALS 2`.

</details>

---

### **Pregunta 11: Tipo String vs Tipo C**

¿Cuál es la principal diferencia entre `TYPE string` y `TYPE c LENGTH 255`?

**A)** `string` tiene longitud variable dinámica, `c` tiene longitud fija  
**B)** `string` solo almacena números, `c` almacena cualquier carácter  
**C)** `string` es más rápido en procesamiento que `c`  
**D)** No hay diferencia, son equivalentes  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
`string` tiene longitud variable y se ajusta dinámicamente. `c LENGTH n` tiene longitud fija predefinida. Ambos almacenan caracteres, pero `string` es más flexible para textos de longitud desconocida.

</details>

---

### **Pregunta 12: Tipo de Dato para Fechas**

¿Qué tipo de dato debe usar para almacenar una fecha en formato YYYYMMDD?

**A)** `TYPE c LENGTH 8`  
**B)** `TYPE d`  
**C)** `TYPE i`  
**D)** `TYPE string`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
`TYPE d` es el tipo específico para fechas en ABAP (8 dígitos YYYYMMDD). Aunque `c LENGTH 8` funciona técnicamente, `d` permite operaciones de fecha (cálculos, validaciones).

</details>

---

### **Pregunta 13: Tipo Packed (P)**

¿Cuál es la declaración CORRECTA de una variable para almacenar importes monetarios con 2 decimales?

**A)** `DATA lv_amount TYPE p.`  
**B)** `DATA lv_amount TYPE p LENGTH 2.`  
**C)** `DATA lv_amount TYPE p LENGTH 15 DECIMALS 2.`  
**D)** `DATA lv_amount TYPE i DECIMALS 2.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
Tipo `p` (packed) requiere LENGTH (total de dígitos) y DECIMALS. Para importes: `TYPE p LENGTH 15 DECIMALS 2` es común. El tipo `i` no acepta decimales.

</details>

---

### **Pregunta 14: Elemento de Datos como Tipo**

¿Cuáles son ventajas de usar elementos de datos en lugar de tipos predefinidos? (Seleccione 2 respuestas)

**A)** Mayor velocidad de ejecución del programa  
**B)** Consistencia en todo el sistema (mismo significado, mismas características)  
**C)** Información semántica disponible (etiquetas, ayuda F1)  
**D)** Menor consumo de memoria  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** B, C

**Explicación:**  
Usar elementos de datos asegura consistencia (todos usan la misma definición) y provee información semántica (etiquetas, textos). No afecta rendimiento o memoria significativamente.

</details>

---

## 🎯 SECCIÓN 3: CLASES EN ABAP

### **Pregunta 15: Clases Globales**

¿Dónde se crean y almacenan las clases GLOBALES en ABAP?

**A)** Dentro del código fuente de un programa report  
**B)** En el ABAP Dictionary (SE11)  
**C)** En el repositorio como objetos independientes (SE24 o Eclipse)  
**D)** En archivos del sistema operativo  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
Clases globales se crean en SE24 (SAP GUI) o Eclipse ADT y se almacenan en el repositorio como objetos independientes (ZCL_*, YCL_*). Son reutilizables en todo el sistema.

</details>

---

### **Pregunta 16: Clases Locales**

¿Cuáles de las siguientes afirmaciones sobre clases LOCALES son CORRECTAS? (Seleccione 2 respuestas)

**A)** Se definen en el tab "Local Types" de un programa  
**B)** Son visibles y reutilizables en todo el sistema  
**C)** Solo son visibles dentro del programa donde se definen  
**D)** Se crean con la transacción SE24  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, C

**Explicación:**  
Clases locales se definen en "Local Types" de un programa/clase y solo son visibles dentro de ese contexto. NO están en SE24 ni son reutilizables fuera del programa.

</details>

---

### **Pregunta 17: Nomenclatura de Clases Globales**

¿Con qué prefijos deben comenzar los nombres de clases globales creadas por clientes?

**A)** `CL_` o `LCL_`  
**B)** `ZCL_` o `YCL_`  
**C)** `/DMO/CL_` o `SAP_`  
**D)** No hay restricción de prefijos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Objetos de cliente deben iniciar con Z o Y. Clases globales: `ZCL_*` o `YCL_*`. `CL_` es para SAP, `LCL_` para clases locales, `/DMO/` es namespace SAP demo.

</details>

---

### **Pregunta 18: Interface IF_OO_ADT_CLASSRUN**

¿Para qué se usa la interface `IF_OO_ADT_CLASSRUN` en una clase ABAP?

**A)** Para conectar la clase a una base de datos externa  
**B)** Para permitir que la clase sea ejecutable como programa principal (F9)  
**C)** Para definir métodos privados en la clase  
**D)** Para crear tablas internas dentro de la clase  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
`IF_OO_ADT_CLASSRUN` permite ejecutar una clase directamente en Eclipse (F9). Obliga a implementar el método `main` que sirve como punto de entrada del programa.

</details>

---

### **Pregunta 19: Visibilidad en Clases**

¿Cuáles son las tres secciones de visibilidad en una clase ABAP global? (Seleccione 3 respuestas)

**A)** PUBLIC  
**B)** PRIVATE  
**C)** PROTECTED  
**D)** INTERNAL  
**E)** GLOBAL  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, B, C

**Explicación:**  
Las tres secciones de visibilidad son: PUBLIC (visible en todas partes), PROTECTED (visible en subclases), PRIVATE (solo dentro de la clase). INTERNAL y GLOBAL no existen.

</details>

---

### **Pregunta 20: Cuándo Usar Clase Local vs Global**

¿Cuándo es apropiado usar una clase LOCAL en lugar de una GLOBAL?

**A)** Cuando la lógica solo se necesita en un programa específico  
**B)** Cuando se requiere máximo rendimiento  
**C)** Cuando se necesita reutilizar la clase en múltiples programas  
**D)** Cuando la clase debe ser transportada a otros sistemas  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
Clase local: lógica específica de un programa, no reutilizable. Clase global: lógica reutilizable, transportable, visible en todo el sistema. Rendimiento es similar.

</details>

---

## 📄 SECCIÓN 4: PROGRAMAS E INCLUDES

### **Pregunta 21: Programa Ejecutable (Report)**

¿Cuáles de las siguientes características son propias de un Programa Ejecutable? (Seleccione 2 respuestas)

**A)** Comienza con la palabra clave `REPORT`  
**B)** Puede ejecutarse directamente con F8 o transacción SA38  
**C)** No puede contener clases locales  
**D)** Debe tener obligatoriamente parámetros de selección  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, B

**Explicación:**  
Programa ejecutable (Report): inicia con `REPORT nombre`, ejecutable con F8/SA38, puede tener clases locales y parámetros son opcionales.

</details>

---

### **Pregunta 22: Propósito de los Includes**

¿Cuál es la función principal de un programa INCLUDE?

**A)** Ser ejecutado independientemente como programa principal  
**B)** Modularizar y reutilizar código que se inserta en otros programas  
**C)** Almacenar datos de configuración del sistema  
**D)** Compilar código ABAP más rápidamente  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Include modulariza código reutilizable (declaraciones, implementaciones) que se inserta en programas con `INCLUDE nombre`. NO es ejecutable por sí solo.

</details>

---

### **Pregunta 23: Sintaxis INCLUDE**

¿Cuál es la sintaxis CORRECTA para incluir un programa include en otro programa?

**A)** `CALL INCLUDE z_my_include.`  
**B)** `INCLUDE z_my_include.`  
**C)** `INSERT z_my_include.`  
**D)** `IMPORT z_my_include.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
La sintaxis correcta es `INCLUDE nombre_include.` (con punto final). El código del include se inserta en ese punto del programa.

</details>

---

### **Pregunta 24: Tipos de Programas ABAP**

¿Cuál de los siguientes NO es un tipo válido de programa ABAP?

**A)** Executable Program (Report - Type 1)  
**B)** Module Pool (Type M)  
**C)** Include Program (Type I)  
**D)** Database Program (Type D)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** D

**Explicación:**  
Tipos válidos: Executable (1), Module Pool (M), Include (I), Function Group (F), Subroutine Pool (S), Interface Pool (J), Class Pool (K). "Database Program" no existe.

</details>

---

## 🔧 SECCIÓN 5: CONCEPTOS BÁSICOS DE PROGRAMACIÓN

### **Pregunta 25: Declaración de Variables**

¿Cuál es la forma CORRECTA de declarar una variable local en ABAP según las convenciones de nomenclatura?

**A)** `DATA carrier_id TYPE /dmo/carrier_id.`  
**B)** `DATA lv_carrier_id TYPE /dmo/carrier_id.`  
**C)** `DATA gv_carrier_id TYPE /dmo/carrier_id.`  
**D)** `DEFINE carrier_id TYPE /dmo/carrier_id.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Convención: variables locales con prefijo `lv_` (local variable). `gv_` es para globales. La palabra clave es `DATA`, no `DEFINE`.

</details>

---

### **Pregunta 26: Tablas Internas**

¿Cuál es la diferencia entre `STANDARD TABLE`, `SORTED TABLE` y `HASHED TABLE`?

**A)** El tipo de datos que pueden almacenar  
**B)** La forma de acceso y si permiten duplicados  
**C)** El tamaño máximo de registros  
**D)** No hay diferencia, son sinónimos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
STANDARD: acceso por índice, permite duplicados. SORTED: ordenada por clave, acceso binario. HASHED: acceso por hash (rápido), clave única. Difieren en forma de acceso y manejo de duplicados.

</details>

---

### **Pregunta 27: Estructura de Control IF**

¿Cuál de las siguientes es la sintaxis CORRECTA de una sentencia IF en ABAP?

**A)** `IF lv_age > 18 { ... }`  
**B)** `IF lv_age > 18 THEN ... ENDIF`  
**C)** `IF ( lv_age > 18 ) ... END IF`  
**D)** `IF lv_age > 18. ... ENDIF.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** D

**Explicación:**  
Sintaxis ABAP: `IF condición. ... ENDIF.` (con puntos). No usa llaves `{}`, ni THEN, ni paréntesis en la condición, ni espacio en ENDIF.

</details>

---

### **Pregunta 28: LOOP AT Tabla Interna**

¿Cuál es la forma CORRECTA de recorrer una tabla interna en ABAP?

**A)** `FOR EACH ls_flight IN lt_flights ... ENDFOR`  
**B)** `LOOP AT lt_flights INTO ls_flight. ... ENDLOOP.`  
**C)** `WHILE lt_flights INTO ls_flight ... ENDWHILE`  
**D)** `ITERATE lt_flights INTO ls_flight. ... ENDITERATE.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Sintaxis correcta: `LOOP AT tabla INTO estructura. ... ENDLOOP.` También existe `LOOP AT tabla ASSIGNING <field_symbol>` y `LOOP AT tabla REFERENCE INTO`.

</details>

---

### **Pregunta 29: Sistema de Ayuda en Eclipse**

¿Qué atajo de teclado muestra la ayuda F1 (documentación) de un elemento en Eclipse ADT?

**A)** F1  
**B)** Ctrl + Espacio  
**C)** F2  
**D)** Ctrl + Shift + A  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
F1 = Ayuda/documentación. F2 = Navegar a definición. Ctrl+Espacio = Code completion. F3 = Abrir objeto. F8 = Ejecutar.

</details>

---

### **Pregunta 30: Debugging en ABAP**

¿Cuál es la forma de iniciar el debugger en Eclipse para una clase ABAP?

**A)** F5  
**B)** F7  
**C)** F8 (Run) con breakpoints establecidos, o clic derecho → Debug As  
**D)** Ctrl + D  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
Debug: establecer breakpoints (doble clic en margen) y ejecutar con F8, o clic derecho → "Debug As → ABAP Application". F9 ejecuta sin debug, F5/F7 son para navegación dentro del debugger.

</details>

---

## 📊 Resumen de Evaluación

### Distribución de Preguntas por Tema:

| Tema | Cantidad | Preguntas |
|------|----------|-----------|
| **Diccionario de Datos** | 8 | 1-8 |
| **Tipos de Datos ABAP** | 6 | 9-14 |
| **Clases (Global/Local)** | 6 | 15-20 |
| **Programas e Includes** | 4 | 21-24 |
| **Conceptos Básicos** | 6 | 25-30 |
| **TOTAL** | **30** | |

---

## 🎯 Criterios de Evaluación

| Puntaje | Nivel | Descripción |
|---------|-------|-------------|
| **27-30** | ⭐⭐⭐ Excelente | Dominio sólido de fundamentos ABAP |
| **23-26** | ⭐⭐ Bueno | Conocimiento adecuado, revisar algunos temas |
| **18-22** | ⭐ Aceptable | Conocimiento básico, requiere refuerzo |
| **< 18** | ⚠️ Insuficiente | Revisar material del curso nuevamente |

---

## 📚 Recursos Adicionales

Si necesitas repasar algún tema:

- **Diccionario de Datos:** Transacción SE11, revisar objetos /DMO/*
- **Tipos de Datos:** Documentación SAP sobre tipos built-in
- **Clases:** Crear clases de prueba en Eclipse con IF_OO_ADT_CLASSRUN
- **Programas:** Practicar creación de reports simples
- **Debugging:** Tutorial de ABAP Debugger en Eclipse

---

**Versión:** 1.0  
**Fecha:** Diciembre 2024  
**Basado en:** Cursos S4D100 y S4D400 - SAP Learning  
**Formato:** Markdown con respuestas colapsables para autoevaluación  

¡Buena suerte! 🚀
