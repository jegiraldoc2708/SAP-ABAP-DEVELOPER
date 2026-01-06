# Quiz ABAP - Fundamentos de Programación
## Evaluación de Conceptos Básicos - 51 Preguntas

> **Curso**: S4D100 / S4D400 - Fundamentos de Programación ABAP  
> **Nivel**: Básico-Intermedio  
> **Duración estimada**: 75-90 minutos  
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

### **Pregunta 25: ¿Qué es una Variable en ABAP?**

¿Cuál de las siguientes definiciones describe MEJOR qué es una variable en ABAP?

**A)** Una constante que no puede cambiar su valor durante la ejecución  
**B)** Un espacio de memoria con nombre que almacena un valor y puede cambiar durante la ejecución  
**C)** Una función que retorna valores calculados  
**D)** Una tabla de base de datos temporal  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Una variable es un espacio de memoria identificado con un nombre que puede almacenar un valor de un tipo específico. El valor puede cambiar durante la ejecución del programa. Se declara con `DATA nombre TYPE tipo`.

</details>

---

### **Pregunta 26: Declaración de Variables**

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

### **Pregunta 27: Tablas Internas**

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

### **Pregunta 28: Estructura de Control IF**

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

### **Pregunta 29: LOOP AT Tabla Interna**

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

### **Pregunta 30: Sistema de Ayuda en Eclipse**

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

### **Pregunta 31: Debugging en ABAP**

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

## 🗄️ SECCIÓN 6: SELECT Y BASE DE DATOS

### **Pregunta 32: Sintaxis Básica SELECT**

¿Cuál es la sintaxis CORRECTA de un SELECT básico en ABAP moderno?

**A)** `SELECT * FROM /dmo/connection INTO TABLE lt_connections.`  
**B)** `SELECT * FROM /dmo/connection INTO TABLE @lt_connections.`  
**C)** `SELECT ALL FROM /dmo/connection TO lt_connections.`  
**D)** `GET * FROM /dmo/connection INTO @lt_connections.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
En ABAP moderno (desde 7.40), las variables en SELECT deben estar precedidas por `@` (host variables). Sintaxis: `SELECT ... FROM tabla INTO TABLE @variable.`

</details>

---

### **Pregunta 33: SELECT SINGLE**

¿Cuál es la diferencia entre `SELECT SINGLE` y `SELECT` normal?

**A)** SELECT SINGLE lee máximo un registro, SELECT lee todos los registros  
**B)** SELECT SINGLE es más lento que SELECT normal  
**C)** SELECT SINGLE solo funciona con tablas pequeñas  
**D)** No hay diferencia, son sinónimos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
`SELECT SINGLE` lee como máximo UN registro (INTO estructura), aunque la condición coincida con múltiples. `SELECT` lee todos los registros que cumplan la condición (INTO TABLE).

</details>

---

### **Pregunta 34: Cláusula WHERE**

¿Cuáles operadores son válidos en la cláusula WHERE de un SELECT? (Seleccione 3 respuestas)

**A)** `=` (igual)  
**B)** `<>` o `!=` (diferente)  
**C)** `IN` (pertenece a una lista)  
**D)** `CONTAINS` (contiene substring)  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, B, C

**Explicación:**  
Operadores válidos en WHERE: `=`, `<>`, `<`, `>`, `<=`, `>=`, `IN`, `BETWEEN`, `LIKE`, `IS NULL`. `CONTAINS` NO es válido en SELECT (se usa en búsqueda full-text).

</details>

---

### **Pregunta 35: SELECT con Campos Específicos**

¿Cuál es la ventaja de seleccionar solo los campos necesarios en lugar de usar `SELECT *`?

**A)** El código es más largo y detallado  
**B)** Mejor rendimiento (menos datos transferidos) y claridad del código  
**C)** Es obligatorio según las reglas de sintaxis ABAP  
**D)** No hay ninguna ventaja  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Seleccionar campos específicos (`SELECT campo1, campo2`) reduce transferencia de datos, mejora rendimiento y hace el código más claro. `SELECT *` trae todos los campos (puede ser innecesario).

</details>

---

### **Pregunta 36: INTO TABLE vs INTO**

¿Cuál es la diferencia entre `INTO TABLE` e `INTO` en un SELECT?

**A)** INTO TABLE guarda en tabla interna, INTO guarda en estructura (un solo registro)  
**B)** INTO TABLE es más rápido que INTO  
**C)** INTO solo funciona con SELECT SINGLE  
**D)** Son equivalentes y se pueden intercambiar  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
`INTO TABLE @lt_tabla` guarda múltiples registros en tabla interna. `INTO @ls_estructura` guarda UN registro en estructura (debe usarse con SELECT SINGLE o dentro de LOOP).

</details>

---

### **Pregunta 37: Validación de SELECT**

¿Cómo verificar si un SELECT encontró datos?

**A)** Revisar `sy-subrc = 0` después del SELECT  
**B)** Usar `IS NOT INITIAL` en la tabla/estructura resultante  
**C)** Revisar `lines( tabla ) > 0`  
**D)** Todas las anteriores son válidas  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** D

**Explicación:**  
Métodos válidos: (1) `sy-subrc = 0` indica éxito, (2) `lt_tabla IS NOT INITIAL` verifica si hay datos, (3) `lines( lt_tabla ) > 0` cuenta registros. Todas son correctas.

</details>

---

### **Pregunta 38: ORDER BY**

¿Cuál es la sintaxis CORRECTA de ORDER BY en un SELECT?

**A)** `SELECT ... FROM tabla ORDER BY campo1 ASCENDING.`  
**B)** `SELECT ... FROM tabla ORDER BY campo1, campo2 DESCENDING.`  
**C)** `SELECT ... FROM tabla ORDER BY campo1, campo2 DESC.`  
**D)** `SELECT ... FROM tabla SORT BY campo1.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
Sintaxis: `ORDER BY campo1 [ASC|DESC], campo2 [ASC|DESC]`. `DESC` = descendente, `ASC` = ascendente (default). No se usa punto final, ni ASCENDING/DESCENDING completos, ni SORT BY.

</details>

---

### **Pregunta 39: INNER JOIN**

¿Qué hace un INNER JOIN entre dos tablas?

**A)** Devuelve todos los registros de ambas tablas  
**B)** Devuelve solo los registros que tienen coincidencia en AMBAS tablas  
**C)** Devuelve los registros de la primera tabla más los de la segunda sin duplicar  
**D)** Elimina registros duplicados de una tabla  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
INNER JOIN devuelve solo registros donde hay coincidencia en AMBAS tablas según la condición ON. Registros sin coincidencia se excluyen.

</details>

---

### **Pregunta 40: Sintaxis INNER JOIN**

¿Cuál es la estructura CORRECTA de un SELECT con INNER JOIN?

**A)** `SELECT FROM tabla1 JOIN tabla2 ON tabla1~campo = tabla2~campo`  
**B)** `SELECT FROM tabla1 INNER JOIN tabla2 ON tabla1.campo = tabla2.campo`  
**C)** `SELECT FROM tabla1 AS t1 INNER JOIN tabla2 AS t2 ON t1~campo = t2~campo`  
**D)** `SELECT FROM tabla1, tabla2 WHERE tabla1~campo = tabla2~campo`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
Sintaxis moderna: `SELECT FROM tabla1 AS alias1 INNER JOIN tabla2 AS alias2 ON alias1~campo = alias2~campo`. Usa alias y tilde `~` para separar tabla de campo.

</details>

---

### **Pregunta 41: LEFT OUTER JOIN**

¿Cuál es la diferencia entre INNER JOIN y LEFT OUTER JOIN?

**A)** No hay diferencia, son sinónimos  
**B)** LEFT OUTER JOIN incluye todos los registros de la tabla izquierda, aunque no tengan coincidencia  
**C)** INNER JOIN es más rápido que LEFT OUTER JOIN  
**D)** LEFT OUTER JOIN solo funciona con dos tablas  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
LEFT OUTER JOIN devuelve TODOS los registros de la tabla izquierda, más los coincidentes de la derecha (campos sin coincidencia = NULL/inicial). INNER JOIN solo devuelve coincidencias.

</details>

---

### **Pregunta 42: Operador IN en WHERE**

¿Cuál es la sintaxis CORRECTA para usar el operador IN en un SELECT?

**A)** `WHERE carrier_id IN ('AA', 'UA', 'DL')`  
**B)** `WHERE carrier_id IN @lt_carriers`  
**C)** `WHERE carrier_id = 'AA' OR 'UA' OR 'DL'`  
**D)** Opciones A y B son correctas  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** D

**Explicación:**  
IN acepta: (1) Lista literal `IN ('AA', 'UA')`, (2) Tabla interna `IN @lt_tabla`. Opción C es incorrecta (sintaxis inválida de OR).

</details>

---

### **Pregunta 43: DISTINCT**

¿Para qué se usa la palabra clave DISTINCT en un SELECT?

**A)** Para ordenar los resultados alfabéticamente  
**B)** Para eliminar registros duplicados del resultado  
**C)** Para contar el número de registros  
**D)** Para seleccionar solo el primer registro  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
`SELECT DISTINCT` elimina duplicados del resultado (solo devuelve registros únicos). Ejemplo: `SELECT DISTINCT carrier_id FROM /dmo/connection`.

</details>

---

### **Pregunta 44: Funciones de Agregación**

¿Cuáles de las siguientes son funciones de agregación válidas en SELECT? (Seleccione 3 respuestas)

**A)** `COUNT(*)`  
**B)** `SUM(campo)`  
**C)** `AVG(campo)`  
**D)** `CONCAT(campo1, campo2)`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuestas correctas:** A, B, C

**Explicación:**  
Funciones de agregación válidas: `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`. `CONCAT` es una función de cadena, no de agregación.

</details>

---

### **Pregunta 45: GROUP BY**

¿Cuándo es OBLIGATORIO usar GROUP BY en un SELECT?

**A)** Siempre que se use ORDER BY  
**B)** Cuando se mezclan funciones de agregación con campos normales en el SELECT  
**C)** Solo cuando se usa INNER JOIN  
**D)** Nunca es obligatorio, es opcional  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
GROUP BY es obligatorio cuando se mezclan funciones de agregación (`COUNT`, `SUM`, etc.) con campos normales. Los campos normales deben estar en GROUP BY.

</details>

---

### **Pregunta 46: CDS View**

¿Qué es una CDS View (Core Data Services View)?

**A)** Un programa ABAP ejecutable  
**B)** Una vista definida en el ABAP Dictionary con lógica SQL avanzada  
**C)** Una clase ABAP para acceso a datos  
**D)** Un tipo especial de tabla de base de datos  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
CDS View es una vista definida en lenguaje DDL (Data Definition Language) que permite lógica SQL avanzada, anotaciones, asociaciones. Se usa como fuente de datos en SELECT.

</details>

---

### **Pregunta 47: SELECT desde CDS View**

¿Cuál es la diferencia entre leer una tabla de base de datos y una CDS View?

**A)** No hay diferencia en la sintaxis del SELECT  
**B)** Las CDS Views son más lentas que las tablas  
**C)** Las CDS Views no se pueden usar en SELECT  
**D)** Las CDS Views solo se usan con INNER JOIN  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
Sintaxis es la misma: `SELECT ... FROM nombre_cds_view`. CDS Views se usan igual que tablas en SELECT, pero pueden contener lógica predefinida (joins, cálculos).

</details>

---

### **Pregunta 48: INSERT Statement**

¿Cuál es la sintaxis CORRECTA para insertar UN registro en una tabla de base de datos?

**A)** `INSERT /dmo/connection FROM @ls_connection.`  
**B)** `INSERT INTO /dmo/connection VALUES @ls_connection.`  
**C)** `ADD @ls_connection TO /dmo/connection.`  
**D)** `APPEND @ls_connection TO /dmo/connection.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
Sintaxis: `INSERT INTO tabla VALUES @estructura.` o `INSERT tabla FROM @estructura.` Opciones C y D son para tablas internas, no base de datos.

</details>

---

### **Pregunta 49: UPDATE Statement**

¿Qué hace la sentencia UPDATE en una tabla de base de datos?

**A)** Inserta nuevos registros  
**B)** Modifica registros existentes según una condición WHERE  
**C)** Elimina registros de la tabla  
**D)** Selecciona registros para lectura  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** B

**Explicación:**  
`UPDATE tabla SET campo = valor WHERE condición` modifica registros existentes. No inserta ni elimina, solo actualiza valores de campos en registros que cumplan el WHERE.

</details>

---

### **Pregunta 50: DELETE Statement**

¿Cuál es la sintaxis CORRECTA para eliminar registros de una tabla de base de datos?

**A)** `DELETE FROM /dmo/connection WHERE carrier_id = @lv_carrier.`  
**B)** `REMOVE FROM /dmo/connection WHERE carrier_id = @lv_carrier.`  
**C)** `DROP /dmo/connection WHERE carrier_id = @lv_carrier.`  
**D)** `CLEAR /dmo/connection WHERE carrier_id = @lv_carrier.`  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** A

**Explicación:**  
Sintaxis: `DELETE FROM tabla WHERE condición.` REMOVE, DROP y CLEAR no son válidos para eliminar registros de BD. DROP elimina la tabla completa (DDL).

</details>

---

### **Pregunta 51: MODIFY Statement**

¿Qué hace la sentencia MODIFY en base de datos?

**A)** Solo inserta registros nuevos  
**B)** Solo actualiza registros existentes  
**C)** Inserta si no existe, actualiza si existe (UPSERT)  
**D)** Elimina y vuelve a insertar todos los registros  

<details>
<summary>👁️ <b>Ver Respuesta y Explicación</b></summary>

**Respuesta correcta:** C

**Explicación:**  
`MODIFY tabla FROM @estructura` hace UPSERT: si el registro existe (según la clave), lo actualiza; si no existe, lo inserta. Combina INSERT y UPDATE.

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
| **Conceptos Básicos Programación** | 7 | 25-31 |
| **SELECT y Base de Datos** | 20 | 32-51 |
| **TOTAL** | **51** | |

---

## 🗄️ Desglose Sección 6: SELECT y Base de Datos

| Subtema | Preguntas |
|---------|-----------|
| SELECT básico (sintaxis, SINGLE, WHERE) | 32-37 |
| ORDER BY y validaciones | 38 |
| INNER JOIN y LEFT OUTER JOIN | 39-41 |
| Operador IN y DISTINCT | 42-43 |
| Funciones agregación y GROUP BY | 44-45 |
| CDS Views | 46-47 |
| Modificación de datos (INSERT, UPDATE, DELETE, MODIFY) | 48-51 |

---

## 🎯 Criterios de Evaluación

| Puntaje | Nivel | Descripción |
|---------|-------|-------------|
| **46-51** | ⭐⭐⭐ Excelente | Dominio sólido de fundamentos ABAP y BD |
| **39-45** | ⭐⭐ Bueno | Conocimiento adecuado, revisar algunos temas |
| **31-38** | ⭐ Aceptable | Conocimiento básico, requiere refuerzo |
| **< 31** | ⚠️ Insuficiente | Revisar material del curso nuevamente |

---

## 📚 Recursos Adicionales

Si necesitas repasar algún tema:

### Secciones 1-5 (Preguntas 1-31):
- **Diccionario de Datos:** Transacción SE11
- **Tipos de Datos:** Documentación SAP built-in types
- **Clases:** Practicar con IF_OO_ADT_CLASSRUN
- **Programas:** Crear reports simples en Eclipse

### Sección 6 (Preguntas 32-51) - SELECT y BD:
- **SELECT básico:** Practicar con tablas /DMO/*
- **INNER JOIN:** Unir /dmo/connection con /dmo/carrier
- **Agregaciones:** Usar COUNT, SUM, AVG en SELECT
- **CDS Views:** Analizar vistas /DMO/* existentes
- **Modificaciones:** Practicar INSERT/UPDATE/DELETE en tablas Z*

---

## 🔍 Temas de Base de Datos Cubiertos

### Conceptos de Base de Datos Cubiertos:
1. **Host Variables** (`@` en SELECT moderno)
2. **SELECT SINGLE vs SELECT múltiple**
3. **Operadores en WHERE** (=, <>, IN, BETWEEN, LIKE)
4. **INTO TABLE vs INTO estructura**
5. **Validación de resultados** (sy-subrc, IS INITIAL, lines())
6. **ORDER BY** para ordenamiento
7. **INNER JOIN** (sintaxis con alias y ~)
8. **LEFT OUTER JOIN** (diferencias con INNER)
9. **Operador IN** con listas y tablas internas
10. **DISTINCT** para eliminar duplicados
11. **Funciones de agregación** (COUNT, SUM, AVG, MAX, MIN)
12. **GROUP BY** (obligatorio con agregaciones)
13. **CDS Views** como fuente de datos
14. **INSERT** (insertar registros)
15. **UPDATE** (modificar registros)
16. **DELETE** (eliminar registros)
17. **MODIFY** (UPSERT: insert o update)

---

**Material de:** Cursos S4D100 y S4D400 - SAP Learning  
**Formato:** Markdown con respuestas colapsables  
**Fecha:** Enero 2025

¡Buena suerte! 🚀
