# S4D400 - Basic ABAP Programming
## Solutions Guide - Enfoque en Código

> **Curso**: S4D400 - Basic ABAP Programming  
> **Material**: SAP Training - Exercises and Solutions  
> **Versión**: 24  
> **Nota**: Esta guía se enfoca en las soluciones de código. Los pasos de navegación en Eclipse/SAP GUI han sido omitidos intencionalmente.

---

## 📑 Tabla de Contenidos

- [Unit 1: Getting Started](#unit-1-getting-started)
  - [Solution 1: Create an ABAP Cloud Project](#solution-1-create-an-abap-cloud-project-and-investigate-abap-coding)
  - [Solution 2: Create an ABAP Package](#solution-2-create-an-abap-package)
  - [Solution 3: Create a 'Hello World' Application](#solution-3-create-a-hello-world-application)
- [Unit 2: Applying Basic Techniques and Concepts](#unit-2-applying-basic-techniques-and-concepts)
  - [Solution 4: Declare Variables and Process Data](#solution-4-declare-variables-and-process-data)
  - [Solution 5: Implement Conditional Branching](#solution-5-implement-conditional-branching)
  - [Solution 6: Work with Simple Internal Tables](#solution-6-work-with-simple-internal-tables)
  - [Solution 7: Debug ABAP Code](#solution-7-debug-abap-code)
- [Unit 3: Working with Local Classes](#unit-3-working-with-local-classes)
  - [Teoría: Programación Orientada a Objetos en ABAP](#-teoría-programación-orientada-a-objetos-en-abap)
  - [Solution 8: Define a Local Class](#solution-8-define-a-local-class)
  - [Solution 9: Create and Manage Instances](#solution-9-create-and-manage-instances)
  - [Solution 10: Define and Call Methods](#solution-10-define-and-call-methods)
  - [Solution 11: Use Private Attributes and a Constructor](#solution-11-use-private-attributes-and-a-constructor)
- [Unit 4: Reading Data from the Database](#unit-4-reading-data-from-the-database)
  - [Solution 12: Read Data from a Database Table](#solution-12-read-data-from-a-database-table)
  - [Solution 13: Analyze and Use a CDS View Entity](#solution-13-analyze-and-use-a-cds-view-entity)
- [Unit 5: Working with Structured Data Objects](#unit-5-working-with-structured-data-objects)
  - [Solution 14: Use a Structured Data Object](#solution-14-use-a-structured-data-object)
- [Unit 6: Working with Complex Internal Tables](#unit-6-working-with-complex-internal-tables)
  - [Solution 15: Use a Complex Internal Table](#solution-15-use-a-complex-internal-table)
- [Unit 7: Implementing Database Updates Using Business Objects](#unit-7-implementing-database-updates-using-business-objects)
  - [Solution 16: Analyze a Business Object](#solution-16-analyze-a-business-object)
  - [Solution 17: Modify Data Using EML](#solution-17-modify-data-using-eml)
- [Unit 8: Describing the ABAP RESTful Application Programming Model](#unit-8-describing-the-abap-restful-application-programming-model)
  - [Solution 18: Copy a Database Table](#solution-18-copy-a-database-table)
  - [Solution 19: Generate and Preview an OData UI Service](#solution-19-generate-and-preview-an-odata-ui-service)
  - [Solution 20: Validate Price and Currency](#solution-20-validate-price-and-currency)
  - [Solution 21: Adjust the User Interface](#solution-21-adjust-the-user-interface)

---

# Unit 1: Getting Started

## Solution 1: Create an ABAP Cloud Project and Investigate ABAP Coding

**Objetivo**: Configuración inicial del proyecto ABAP Cloud en Eclipse.

**Nota**: Este ejercicio se enfoca en la configuración del entorno de desarrollo. No hay código ABAP que implementar.

**Tareas realizadas**:
- Creación del ABAP Cloud Project
- Conexión con service key
- Análisis de clase `/DMO/CL_FLIGHT_LEGACY` (navegación y exploración del IDE)

---

## Solution 2: Create an ABAP Package

**Objetivo**: Crear el package `ZS4D400_##` donde se almacenarán todos los objetos del curso.

**Estructura del Package**:
- **Name**: `ZS4D400_##` (donde ## es tu número de grupo)
- **Description**: Package for S4D400 exercises
- **Package Type**: Development
- **Software Component**: LOCAL

**Nota**: Este ejercicio se enfoca en la creación del package. No hay código ABAP que implementar.

---

## Solution 3: Create a 'Hello World' Application

**Objetivo**: Crear la primera aplicación ABAP usando la interface `IF_OO_ADT_CLASSRUN` para ejecutar código en la consola.

### Código Completo

```abap
CLASS zcl_##_hello_world DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_##_hello_world IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    out->write( 'Hello World' ).
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

- **Interface `IF_OO_ADT_CLASSRUN`**: Permite ejecutar una clase ABAP como aplicación de consola en Eclipse
- **Método `main`**: Punto de entrada de la aplicación (similar a main() en Java o C)
- **Parámetro `out`**: Objeto para escribir salida a la consola
- **Método `write()`**: Envía texto a la consola de Eclipse

### Ejecución

- **Activar**: `Ctrl + F3`
- **Ejecutar**: `F9`
- **Resultado**: "Hello World" aparece en la vista Console

```
Hello World
```

---

# Unit 2: Applying Basic Techniques and Concepts

## Solution 4: Declare Variables and Process Data

**Objetivo**: Trabajar con variables, tipos de datos, operaciones aritméticas y string templates.

### Código Completo

```abap
CLASS zcl_##_compute DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_##_compute IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
  
    " Declarations
    "**************************
    DATA number1 TYPE i.
    DATA number2 TYPE i.
    DATA result  TYPE p LENGTH 8 DECIMALS 2.
    
    " Input Values
    "**************************
    number1 = -8.
    number2 = 3.
    
    " Calculation
    "**************************
    result = number1 / number2.
    DATA(output) = |{ number1 } / { number2 } = { result }|.
    
    " Output
    "**************************
    out->write( output ).
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Tipos de Datos

- **`TYPE i`**: Entero (integer) - números sin decimales
- **`TYPE p LENGTH 8 DECIMALS 2`**: Packed number - números con decimales
  - `LENGTH 8`: Longitud total del número
  - `DECIMALS 2`: Cantidad de decimales (en este caso, 2)

#### Declaración de Variables

- **Declaración explícita**: `DATA variable TYPE tipo.`
- **Declaración inline**: `DATA(variable) = valor.` (el tipo se infiere automáticamente)

#### String Templates

- **Sintaxis**: `|texto { variable } más texto|`
- **Uso**: Interpola variables dentro de cadenas de texto
- **Ventaja**: Más legible que concatenaciones tradicionales

#### Operaciones Aritméticas

- División estándar: `/`
- El resultado depende del tipo de la variable destino
- Con tipo `i`: resultado redondeado (ejemplo: -8 / 3 = -3)
- Con tipo `p DECIMALS 2`: resultado con decimales (ejemplo: -8 / 3 = -2.67)

### Resultado de Ejecución

```
-8 / 3 = -2.67
```

---

## Solution 5: Implement Conditional Branching

**Objetivo**: Implementar una calculadora con 4 operaciones básicas (+, -, *, /) y manejo de errores (operador inválido, división por cero).

### Código Completo

```abap
CLASS zcl_##_branch DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_##_branch IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
  
    " Declarations
    "**************************
    DATA number1 TYPE i.
    DATA number2 TYPE i.
    DATA result  TYPE p LENGTH 8 DECIMALS 2.
    DATA op      TYPE c LENGTH 1.
    DATA output  TYPE string.
    
    " Input Values
    "**************************
    number1 = 123.
    number2 = 0.
    op      = '/'.
    
    " Calculation
    "**************************
    CASE op.
      WHEN '+'.
        result = number1 + number2.
        
      WHEN '-'.
        result = number1 - number2.
        
      WHEN '*'.
        result = number1 * number2.
        
      WHEN '/'.
        TRY.
            result = number1 / number2.
          CATCH cx_sy_zerodivide.
            output = |Division by zero is not defined|.
        ENDTRY.
        
      WHEN OTHERS.
        output = |'{ op }' is not a valid operator!|.
        
    ENDCASE.
    
    " Construir output solo si no hay error
    IF output IS INITIAL.  "no error so far
      output = |{ number1 } { op } { number2 } = { result }|.
    ENDIF.
    
    " Output
    "**************************
    out->write( output ).
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Control de Flujo - CASE

```abap
CASE variable.
  WHEN 'valor1'.
    " código para valor1
  WHEN 'valor2'.
    " código para valor2
  WHEN OTHERS.
    " código para cualquier otro valor
ENDCASE.
```

- Similar a `switch` en otros lenguajes
- `WHEN OTHERS`: captura todos los casos no especificados
- Cada rama ejecuta código diferente según el valor de la variable

#### Control de Flujo - IF

```abap
IF condicion.
  " código si la condición es verdadera
ENDIF.
```

- **`IS INITIAL`**: verifica si una variable está vacía/sin valor
  - Para strings: verifica si está vacío (`''`)
  - Para números: verifica si es 0
  - Para tablas: verifica si está vacía

#### Manejo de Excepciones - TRY-CATCH

```abap
TRY.
    " código que puede generar excepción
  CATCH nombre_excepcion.
    " código que maneja el error
ENDTRY.
```

- **`cx_sy_zerodivide`**: Excepción lanzada cuando se divide por cero
- El bloque `CATCH` captura el error y evita que el programa termine abruptamente
- Permite manejar situaciones de error de forma controlada

#### Tipos de Datos - Character

- **`TYPE c LENGTH 1`**: Cadena de caracteres de longitud fija (1 carácter)
- Útil para operadores, flags, códigos de un solo carácter

### Casos de Prueba

| number1 | number2 | op  | Resultado Esperado |
|---------|---------|-----|--------------------|
| 123     | 45      | +   | `123 + 45 = 168`   |
| 123     | 45      | -   | `123 - 45 = 78`    |
| 123     | 45      | *   | `123 * 45 = 5535`  |
| 123     | 45      | /   | `123 / 45 = 2.73`  |
| 123     | 0       | /   | `Division by zero is not defined` |
| 123     | 45      | %   | `'%' is not a valid operator!` |

---

## Solution 6: Work with Simple Internal Tables

**Objetivo**: Calcular los primeros N números de Fibonacci usando iteraciones (loops) e internal tables.

### ¿Qué son los Números de Fibonacci?

Secuencia donde cada número es la suma de los dos anteriores:
- Posición 1: 0
- Posición 2: 1
- Posición 3: 0 + 1 = 1
- Posición 4: 1 + 1 = 2
- Posición 5: 1 + 2 = 3
- Posición 6: 2 + 3 = 5
- ...

Secuencia completa: `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...`

### Código Completo

```abap
CLASS zcl_##_iterate DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_##_iterate IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
  
    " Declarations
    "**************************
    CONSTANTS max_count TYPE i VALUE 20.
    
    DATA numbers TYPE TABLE OF i.
    DATA output  TYPE TABLE OF string.
    
    " Calculate Fibonacci Numbers
    "**************************
    DO max_count TIMES.
      
      CASE sy-index.
        WHEN 1.
          " Primer número: 0
          APPEND 0 TO numbers.
          
        WHEN 2.
          " Segundo número: 1
          APPEND 1 TO numbers.
          
        WHEN OTHERS.
          " Resto: suma de los dos anteriores
          APPEND numbers[ sy-index - 2 ] + numbers[ sy-index - 1 ]
                 TO numbers.
                 
      ENDCASE.
      
    ENDDO.
    
    " Format Output
    "**************************
    DATA(counter) = 0.
    
    LOOP AT numbers INTO DATA(number).
      counter = counter + 1.
      
      APPEND |{ counter WIDTH = 4 }: { number WIDTH = 10 ALIGN = RIGHT }|
             TO output.
             
    ENDLOOP.
    
    " Output
    "**************************
    out->write(
      data = output
      name = |The first { max_count } Fibonacci Numbers|
    ).
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Internal Tables (Tablas Internas)

```abap
DATA tabla TYPE TABLE OF tipo.
```

- **Definición**: Estructura de datos dinámica similar a arrays/listas en otros lenguajes
- **Ventaja**: Tamaño dinámico (crece automáticamente)
- **Uso común**: Almacenar conjuntos de datos del mismo tipo

#### Operaciones con Internal Tables

**Agregar elementos (APPEND)**:
```abap
APPEND valor TO tabla.
```
- Añade un elemento al final de la tabla

**Acceso por índice**:
```abap
tabla[ indice ]
```
- Accede al elemento en la posición `indice`
- Los índices comienzan en 1 (no en 0 como en otros lenguajes)

#### Iteraciones - DO

```abap
DO n TIMES.
  " código que se ejecuta n veces
ENDDO.
```

- **`sy-index`**: Variable de sistema que contiene el número de iteración actual
  - Primera iteración: `sy-index = 1`
  - Segunda iteración: `sy-index = 2`
  - ...

#### Iteraciones - LOOP AT

```abap
LOOP AT tabla INTO DATA(variable).
  " código que procesa cada elemento
ENDLOOP.
```

- Recorre cada elemento de la tabla
- **`INTO DATA(variable)`**: Declaración inline de la variable de trabajo
- Cada iteración procesa un elemento diferente

#### String Templates - Formato Avanzado

```abap
|{ variable WIDTH = ancho ALIGN = alineacion }|
```

- **`WIDTH`**: Ancho fijo del campo
- **`ALIGN`**: Alineación del texto
  - `LEFT`: Alineado a la izquierda
  - `RIGHT`: Alineado a la derecha
  - `CENTER`: Centrado

#### Constantes

```abap
CONSTANTS nombre TYPE tipo VALUE valor.
```

- Valor que no cambia durante la ejecución
- Más eficiente y seguro que variables para valores fijos
- Convención: nombres en mayúsculas

### Resultado de Ejecución

```
The first 20 Fibonacci Numbers
   1:          0
   2:          1
   3:          1
   4:          2
   5:          3
   6:          5
   7:          8
   8:         13
   9:         21
  10:         34
  11:         55
  12:         89
  13:        144
  14:        233
  15:        377
  16:        610
  17:        987
  18:       1597
  19:       2584
  20:       4181
```

---

## Solution 7: Debug ABAP Code

**Objetivo**: Aprender a usar el debugger de Eclipse para analizar código ABAP paso a paso.

**Clase Template**: `/LRN/CL_S4D400_BTT_DEBUG`  
**Tu Clase**: `ZCL_##_DEBUG`

### Descripción del Ejercicio

Este ejercicio se enfoca en aprender a usar las herramientas de debugging de Eclipse:
- **Breakpoints**: Detener la ejecución en líneas específicas
- **Watch points**: Observar cambios en variables
- **Single steps**: Ejecutar línea por línea (F5)
- **Step over**: Saltar bloques de código (F6)
- **Resume**: Continuar hasta el siguiente breakpoint (F8)

### Pasos Principales

1. **Copiar** la clase template `/LRN/CL_S4D400_BTT_DEBUG` a tu package
2. **Activar y ejecutar** la clase para ver su output normal
3. **Establecer breakpoints** en las primeras líneas ejecutables
4. **Usar el debugger** para:
   - Inspeccionar valores de variables (`loan_total`, `loan_remaining`, etc.)
   - Observar cómo se llenan las internal tables (`repayment_plan`)
   - Seguir el flujo de ejecución (CASE, LOOP, EXIT)
   - Analizar string templates y expresiones embebidas

### Conceptos de Debugging

- **Variables view**: Muestra valores de todas las variables en contexto
- **Breakpoint**: Pausa la ejecución en una línea específica
- **Watch point**: Pausa cuando una variable cambia de valor
- **Statement breakpoint**: Pausa en todas las ocurrencias de un statement (ej: EXIT)
- **F5 (Step Into)**: Entra en métodos y sub-bloques
- **F6 (Step Over)**: Ejecuta como un solo paso
- **F8 (Resume)**: Continúa hasta el siguiente breakpoint

### Nota Importante

Este ejercicio **no modifica el código** de la clase. Es puramente un ejercicio práctico de uso del debugger. La solución oficial indica: *"None, the class remains unchanged"*.

---

# Unit 3: Working with Local Classes

## 📚 Teoría: Programación Orientada a Objetos en ABAP

Antes de comenzar con los ejercicios de esta unidad, es fundamental entender los conceptos de OOP (Object-Oriented Programming) en ABAP.

### ¿Qué es una Clase?

Una **clase** es un plano o plantilla que define:
- **Atributos** (datos/propiedades)
- **Métodos** (comportamientos/funciones)

Es como un molde para crear objetos con características y capacidades específicas.

### Analogía del Mundo Real

Piensa en una clase como el plano de una casa:
- **Clase `Casa`**: El diseño arquitectónico
- **Instancias de `Casa`**: Las casas reales construidas a partir del plano
- **Atributos**: Color de la casa, número de habitaciones, dirección
- **Métodos**: Abrir puerta, encender luces, regar jardín

### Clases Globales vs Clases Locales

#### Clases Globales
```abap
CLASS zcl_##_my_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC.
  
  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.

CLASS zcl_##_my_class IMPLEMENTATION.
  " Implementación de métodos
ENDCLASS.
```

**Características**:
- Son objetos ABAP independientes en el repositorio
- Visibles en todo el sistema
- Se pueden usar desde cualquier programa
- Nombre comienza con `Z` o `Y` (para objetos custom)

#### Clases Locales
```abap
CLASS lcl_connection DEFINITION.
  PUBLIC SECTION.
    DATA carrier_id TYPE /dmo/carrier_id.
ENDCLASS.

CLASS lcl_connection IMPLEMENTATION.
  " Implementación de métodos
ENDCLASS.
```

**Características**:
- Definidas dentro de una clase global o programa
- Solo visibles dentro del contexto donde se definen
- Nombre generalmente comienza con `lcl_` (local class)
- Útiles para encapsular lógica interna

### Atributos (Datos de la Clase)

Los atributos almacenan el **estado** de un objeto.

#### Atributos de Instancia (Instance Attributes)
```abap
DATA carrier_id TYPE /dmo/carrier_id.
DATA connection_id TYPE /dmo/connection_id.
```

- **Únicos para cada instancia** de la clase
- Cada objeto tiene su propia copia
- Analogía: Cada casa tiene su propio color y dirección

#### Atributos Estáticos (Static Attributes)
```abap
CLASS-DATA conn_counter TYPE i.
```

- **Compartidos** entre todas las instancias
- Solo existe una copia para toda la clase
- Analogía: El contador de casas construidas (es el mismo para todas)

### Visibilidad de Atributos y Métodos

ABAP usa **tres niveles de visibilidad**:

#### PUBLIC SECTION (Público)
```abap
PUBLIC SECTION.
  DATA carrier_id TYPE /dmo/carrier_id.
  METHODS get_output RETURNING VALUE(r_output) TYPE string_table.
```

- Accesible desde **cualquier parte**
- Uso: `objeto->carrier_id` o `objeto->get_output()`
- Analogía: La puerta principal de la casa (todos pueden verla)

#### PROTECTED SECTION (Protegido)
```abap
PROTECTED SECTION.
  DATA internal_buffer TYPE string.
```

- Accesible desde **la misma clase y sus subclases**
- No accesible desde fuera
- Analogía: El garaje (solo la familia tiene acceso)

#### PRIVATE SECTION (Privado)
```abap
PRIVATE SECTION.
  DATA secret_key TYPE string.
  METHODS validate_data.
```

- Accesible **solo dentro de la misma clase**
- Máxima encapsulación
- Analogía: La caja fuerte (solo el dueño tiene la llave)

### Encapsulación

La **encapsulación** es el principio de:
1. **Ocultar** los detalles internos (datos privados)
2. **Exponer** una interfaz pública (métodos públicos)

#### ❌ MAL: Atributos públicos (sin encapsulación)
```abap
CLASS lcl_connection DEFINITION.
  PUBLIC SECTION.
    DATA carrier_id TYPE /dmo/carrier_id.  " ❌ Cualquiera puede modificar
ENDCLASS.

" Uso (problemático):
connection->carrier_id = 'XX'.  " Sin validación, sin control
```

#### ✅ BIEN: Atributos privados + métodos públicos (con encapsulación)
```abap
CLASS lcl_connection DEFINITION.
  PUBLIC SECTION.
    METHODS set_carrier
      IMPORTING i_carrier_id TYPE /dmo/carrier_id
      RAISING cx_abap_invalid_value.      " ✅ Validación controlada
      
    METHODS get_carrier
      RETURNING VALUE(r_carrier) TYPE /dmo/carrier_id.  " ✅ Acceso seguro
      
  PRIVATE SECTION.
    DATA carrier_id TYPE /dmo/carrier_id.  " ✅ Solo la clase puede modificar
ENDCLASS.

" Uso (controlado):
TRY.
    connection->set_carrier( 'LH' ).  " Con validación
  CATCH cx_abap_invalid_value.
    " Manejo de error
ENDTRY.
```

### Métodos

Los métodos definen el **comportamiento** de una clase.

#### Tipos de Métodos

##### 1. Métodos de Instancia (Instance Methods)
```abap
METHODS set_attributes
  IMPORTING
    i_carrier_id    TYPE /dmo/carrier_id
    i_connection_id TYPE /dmo/connection_id.
```

- Operan sobre **una instancia específica**
- Pueden acceder a atributos de instancia y estáticos
- Llamada: `objeto->set_attributes(...)`

##### 2. Métodos Estáticos (Static Methods)
```abap
CLASS-METHODS get_instance_count
  RETURNING VALUE(r_count) TYPE i.
```

- Operan a **nivel de clase**, no de instancia
- Solo pueden acceder a atributos estáticos
- Llamada: `clase=>get_instance_count()`

##### 3. Constructor de Instancia
```abap
METHODS constructor
  IMPORTING
    i_carrier_id    TYPE /dmo/carrier_id
    i_connection_id TYPE /dmo/connection_id
  RAISING
    cx_abap_invalid_value.
```

- Nombre especial: `constructor`
- Se ejecuta **automáticamente** al crear una instancia
- Usado para **inicializar** el objeto
- Solo puede haber **uno** por clase

##### 4. Métodos Funcionales (Functional Methods)
```abap
METHODS get_output
  RETURNING VALUE(r_output) TYPE string_table.
```

- Retornan un **valor**
- Usan el parámetro `RETURNING`
- Pueden usarse directamente en expresiones

**Ejemplo de uso**:
```abap
out->write( connection->get_output() ).  " Llamada directa en expresión
```

### Parámetros de Métodos

#### IMPORTING (Entrada)
```abap
METHODS set_data
  IMPORTING
    i_value TYPE i.
```
- Recibe datos **desde** el caller
- El caller provee el valor

#### EXPORTING (Salida)
```abap
METHODS get_data
  EXPORTING
    e_value TYPE i.
```
- Envía datos **hacia** el caller
- El caller recibe el valor

#### RETURNING (Retorno)
```abap
METHODS get_value
  RETURNING VALUE(r_value) TYPE i.
```
- Similar a EXPORTING, pero más conveniente
- Permite usar el método en expresiones
- **Solo puede haber uno** por método

#### RAISING (Excepciones)
```abap
METHODS validate
  RAISING cx_abap_invalid_value.
```
- Declara qué excepciones puede lanzar el método
- El caller debe manejar estas excepciones con TRY-CATCH

### Referencias y Objetos

En OOP, trabajamos con **referencias** a objetos, no con los objetos directamente.

#### Variables de Referencia
```abap
DATA connection TYPE REF TO lcl_connection.
```

- `connection` es una **referencia** (un apuntador)
- `TYPE REF TO lcl_connection`: Tipo de referencia a la clase
- Inicialmente tiene valor **inicial** (no apunta a nada)

#### Crear Instancias (Objetos)
```abap
connection = NEW #( ).
```

- `NEW #()`: Crea una **nueva instancia** de la clase
- `#`: El tipo se infiere de la variable de referencia
- Llama automáticamente al **constructor**

#### Crear Instancias con Parámetros
```abap
connection = NEW #(
  i_carrier_id    = 'LH'
  i_connection_id = '0400'
).
```

- Pasa parámetros al **constructor**
- Inicializa el objeto en una sola expresión

#### Acceso a Componentes
```abap
" Acceso a atributos
connection->carrier_id = 'AA'.

" Llamada a métodos
connection->set_attributes(
  i_carrier_id    = 'LH'
  i_connection_id = '0400'
).

DATA(output) = connection->get_output().
```

- Operador `->`: Accede a atributos y métodos de la instancia

### Internal Tables de Referencias

Podemos almacenar múltiples referencias en una internal table:

```abap
" Declaración
DATA connections TYPE TABLE OF REF TO lcl_connection.

" Agregar referencias
APPEND connection TO connections.

" Recorrer la tabla
LOOP AT connections INTO DATA(conn).
  out->write( conn->get_output() ).
ENDLOOP.
```

### Manejo de Excepciones en Métodos

```abap
" Definición del método
METHODS set_attributes
  IMPORTING
    i_carrier_id TYPE /dmo/carrier_id
  RAISING
    cx_abap_invalid_value.

" Implementación
METHOD set_attributes.
  IF i_carrier_id IS INITIAL.
    RAISE EXCEPTION TYPE cx_abap_invalid_value.
  ENDIF.
  carrier_id = i_carrier_id.
ENDMETHOD.

" Llamada con manejo de excepciones
TRY.
    connection->set_attributes( i_carrier_id = 'LH' ).
  CATCH cx_abap_invalid_value.
    out->write( 'Invalid value provided' ).
ENDTRY.
```

### Palabra Clave `me`

Dentro de un método, `me` es una referencia al **objeto actual** (this en otros lenguajes):

```abap
METHOD constructor.
  me->carrier_id = i_carrier_id.
  " Equivalente a:
  " carrier_id = i_carrier_id.
ENDMETHOD.
```

- Útil para **disambiguar** cuando hay parámetros con el mismo nombre
- Hace el código más **explícito**

### Atributo READ-ONLY

```abap
CLASS-DATA conn_counter TYPE i READ-ONLY.
```

- El atributo puede ser **leído** desde fuera
- Solo puede ser **modificado** desde dentro de la clase
- Útil para contadores, configuraciones constantes, etc.

### Buenas Prácticas de OOP

1. **Encapsulación**: Hacer atributos privados y exponer métodos públicos
2. **Validación en Constructor**: Validar parámetros y lanzar excepciones si son inválidos
3. **Métodos Cohesivos**: Cada método debe tener una responsabilidad clara
4. **Nombres Descriptivos**: `get_output()`, `set_attributes()`, no `do_stuff()`
5. **Usar READ-ONLY**: Para atributos que no deben modificarse externamente

---

## Solution 8: Define a Local Class

**Objetivo**: Crear una clase local dentro de una clase global y declarar atributos públicos.

**Clase Global**: `ZCL_##_LOCAL_CLASS`  
**Clase Local**: `lcl_connection`

### Código Completo

#### Global Class (Tab: Global Class)
```abap
CLASS zcl_##_local_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_##_local_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Por ahora vacío - se llenará en ejercicios siguientes
    
  ENDMETHOD.
  
ENDCLASS.
```

#### Local Class (Tab: Local Types)
```abap
*"* use this source file for the definition and implementation of
*"* local helper classes, interface definitions and type
*"* declarations

CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    " Atributos de instancia
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    
    " Atributo estático (compartido por todas las instancias)
    CLASS-DATA conn_counter TYPE i.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
  
ENDCLASS.


CLASS lcl_connection IMPLEMENTATION.
  " Por ahora vacío - se llenará en ejercicios siguientes
ENDCLASS.
```

### Conceptos Clave

#### Clase Local
- Definida dentro del **tab "Local Types"** de una clase global
- Prefijo `lcl_` (local class)
- Solo visible dentro de la clase global donde se define

#### DATA vs CLASS-DATA

**DATA (Atributo de Instancia)**:
- Cada objeto tiene su **propia copia**
- Valores pueden ser diferentes entre instancias
- Ejemplo: `carrier_id` es único para cada conexión

**CLASS-DATA (Atributo Estático)**:
- **Una sola copia** compartida por todas las instancias
- Mismo valor para todos los objetos
- Ejemplo: `conn_counter` cuenta el total de conexiones creadas

#### CREATE PUBLIC

Al crear la clase con quick fix, Eclipse genera `CREATE PRIVATE`:
```abap
CLASS lcl_connection DEFINITION CREATE PRIVATE.
```

**DEBES ELIMINARLO** para permitir crear instancias desde fuera:
```abap
CLASS lcl_connection DEFINITION.  " ✅ Sin CREATE PRIVATE
```

- `CREATE PRIVATE`: Solo se pueden crear instancias **dentro** de la clase (patrón Singleton)
- Sin adición: Se pueden crear instancias desde **cualquier parte** (normal)

### Tabla de Atributos

| Atributo       | Scope    | Data Type           | Descripción                    |
|----------------|----------|---------------------|--------------------------------|
| carrier_id     | instance | /DMO/CARRIER_ID     | ID de la aerolínea (ej: 'LH')  |
| connection_id  | instance | /DMO/CONNECTION_ID  | ID de la conexión (ej: '0400') |
| conn_counter   | static   | I                   | Contador de conexiones creadas |

---

## Solution 9: Create and Manage Instances

**Objetivo**: Crear instancias de la clase local y almacenar múltiples referencias en una internal table.

**Template**: `/LRN/CL_S4D400_CLS_LOCAL_CLASS`  
**Solución**: `/LRN/CL_S4D400_CLS_INSTANCES` (o continuar con `ZCL_##_LOCAL_CLASS`)

### Código Completo

#### Global Class - Method main
```abap
METHOD if_oo_adt_classrun~main.

  " Declarations
  "**************************
  DATA connection  TYPE REF TO lcl_connection.
  DATA connections TYPE TABLE OF REF TO lcl_connection.

  " First Instance
  "**************************
  connection = NEW #( ).
  
  connection->carrier_id    = 'LH'.
  connection->connection_id = '0400'.
  
  APPEND connection TO connections.

  " Second Instance
  "**************************
  connection = NEW #( ).
  
  connection->carrier_id    = 'AA'.
  connection->connection_id = '0017'.
  
  APPEND connection TO connections.

  " Third Instance
  "**************************
  connection = NEW #( ).
  
  connection->carrier_id    = 'SQ'.
  connection->connection_id = '0001'.
  
  APPEND connection TO connections.

ENDMETHOD.
```

#### Local Class (sin cambios desde Solution 8)
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    CLASS-DATA conn_counter TYPE i.
    
ENDCLASS.

CLASS lcl_connection IMPLEMENTATION.
ENDCLASS.
```

### Conceptos Clave

#### Referencias a Objetos

```abap
DATA connection TYPE REF TO lcl_connection.
```

- `connection` es una **variable de referencia**
- No es el objeto en sí, es un **apuntador** al objeto
- Tipo: `REF TO` seguido del nombre de la clase

#### Crear Instancias

```abap
connection = NEW #( ).
```

- `NEW`: Operador de creación de instancias
- `#( )`: El tipo se infiere de la variable (`lcl_connection`)
- Cada llamada crea un **nuevo objeto** en memoria

#### Acceso a Atributos Públicos

```abap
connection->carrier_id = 'LH'.
```

- Operador `->`: Acceso a componentes de la instancia
- Se puede leer y escribir atributos públicos directamente

#### Internal Table de Referencias

```abap
DATA connections TYPE TABLE OF REF TO lcl_connection.
```

- Tabla que almacena **referencias** a objetos
- No almacena los objetos directamente
- Tipo de línea: `REF TO lcl_connection`

#### Reusar Variable de Referencia

```abap
connection = NEW #( ).  " Primera instancia
connection->carrier_id = 'LH'.
APPEND connection TO connections.

connection = NEW #( ).  " Segunda instancia (diferente)
connection->carrier_id = 'AA'.
APPEND connection TO connections.
```

- La variable `connection` se reutiliza
- Cada `NEW #()` crea un **objeto diferente**
- `APPEND` guarda la **referencia** (no una copia)
- Resultado: La tabla contiene referencias a 3 objetos diferentes

### Visualización en el Debugger

Al debuggear, puedes ver:

1. **Variables View**:
   - `connection`: Muestra la referencia actual
   - Expandir `connection` muestra los atributos del objeto

2. **connections (Internal Table)**:
   - Muestra la lista de referencias
   - Cada línea apunta a un objeto diferente

### Importante: Diferencia entre Copia y Referencia

```abap
" Con tipos simples (copia)
DATA number1 TYPE i VALUE 10.
DATA number2 TYPE i.
number2 = number1.  " number2 obtiene una COPIA del valor

" Con objetos (referencia)
DATA conn1 TYPE REF TO lcl_connection.
DATA conn2 TYPE REF TO lcl_connection.

conn1 = NEW #( ).
conn1->carrier_id = 'LH'.

conn2 = conn1.  " conn2 apunta al MISMO objeto que conn1
conn2->carrier_id = 'AA'.  " ¡Modifica el objeto compartido!

" Ahora conn1->carrier_id también es 'AA'
```

---

## Solution 10: Define and Call Methods

**Objetivo**: Definir métodos en la clase local (setter, getter funcional) y llamarlos con manejo de excepciones.

**Template**: `/LRN/CL_S4D400_CLS_INSTANCES`  
**Solución**: `/LRN/CL_S4D400_CLS_METHODS` (o continuar con la clase anterior)

### Código Completo

#### Local Class - Definition
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    " Atributos
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    CLASS-DATA conn_counter TYPE i.
    
    " Métodos
    METHODS set_attributes
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
        
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PROTECTED SECTION.
  PRIVATE SECTION.
  
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD set_attributes.
    
    " Validación de parámetros
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    " Asignación de atributos
    carrier_id    = i_carrier_id.
    connection_id = i_connection_id.
    
  ENDMETHOD.

  METHOD get_output.
    
    " Construir salida formateada
    APPEND |------------------------------| TO r_output.
    APPEND |Carrier:    { carrier_id    }| TO r_output.
    APPEND |Connection: { connection_id }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

#### Global Class - Method main
```abap
METHOD if_oo_adt_classrun~main.

  " Declarations
  "**************************
  DATA connection  TYPE REF TO lcl_connection.
  DATA connections TYPE TABLE OF REF TO lcl_connection.

  " First Instance
  "**************************
  connection = NEW #( ).
  
  TRY.
      connection->set_attributes(
        i_carrier_id    = 'LH'
        i_connection_id = '0400'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Second Instance
  "**************************
  connection = NEW #( ).
  
  TRY.
      connection->set_attributes(
        i_carrier_id    = 'AA'
        i_connection_id = '0017'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Third Instance
  "**************************
  connection = NEW #( ).
  
  TRY.
      connection->set_attributes(
        i_carrier_id    = 'SQ'
        i_connection_id = '0001'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Output
  "**************************
  LOOP AT connections INTO connection.
    out->write( connection->get_output( ) ).
  ENDLOOP.

ENDMETHOD.
```

### Conceptos Clave

#### Método con IMPORTING

```abap
METHODS set_attributes
  IMPORTING
    i_carrier_id    TYPE /dmo/carrier_id
    i_connection_id TYPE /dmo/connection_id
  RAISING
    cx_abap_invalid_value.
```

- **IMPORTING**: Recibe parámetros desde el caller
- **RAISING**: Declara qué excepciones puede lanzar
- El caller **debe** manejar estas excepciones con TRY-CATCH

#### Método Funcional (RETURNING)

```abap
METHODS get_output
  RETURNING VALUE(r_output) TYPE string_table.
```

- **RETURNING**: Retorna un valor directamente
- Puede usarse en expresiones
- No puede combinarse con EXPORTING

#### Lanzar Excepciones

```abap
IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
  RAISE EXCEPTION TYPE cx_abap_invalid_value.
ENDIF.
```

- `RAISE EXCEPTION TYPE`: Lanza una excepción
- El método se detiene inmediatamente
- El caller captura la excepción en el bloque CATCH

#### Manejo de Excepciones

```abap
TRY.
    connection->set_attributes(
      i_carrier_id    = 'LH'
      i_connection_id = '0400'
    ).
    APPEND connection TO connections.  " Solo si no hay excepción
    
  CATCH cx_abap_invalid_value.
    out->write( 'Method call failed' ).
ENDTRY.
```

- **TRY**: Bloque de código que puede generar excepciones
- **CATCH**: Maneja la excepción si ocurre
- Si hay excepción, el código después del método **NO se ejecuta**

#### Llamada a Método Funcional

```abap
out->write( connection->get_output( ) ).
```

- Método `get_output()` se llama **dentro de la expresión**
- Retorna `string_table` directamente
- Más conciso que usar una variable intermedia

#### Code Completion en Eclipse

Para usar code completion al llamar métodos:

1. Escribir `connection->` y presionar `Ctrl + Space`
2. Seleccionar el método de la lista
3. Presionar `Shift + Enter` para insertar la **firma completa**

```abap
" Al presionar Shift + Enter, genera automáticamente:
connection->set_attributes(
  EXPORTING
    i_carrier_id    =
    i_connection_id =
).
```

### Resultado de Ejecución

```
------------------------------
Carrier:    LH
Connection: 0400
------------------------------
Carrier:    AA
Connection: 0017
------------------------------
Carrier:    SQ
Connection: 0001
```

---

## Solution 11: Use Private Attributes and a Constructor

**Objetivo**: Hacer los atributos de instancia privados, agregar un constructor para inicializarlos, y usar un atributo estático READ-ONLY.

**Template**: `/LRN/CL_S4D400_CLS_METHODS`  
**Solución**: `/LRN/CL_S4D400_CLS_CONSTRUCTOR` (o continuar con la clase anterior)

### Código Completo

#### Local Class - Definition
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    " Atributo estático READ-ONLY
    CLASS-DATA conn_counter TYPE i READ-ONLY.
    
    " Constructor de instancia
    METHODS constructor
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
    
    " Método público para obtener output
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PROTECTED SECTION.
  
  PRIVATE SECTION.
    " Atributos de instancia PRIVADOS
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD constructor.
    
    " Validación de parámetros
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    " Asignación de atributos usando 'me'
    me->carrier_id    = i_carrier_id.
    me->connection_id = i_connection_id.
    
    " Incrementar contador estático
    conn_counter = conn_counter + 1.
    
  ENDMETHOD.

  METHOD get_output.
    
    " Construir salida formateada
    APPEND |------------------------------| TO r_output.
    APPEND |Carrier:    { carrier_id    }| TO r_output.
    APPEND |Connection: { connection_id }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

#### Global Class - Method main
```abap
METHOD if_oo_adt_classrun~main.

  " Declarations
  "**************************
  DATA connection  TYPE REF TO lcl_connection.
  DATA connections TYPE TABLE OF REF TO lcl_connection.

  " First Instance
  "**************************
  TRY.
      connection = NEW #(
        i_carrier_id    = 'LH'
        i_connection_id = '0400'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Second Instance
  "**************************
  TRY.
      connection = NEW #(
        i_carrier_id    = 'AA'
        i_connection_id = '0017'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Third Instance
  "**************************
  TRY.
      connection = NEW #(
        i_carrier_id    = 'SQ'
        i_connection_id = '0001'
      ).
      
      APPEND connection TO connections.
      
    CATCH cx_abap_invalid_value.
      out->write( 'Method call failed' ).
  ENDTRY.

  " Output
  "**************************
  LOOP AT connections INTO connection.
    out->write( connection->get_output( ) ).
  ENDLOOP.
  
  " Mostrar contador de conexiones
  out->write( |Total connections created: { lcl_connection=>conn_counter }| ).

ENDMETHOD.
```

### Conceptos Clave

#### Atributos Privados

```abap
PRIVATE SECTION.
  DATA carrier_id    TYPE /dmo/carrier_id.
  DATA connection_id TYPE /dmo/connection_id.
```

**Beneficios**:
- **Encapsulación**: Los datos están protegidos
- **Control**: Solo la clase puede modificarlos
- **Validación**: Cambios pasan por métodos controlados

**Acceso**:
- ❌ `connection->carrier_id = 'LH'`  " Error: atributo privado
- ✅ Solo desde dentro de la clase (en métodos)

#### Constructor de Instancia

```abap
METHODS constructor
  IMPORTING
    i_carrier_id    TYPE /dmo/carrier_id
    i_connection_id TYPE /dmo/connection_id
  RAISING
    cx_abap_invalid_value.
```

**Características**:
- Nombre especial: **`constructor`**
- Se ejecuta **automáticamente** al crear la instancia
- Usado para **inicializar** el objeto
- Solo puede haber **uno** por clase

**Llamada implícita**:
```abap
connection = NEW #(
  i_carrier_id    = 'LH'
  i_connection_id = '0400'
).
" ↑ Esto llama automáticamente al constructor
```

#### Uso de `me`

```abap
me->carrier_id = i_carrier_id.
```

- `me`: Referencia al **objeto actual** (similar a `this` en Java/C++)
- Útil cuando hay **ambigüedad** de nombres
- Hace el código más **explícito**

#### Atributo READ-ONLY

```abap
CLASS-DATA conn_counter TYPE i READ-ONLY.
```

**Características**:
- Puede ser **leído** desde fuera de la clase
- Solo puede ser **modificado** dentro de la clase

**Acceso**:
- ✅ `lcl_connection=>conn_counter`  " Leer (OK)
- ❌ `lcl_connection=>conn_counter = 5`  " Modificar (Error)

#### Acceso a Atributos Estáticos

```abap
out->write( |Total: { lcl_connection=>conn_counter }| ).
```

- Operador `=>`: Acceso a componentes **estáticos** de la clase
- No requiere una instancia
- Sintaxis: `nombre_clase=>componente_estático`

#### Incrementar Contador en Constructor

```abap
METHOD constructor.
  " ... validación ...
  
  me->carrier_id    = i_carrier_id.
  me->connection_id = i_connection_id.
  
  conn_counter = conn_counter + 1.  " Se ejecuta solo si no hay excepción
ENDMETHOD.
```

- El contador se incrementa **después** de la validación
- Si el constructor lanza una excepción, el objeto **no se crea**
- El contador solo cuenta instancias **exitosamente creadas**

#### Quick Fix: Generate Constructor

En Eclipse, puedes generar el constructor automáticamente:

1. Colocar cursor en el nombre de la clase
2. Presionar `Ctrl + 1`
3. Seleccionar **"Generate constructor"**
4. Marcar los atributos que serán parámetros
5. Eclipse genera la definición e implementación básica

### Comparación: Antes vs Después

#### ANTES (Solution 9-10):
```abap
" Atributos públicos - cualquiera puede modificar
connection = NEW #( ).
connection->carrier_id = 'LH'.  " Acceso directo
connection->connection_id = '0400'.

" O usando método setter
connection->set_attributes(
  i_carrier_id    = 'LH'
  i_connection_id = '0400'
).
```

#### DESPUÉS (Solution 11):
```abap
" Atributos privados + constructor
" Inicialización forzada al crear el objeto
connection = NEW #(
  i_carrier_id    = 'LH'
  i_connection_id = '0400'
).

" No se puede acceder directamente
" connection->carrier_id = 'AA'.  " ❌ Error de compilación
```

### Ventajas del Constructor

1. **Garantiza inicialización**: El objeto siempre está en un estado válido
2. **Inmutabilidad**: Los atributos no pueden cambiar después de crearse
3. **Validación centralizada**: Todas las instancias pasan por la misma validación
4. **Código más limpio**: Creación e inicialización en una sola línea

### Resultado de Ejecución

```
------------------------------
Carrier:    LH
Connection: 0400
------------------------------
Carrier:    AA
Connection: 0017
------------------------------
Carrier:    SQ
Connection: 0001
Total connections created: 3
```

---

## 📝 Notas Importantes

### Convenciones de Nombres

- `##`: Sustituir por tu número de grupo (ejemplo: `01`, `02`, etc.)
- Classes globales: `ZCL_##_NOMBRE`
- Classes locales: `lcl_nombre`
- Packages: `ZS4D400_##`

### Activación y Ejecución

- **Activar clase**: `Ctrl + F3`
- **Ejecutar como console app**: `F9`
- **Abrir objeto ABAP**: `Ctrl + Shift + A`
- **Quick Fix**: `Ctrl + 1`
- **Code Completion**: `Ctrl + Space`
- **Insert Full Signature**: `Shift + Enter` (después de seleccionar método)

### Debugging

- **Toggle Breakpoint**: Doble clic en margen izquierdo
- **F5**: Step Into (entra en métodos)
- **F6**: Step Over (ejecuta método completo)
- **F8**: Resume (continua hasta siguiente breakpoint)
- **Watch Point**: Click derecho en variable → "Set Watchpoint"

### Buenas Prácticas OOP

1. **Encapsulación**: Atributos privados, métodos públicos
2. **Validación en Constructor**: Garantizar estado válido del objeto
3. **Usar Excepciones**: Para errores de validación (no retornar códigos de error)
4. **Métodos Cohesivos**: Cada método tiene una responsabilidad clara
5. **Nombres Descriptivos**: `get_output()`, `set_attributes()`, no `do_stuff()`
6. **READ-ONLY para Contadores**: Proteger atributos que no deben modificarse externamente

---

**Siguiente**: Unit 4 - Reading Data from the Database

# Unit 4: Reading Data from the Database

## Solution 12: Read Data from a Database Table

**Objetivo**: Extender la clase con atributos para aeropuertos (origen/destino) y leer sus valores desde una tabla de base de datos usando SELECT.

**Template**: `/LRN/CL_S4D400_CLS_CONSTRUCTOR`  
**Solución**: `/LRN/CL_S4D400_DBS_SELECT` (o continuar con `ZCL_##_CONSTRUCTOR`)

### Código Completo

#### Local Class - Definition (cambios marcados)
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    CLASS-DATA conn_counter TYPE i READ-ONLY.
    
    METHODS constructor
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
    
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PROTECTED SECTION.
  
  PRIVATE SECTION.
    DATA carrier_id      TYPE /dmo/carrier_id.
    DATA connection_id   TYPE /dmo/connection_id.
    
    " Nuevos atributos para aeropuertos
    DATA airport_from_id TYPE /dmo/airport_from_id.
    DATA airport_to_id   TYPE /dmo/airport_to_id.
    
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD constructor.
    
    " Validación de parámetros
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    " Asignación de atributos
    me->carrier_id    = i_carrier_id.
    me->connection_id = i_connection_id.
    
    " Leer datos de aeropuertos desde base de datos
    SELECT SINGLE
      FROM /dmo/connection
      FIELDS airport_from_id, airport_to_id
      WHERE carrier_id    = @i_carrier_id
        AND connection_id = @i_connection_id
      INTO ( @airport_from_id, @airport_to_id ).
    
    " Validar que se encontró el registro
    IF sy-subrc <> 0.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    " Incrementar contador
    conn_counter = conn_counter + 1.
    
  ENDMETHOD.

  METHOD get_output.
    
    " Construir salida formateada
    APPEND |--------------------------------| TO r_output.
    APPEND |Carrier:     { carrier_id    }| TO r_output.
    APPEND |Connection:  { connection_id }| TO r_output.
    APPEND |Departure:   { airport_from_id }| TO r_output.
    APPEND |Destination: { airport_to_id   }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### SELECT Statement Básico

```abap
SELECT SINGLE
  FROM tabla
  FIELDS campo1, campo2
  WHERE condicion1 = @valor1
    AND condicion2 = @valor2
  INTO ( @variable1, @variable2 ).
```

**Componentes**:
- **SELECT SINGLE**: Lee un solo registro (no una tabla)
- **FROM**: Especifica la tabla de base de datos
- **FIELDS**: Lista de campos a leer
- **WHERE**: Condiciones de filtrado
- **INTO**: Variables destino para los valores

#### Escape de Variables (@)

```abap
WHERE carrier_id = @i_carrier_id
INTO ( @airport_from_id, @airport_to_id )
```

- **Prefijo `@`**: Obligatorio para variables en SQL moderno
- Indica que es una variable de ABAP, no un campo de tabla
- Sin `@` genera error de sintaxis

#### System Field sy-subrc

```abap
IF sy-subrc <> 0.
  RAISE EXCEPTION TYPE cx_abap_invalid_value.
ENDIF.
```

- **sy-subrc**: Código de retorno del último statement
- `0`: Operación exitosa
- `<> 0`: Operación falló (registro no encontrado, error, etc.)
- Siempre verificar después de operaciones de base de datos

#### Client Handling Automático

En la WHERE condition **NO se especifica** el campo client:
```abap
WHERE carrier_id = @i_carrier_id  " ✅ Correcto
```

**¿Por qué?**
- El compilador agrega automáticamente la condición del client
- Todas las tablas multi-client filtran por el client actual
- Esto es parte de la arquitectura multi-tenant de SAP

### Resultado de Ejecución

```
--------------------------------
Carrier:     LH
Connection:  0400
Departure:   FRA
Destination: JFK
--------------------------------
Carrier:     AA
Connection:  0017
Departure:   JFK
Destination: SFO
--------------------------------
Carrier:     SQ
Connection:  0001
Departure:   SIN
Destination: SFO
Total connections created: 3
```

---

## Solution 13: Analyze and Use a CDS View Entity

**Objetivo**: Leer datos desde una CDS view entity en lugar de la tabla directamente, obteniendo también el nombre de la aerolínea usando asociaciones.

**Template**: `/LRN/CL_S4D400_DBS_SELECT`  
**Solución**: `/LRN/CL_S4D400_DBS_CDS` (o continuar con la clase anterior)

### Código Completo

#### Local Class - Definition (cambios marcados)
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    CLASS-DATA conn_counter TYPE i READ-ONLY.
    
    METHODS constructor
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
    
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PRIVATE SECTION.
    DATA carrier_id      TYPE /dmo/carrier_id.
    DATA connection_id   TYPE /dmo/connection_id.
    DATA airport_from_id TYPE /dmo/airport_from_id.
    DATA airport_to_id   TYPE /dmo/airport_to_id.
    
    " Nuevo atributo para nombre de aerolínea
    DATA carrier_name    TYPE /dmo/carrier_name.
    
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD constructor.
    
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    me->carrier_id    = i_carrier_id.
    me->connection_id = i_connection_id.
    
    " Leer desde CDS view entity (no tabla directa)
    SELECT SINGLE
      FROM /DMO/I_Connection
      FIELDS DepartureAirport,
             DestinationAirport,
             \_Airline-Name              " Acceso a asociación
      WHERE AirlineID    = @i_carrier_id
        AND ConnectionID = @i_connection_id
      INTO ( @airport_from_id, @airport_to_id, @carrier_name ).
    
    IF sy-subrc <> 0.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    conn_counter = conn_counter + 1.
    
  ENDMETHOD.

  METHOD get_output.
    
    APPEND |--------------------------------| TO r_output.
    APPEND |Carrier:     { carrier_id } { carrier_name }| TO r_output.
    APPEND |Connection:  { connection_id }| TO r_output.
    APPEND |Departure:   { airport_from_id }| TO r_output.
    APPEND |Destination: { airport_to_id   }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### CDS View Entity

**¿Qué es?**
- Vista de base de datos mejorada con semántica de negocio
- Puede tener **asociaciones** (relaciones) a otras vistas
- Campos con alias más descriptivos
- Metadatos y anotaciones adicionales

**Ventajas sobre tablas directas**:
- Acceso más semántico (`DepartureAirport` vs `airport_from_id`)
- Navegación por asociaciones (joins automáticos)
- Lógica de negocio encapsulada

#### Asociaciones en CDS

```abap
\_Airline-Name
```

**Sintaxis**:
- `\_Airline`: Nombre de la asociación (prefijo `\_`)
- `-Name`: Campo del target de la asociación

**Equivalente sin asociación**:
```sql
SELECT ... FROM connection
  JOIN carrier ON connection~carrier_id = carrier~carrier_id
```

La asociación hace el join automáticamente.

#### Alias de Campos

En la CDS view `/DMO/I_Connection`:
- `airport_from_id` → `DepartureAirport`
- `airport_to_id` → `DestinationAirport`
- `carrier_id` → `AirlineID`
- `connection_id` → `ConnectionID`

**Usar los nombres de alias** en SELECT:
```abap
WHERE AirlineID = @i_carrier_id  " ✅ Alias de la vista
      carrier_id = @i_carrier_id  " ❌ Nombre de tabla original
```

### Resultado de Ejecución

```
--------------------------------
Carrier:     LH Lufthansa
Connection:  0400
Departure:   FRA
Destination: JFK
--------------------------------
Carrier:     AA American Airlines
Connection:  0017
Departure:   JFK
Destination: SFO
```

---

# Unit 5: Working with Structured Data Objects

## Solution 14: Use a Structured Data Object

**Objetivo**: Usar una estructura (structure) en lugar de atributos individuales para agrupar datos relacionados.

**Template**: `/LRN/CL_S4D400_DBS_CDS`  
**Solución**: `/LRN/CL_S4D400_STS_STRUCTURE` (o continuar con la clase anterior)

### Código Completo

#### Local Class - Definition
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    CLASS-DATA conn_counter TYPE i READ-ONLY.
    
    METHODS constructor
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
    
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PRIVATE SECTION.
    " Definir tipo de estructura
    TYPES:
      BEGIN OF st_details,
        DepartureAirport   TYPE /dmo/airport_from_id,
        DestinationAirport TYPE /dmo/airport_to_id,
        AirlineName        TYPE /dmo/carrier_name,
      END OF st_details.
    
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    
    " Atributo estructurado (reemplaza 3 atributos individuales)
    DATA details TYPE st_details.
    
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD constructor.
    
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    me->carrier_id    = i_carrier_id.
    me->connection_id = i_connection_id.
    
    " SELECT directo a la estructura
    SELECT SINGLE
      FROM /DMO/I_Connection
      FIELDS DepartureAirport,
             DestinationAirport,
             \_Airline-Name AS AirlineName  " Alias requerido
      WHERE AirlineID    = @i_carrier_id
        AND ConnectionID = @i_connection_id
      INTO CORRESPONDING FIELDS OF @details.
    
    IF sy-subrc <> 0.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    conn_counter = conn_counter + 1.
    
  ENDMETHOD.

  METHOD get_output.
    
    APPEND |--------------------------------| TO r_output.
    APPEND |Carrier:     { carrier_id } { details-airlinename }| TO r_output.
    APPEND |Connection:  { connection_id }| TO r_output.
    APPEND |Departure:   { details-departureairport }| TO r_output.
    APPEND |Destination: { details-destinationairport }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Estructura (Structure Type)

```abap
TYPES:
  BEGIN OF st_details,
    DepartureAirport   TYPE /dmo/airport_from_id,
    DestinationAirport TYPE /dmo/airport_to_id,
    AirlineName        TYPE /dmo/carrier_name,
  END OF st_details.
```

**Definición**:
- `BEGIN OF nombre` ... `END OF nombre`: Define una estructura
- Lista de componentes (campos) con sus tipos
- Similar a un `struct` en C o una clase simple en otros lenguajes

**Ventajas**:
- Agrupa datos relacionados lógicamente
- Menos atributos en la clase (1 estructura vs N campos)
- Más fácil de pasar como parámetro

#### Acceso a Componentes de Estructura

```abap
details-departureairport
details-destinationairport
details-airlinename
```

- Operador `-`: Acceso a componentes de estructura
- Nombres case-insensitive en ABAP

#### INTO CORRESPONDING FIELDS OF

```abap
INTO CORRESPONDING FIELDS OF @details
```

**Funcionalidad**:
- Mapea campos por **nombre** (no por posición)
- Solo asigna campos con nombres coincidentes
- Ignora campos extra en la SELECT o en la estructura

**Ventaja**:
- No importa el orden de los campos
- Más flexible que `INTO ( @campo1, @campo2 )`

**Requiere alias** si los nombres no coinciden:
```abap
\_Airline-Name AS AirlineName  " ✅ Nombre coincide con componente
```

#### Comparación: Antes vs Después

**ANTES (atributos individuales)**:
```abap
DATA airport_from_id TYPE /dmo/airport_from_id.
DATA airport_to_id   TYPE /dmo/airport_to_id.
DATA carrier_name    TYPE /dmo/carrier_name.

SELECT ... INTO ( @airport_from_id, @airport_to_id, @carrier_name ).
```

**DESPUÉS (estructura)**:
```abap
DATA details TYPE st_details.

SELECT ... INTO CORRESPONDING FIELDS OF @details.
```

Más conciso y mantenible.

---

# Unit 6: Working with Complex Internal Tables

## Solution 15: Use a Complex Internal Table

**Objetivo**: Usar internal tables con tipos complejos, llenarlas con SELECT, y acceder a sus datos usando table expressions.

**Template**: `/LRN/CL_S4D400_STS_STRUCTURE`  
**Solución**: `/LRN/CL_S4D400_ITS_ITAB` (o continuar con la clase anterior)

### Código Completo

#### Local Class - Definition
```abap
CLASS lcl_connection DEFINITION.

  PUBLIC SECTION.
    CLASS-DATA conn_counter TYPE i READ-ONLY.
    
    " Constructor de clase (static)
    CLASS-METHODS class_constructor.
    
    METHODS constructor
      IMPORTING
        i_carrier_id    TYPE /dmo/carrier_id
        i_connection_id TYPE /dmo/connection_id
      RAISING
        cx_abap_invalid_value.
    
    METHODS get_output
      RETURNING VALUE(r_output) TYPE string_table.
    
  PRIVATE SECTION.
    " Tipo de estructura para aeropuertos
    TYPES:
      BEGIN OF st_airport,
        AirportID TYPE /dmo/airport_id,
        Name      TYPE /dmo/airport_name,
      END OF st_airport.
    
    " Tipo de tabla interna
    TYPES tt_airports TYPE STANDARD TABLE OF st_airport
                      WITH NON-UNIQUE DEFAULT KEY.
    
    " Estructura de detalles (de ejercicio anterior)
    TYPES:
      BEGIN OF st_details,
        DepartureAirport   TYPE /dmo/airport_from_id,
        DestinationAirport TYPE /dmo/airport_to_id,
        AirlineName        TYPE /dmo/carrier_name,
      END OF st_details.
    
    DATA carrier_id    TYPE /dmo/carrier_id.
    DATA connection_id TYPE /dmo/connection_id.
    DATA details       TYPE st_details.
    
    " Tabla estática de aeropuertos (compartida por todas las instancias)
    CLASS-DATA airports TYPE tt_airports.
    
ENDCLASS.
```

#### Local Class - Implementation
```abap
CLASS lcl_connection IMPLEMENTATION.

  METHOD class_constructor.
    
    " Leer TODOS los aeropuertos una sola vez
    SELECT FROM /DMO/I_Airport
      FIELDS AirportID, Name
      INTO TABLE @airports.
    
  ENDMETHOD.

  METHOD constructor.
    
    IF i_carrier_id IS INITIAL OR i_connection_id IS INITIAL.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    me->carrier_id    = i_carrier_id.
    me->connection_id = i_connection_id.
    
    SELECT SINGLE
      FROM /DMO/I_Connection
      FIELDS DepartureAirport,
             DestinationAirport,
             \_Airline-Name AS AirlineName
      WHERE AirlineID    = @i_carrier_id
        AND ConnectionID = @i_connection_id
      INTO CORRESPONDING FIELDS OF @details.
    
    IF sy-subrc <> 0.
      RAISE EXCEPTION TYPE cx_abap_invalid_value.
    ENDIF.
    
    conn_counter = conn_counter + 1.
    
  ENDMETHOD.

  METHOD get_output.
    
    " Buscar nombres de aeropuertos en la tabla estática
    DATA(departure)   = airports[ airportid = details-departureairport ]-name.
    DATA(destination) = airports[ airportid = details-destinationairport ]-name.
    
    " Alternativa: Table expressions directas en string templates
    " APPEND |Departure:   { details-departureairport } { airports[ airportid = details-departureairport ]-name }| TO r_output.
    
    APPEND |--------------------------------| TO r_output.
    APPEND |Carrier:     { carrier_id } { details-airlinename }| TO r_output.
    APPEND |Connection:  { connection_id }| TO r_output.
    APPEND |Departure:   { details-departureairport } { departure }| TO r_output.
    APPEND |Destination: { details-destinationairport } { destination }| TO r_output.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Constructor de Clase (Class Constructor)

```abap
CLASS-METHODS class_constructor.

METHOD class_constructor.
  " Código de inicialización
ENDMETHOD.
```

**Características**:
- Nombre especial: `class_constructor`
- Se ejecuta **una sola vez** cuando la clase se carga
- Antes de crear cualquier instancia
- Usado para inicializar atributos estáticos

**Diferencia con constructor de instancia**:
- `constructor`: Se ejecuta cada vez que se crea una instancia
- `class_constructor`: Se ejecuta una sola vez al cargar la clase

#### SELECT INTO TABLE

```abap
SELECT FROM /DMO/I_Airport
  FIELDS AirportID, Name
  INTO TABLE @airports.
```

**Funcionalidad**:
- Lee **múltiples registros** (no SINGLE)
- Llena una **internal table** completa
- Borra contenido previo de la tabla

**Ventaja**:
- Leer todos los datos de una vez (eficiente)
- Datos disponibles en memoria para acceso rápido

#### Table Expressions

```abap
airports[ airportid = details-departureairport ]
```

**Sintaxis**:
- `tabla[ condicion ]`: Busca la primera línea que cumple la condición
- Retorna la **línea completa** (como estructura)

**Acceso a componente**:
```abap
airports[ airportid = 'FRA' ]-name
```
- `-name`: Accede al componente `name` de la línea encontrada

**¿Qué pasa si no encuentra?**
- Lanza **excepción** `CX_SY_ITAB_LINE_NOT_FOUND`
- Debe manejarse con TRY-CATCH o estar seguro de que existe

#### Declaración Inline con Table Expression

```abap
DATA(departure) = airports[ airportid = details-departureairport ]-name.
```

- `DATA(departure)`: Declaración inline
- Tipo inferido: `TYPE /dmo/airport_name` (tipo del componente `-name`)

### Resultado de Ejecución

```
--------------------------------
Carrier:     LH Lufthansa
Connection:  0400
Departure:   FRA Frankfurt
Destination: JFK John F. Kennedy Intl
--------------------------------
Carrier:     AA American Airlines
Connection:  0017
Departure:   JFK John F. Kennedy Intl
Destination: SFO San Francisco Intl
```

---

# Unit 7: Implementing Database Updates Using Business Objects

## Solution 16: Analyze a Business Object

**Objetivo**: Analizar la estructura de un Business Object (BO) completo: interface, behavior, CDS views e implementación.

Este ejercicio es **analítico** - no se escribe código, solo se navega y analiza.

### Estructura de un Business Object

```
Business Object Interface: /DMO/I_AgencyTP
├─ Behavior Definition (Interface)
│  ├─ use create;
│  ├─ use update;
│  ├─ use delete;
│  └─ use action (draft actions)
│
├─ CDS View (Projection): /DMO/I_AgencyTP
│  └─ Proyección sobre: /DMO/R_AgencyTP
│
└─ Business Object Implementation: /DMO/R_AgencyTP
   ├─ Behavior Definition
   │  ├─ managed implementation in class
   │  ├─ field (readonly) AgencyID;
   │  └─ validation validateName;
   │
   ├─ CDS View: /DMO/R_AgencyTP
   │  └─ Lee desde: /DMO/I_Agency
   │
   └─ Behavior Implementation: /DMO/BP_R_AGENCYTP
      └─ Local Class: lhc_agency
         ├─ Validations
         └─ Authorization checks
```

### Conceptos Clave

#### Business Object (BO)

**Definición**:
- Entidad de negocio con datos + comportamiento
- Encapsula lógica de validación y persistencia
- Expuesto vía servicios (OData, etc.)

**Capas**:
1. **Interface** (estable, versionada): `/DMO/I_AgencyTP`
2. **Implementation** (puede cambiar): `/DMO/R_AgencyTP`
3. **Projection** (vista específica): Según consumidor

#### Behavior Definition

**Interface Behavior**:
```abap
define behavior for /DMO/I_AgencyTP alias /DMO/Agency
interface;
use create;
use update;
use delete;
```

- `interface;`: Es una interfaz (no la implementación)
- `use create/update/delete;`: Operaciones expuestas
- `extensible`: Permite extensiones

**Implementation Behavior**:
```abap
managed implementation in class /dmo/bp_r_agencytp unique;

field (readonly) AgencyID;

validation validateName on save { create; field Name; }
```

- `managed`: Framework maneja create/update/delete automáticamente
- `implementation in class`: Clase que contiene lógica custom
- `field (readonly)`: Campo no modificable
- `validation`: Verificación de consistencia

#### Validations

```abap
validation validateName on save { create; field Name; }
```

**Cuándo se ejecuta**:
- `on save`: Antes de guardar en BD
- `{ create; }`: Siempre en operación CREATE
- `{ field Name; }`: Solo en UPDATE si cambió el campo Name

**Implementación**:
- Método en behavior implementation class
- Verifica reglas de negocio
- Puede rechazar operación con mensaje de error

#### Behavior Implementation Class

**Estructura**:
```abap
CLASS /dmo/bp_r_agencytp DEFINITION.
  " Vacía - solo wrapper
ENDCLASS.

CLASS /dmo/bp_r_agencytp IMPLEMENTATION.
  " Vacía
ENDCLASS.

" Toda la lógica está en clase local
CLASS lhc_agency DEFINITION.
  PRIVATE SECTION.
    METHODS validatename FOR VALIDATE ON SAVE
      IMPORTING keys FOR /dmo/agency~validatename.
ENDCLASS.
```

- **Behavior Pool**: Global class wrapper
- **Local Class**: Contiene la implementación real
- Patrón estándar RAP (ABAP RESTful Programming Model)

---

## Solution 17: Modify Data Using EML

**Objetivo**: Usar EML (Entity Manipulation Language) para modificar datos de un Business Object.

**Solución**: `/LRN/CL_S4D400_BOS_EML`  
**Clase**: `ZCL_##_EML`

### Código Completo

```abap
CLASS zcl_##_eml DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    
ENDCLASS.



CLASS zcl_##_eml IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Declarations
    "**************************
    DATA agencies_upd TYPE TABLE FOR UPDATE /dmo/i_agencytp.
    
    " Preparar datos a modificar
    "**************************
    agencies_upd = VALUE #(
      ( agencyid = '070099'
        name     = 'Updated Travel Agency Name' )
    ).
    
    " Ejecutar operación EML
    "**************************
    MODIFY ENTITIES OF /dmo/i_agencytp
      ENTITY /dmo/agency
        UPDATE FIELDS ( name )
        WITH agencies_upd.
    
    " Confirmar cambios en BD
    "**************************
    COMMIT ENTITIES.
    
    " Output
    "**************************
    out->write( 'Method execution finished!' ).
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### EML (Entity Manipulation Language)

**¿Qué es?**
- Lenguaje específico para modificar Business Objects
- Reemplaza SQL directo (INSERT/UPDATE/DELETE)
- Respeta validaciones y lógica de negocio del BO

**Ventajas**:
- Validaciones automáticas
- Triggers de negocio ejecutados
- Transacciones manejadas correctamente
- Draft handling incluido

#### Derived Table Types

```abap
DATA agencies_upd TYPE TABLE FOR UPDATE /dmo/i_agencytp.
```

**Tipos derivados**:
- `TABLE FOR UPDATE`: Para operaciones MODIFY/UPDATE
- `TABLE FOR CREATE`: Para operaciones CREATE
- `TABLE FOR DELETE`: Para operaciones DELETE

El tipo se deriva automáticamente del BO.

#### VALUE Constructor

```abap
agencies_upd = VALUE #(
  ( agencyid = '070099'
    name     = 'Updated Name' )
).
```

- Llena la tabla con una línea
- Sintaxis compacta
- `#`: Tipo inferido de la variable

#### MODIFY ENTITIES Statement

```abap
MODIFY ENTITIES OF /dmo/i_agencytp
  ENTITY /dmo/agency
    UPDATE FIELDS ( name )
    WITH agencies_upd.
```

**Componentes**:
- `MODIFY ENTITIES OF`: Inicio del statement EML
- `/dmo/i_agencytp`: Business Object (interface)
- `ENTITY /dmo/agency`: Alias de la entidad
- `UPDATE FIELDS ( name )`: Solo actualizar campo `name`
- `WITH agencies_upd`: Datos fuente

**Operaciones disponibles**:
- `CREATE`
- `UPDATE`
- `DELETE`
- `EXECUTE` (para actions)

#### COMMIT ENTITIES

```abap
COMMIT ENTITIES.
```

**Funcionalidad**:
- Confirma los cambios en base de datos
- Similar a `COMMIT WORK` pero para BOs
- **Sin COMMIT, los cambios NO se guardan**

**Flujo**:
1. `MODIFY ENTITIES`: Cambios en buffer transaccional
2. `COMMIT ENTITIES`: Persistencia en BD

### Resultado de Ejecución

```
Method execution finished!
```

Los cambios se reflejan en la tabla `/DMO/A_AGENCY`.

---

# Unit 8: Describing the ABAP RESTful Application Programming Model

## Solution 18: Copy a Database Table

**Objetivo**: Preparar infraestructura para crear un OData UI Service: crear subpackage, copiar tabla, llenarla con datos.

**Template**: `/LRN/S4D400_APT` (tabla), `/LRN/CL_S4D400_APT_COPY` (clase)  
**Solución**: `Z##FLIGHT` (tabla), `ZCL_##_COPY` (clase)

### Pasos Principales

1. **Crear Subpackage**: `ZS4D400_##_RAP`
   - Superpackage: `ZS4D400_##`
   - Descripción: "Objects for OData UI Service"
   - Tipo: Development

2. **Copiar Tabla**: `/LRN/S4D400_APT` → `Z##FLIGHT`
   - En el subpackage `ZS4D400_##_RAP`
   - Activar la tabla

3. **Llenar con Datos**:
   - Copiar clase `/LRN/CL_S4D400_APT_COPY` → `ZCL_##_COPY`
   - Cambiar constante `table_name` al nombre de tu tabla
   - Ejecutar clase (F9)

### Código de la Clase de Copia

```abap
CLASS zcl_##_copy DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
ENDCLASS.



CLASS zcl_##_copy IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
    
    " Cambiar al nombre de tu tabla
    CONSTANTS table_name TYPE tabname VALUE 'Z##FLIGHT'.
    
    " Copiar datos desde tabla template
    SELECT FROM /lrn/s4d400_apt
      FIELDS *
      INTO TABLE @DATA(flights).
    
    " Insertar en tu tabla
    INSERT z##flight FROM TABLE @flights.
    
    " Output
    IF sy-subrc = 0.
      out->write( |{ table_name } was filled with data| ).
    ELSE.
      out->write( |{ table_name } is not a table of the right type| ).
    ENDIF.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Subpackage

**Jerarquía de packages**:
```
ZS4D400_##           (Package principal)
└─ ZS4D400_##_RAP    (Subpackage para RAP)
   ├─ Database Tables
   ├─ CDS Views
   ├─ Behavior Definitions
   └─ Service Bindings
```

**Ventajas**:
- Organización lógica
- Separación por funcionalidad
- Transporte conjunto

#### INSERT con Internal Table

```abap
INSERT z##flight FROM TABLE @flights.
```

- Inserta múltiples registros de una vez
- Más eficiente que loops con INSERT individual
- `sy-subrc`: 0 si exitoso, 4 si algunos fallaron

---

## Solution 19: Generate and Preview an OData UI Service

**Objetivo**: Usar el generador RAP para crear automáticamente todos los objetos de un OData UI Service.

**Objetos Generados**:

| Objeto | Nombre | Descripción |
|--------|--------|-------------|
| CDS Entity (model) | `ZR_##Flight` | Vista de datos (R = Restricted) |
| Behavior Definition (model) | `ZR_##FLIGHT` | Comportamiento del BO |
| Behavior Implementation | `ZBP_R_##FLIGHT` | Lógica del BO |
| Draft Table | `Z##FLIGHT_D` | Tabla para borradores |
| CDS Entity (projection) | `ZC_##Flight` | Proyección consumidor (C = Consumption) |
| Behavior Projection | `ZC_##FLIGHT` | Comportamiento proyectado |
| Service Definition | `ZUI_##FLIGHT_O4` | Definición del servicio |
| Service Binding | `ZUI_##FLIGHT_O4` | Binding OData V4 UI |

### Pasos del Generador

1. **Iniciar Generador**:
   - Click derecho en tabla `Z##FLIGHT`
   - "Generate ABAP Repository Object..."
   - Seleccionar: "ABAP RESTful Application Programming Model → OData UI Service"

2. **Configurar Nombres**:
   - Data Model Name: `ZR_##Flight`, Alias: `Flight`
   - Behavior Implementation: `ZBP_R_##FLIGHT`
   - Draft Table: `Z##FLIGHT_D`
   - Service Projection: `ZC_##Flight`
   - Service Projection Behavior: `ZBP_C_##FLIGHT`
   - Service Definition: `ZUI_##FLIGHT_O4`
   - Service Binding: `ZUI_##FLIGHT_O4`, Type: OData V4 - UI

3. **Generar**: Next → Finish

4. **Publicar Servicio**:
   - Abrir Service Binding
   - Botón "Publish"

5. **Preview**:
   - Seleccionar entidad "Flight"
   - Botón "Preview..."
   - Abre Fiori app en navegador

### Conceptos Clave

#### RAP Generator

**Funcionalidad**:
- Genera automáticamente estructura completa de un BO
- Basado en tabla de base de datos
- Incluye CRUD completo (Create, Read, Update, Delete)
- Draft-enabled por defecto

**Ventajas**:
- Ahorra tiempo (crea 8+ objetos automáticamente)
- Estructura consistente
- Mejores prácticas aplicadas

#### Draft Handling

**¿Qué es?**
- Versiones intermedias de datos no guardados
- Permite trabajar sin afectar datos activos
- Botones "Edit" / "Save" / "Cancel" automáticos

**Draft Table**:
- Tabla separada para borradores
- Nombre: `tabla_original_D`
- Estructura idéntica a tabla activa

#### Naming Conventions RAP

- **ZR_**: Restricted Use (modelo interno)
- **ZC_**: Consumption (proyección para consumidor)
- **ZBP_**: Behavior Pool (implementación)
- **ZUI_**: User Interface (servicio)

### Resultados del Preview

**List Page (Pantalla de lista)**:
- Botones: Create, Delete, Settings, Export
- Filtros configurables
- Paginación automática

**Object Page (Detalle)**:
- Botones: Edit, Delete, Share
- Campos agrupados
- Navegación breadcrumb

**Edit Mode**:
- Campos editables según behavior
- Key fields: Read-only
- Validaciones técnicas automáticas

---

## Solution 20: Validate Price and Currency

**Objetivo**: Implementar validaciones custom en el Business Object para precio positivo y código de moneda válido.

### Código Completo

#### Behavior Definition: `ZR_##FLIGHT`
```abap
managed implementation in class zbp_r_##flight unique;
strict ( 2 );

define behavior for ZR_##FLIGHT alias Flight
persistent table z##flight
draft table z##flight_d
lock master
authorization master ( instance )
{
  create;
  update;
  delete;

  " Validaciones
  validation validatePrice on save { create; field Price; }
  validation validateCurrencyCode on save { create; field CurrencyCode; }

  mapping for z##flight
  {
    CarrierID = carrier_id;
    ConnectionID = connection_id;
    FlightDate = flight_date;
    Price = price;
    CurrencyCode = currency_code;
    PlaneTypeID = plane_type_id;
  }
}
```

#### Behavior Implementation: Class `ZBP_R_##FLIGHT` - Local Types

```abap
CLASS lhc_flight DEFINITION INHERITING FROM cl_abap_behavior_handler.

  PRIVATE SECTION.
    METHODS validateprice FOR VALIDATE ON SAVE
      IMPORTING keys FOR flight~validateprice.

    METHODS validatecurrencycode FOR VALIDATE ON SAVE
      IMPORTING keys FOR flight~validatecurrencycode.

ENDCLASS.



CLASS lhc_flight IMPLEMENTATION.

  METHOD validateprice.
    
    " Estructuras para reportar errores
    DATA failed_record   LIKE LINE OF failed-flight.
    DATA reported_record LIKE LINE OF reported-flight.
    
    " Leer datos a validar desde buffer transaccional
    READ ENTITIES OF zr_##flight IN LOCAL MODE
      ENTITY flight
        FIELDS ( price )
        WITH CORRESPONDING #( keys )
      RESULT DATA(flights).
    
    " Validar cada registro
    LOOP AT flights INTO DATA(flight).
      
      IF flight-price <= 0.
        
        " Marcar como fallido
        failed_record-%tky = flight-%tky.
        APPEND failed_record TO failed-flight.
        
        " Reportar mensaje de error
        reported_record-%tky = flight-%tky.
        reported_record-%msg = new_message(
          id       = '/LRN/S4D400'
          number   = '101'
          severity = if_abap_behv_message=>severity-error
        ).
        APPEND reported_record TO reported-flight.
        
      ENDIF.
      
    ENDLOOP.
    
  ENDMETHOD.

  METHOD validatecurrencycode.
    
    DATA failed_record   LIKE LINE OF failed-flight.
    DATA reported_record LIKE LINE OF reported-flight.
    DATA exists TYPE abap_bool.
    
    " Leer datos a validar
    READ ENTITIES OF zr_##flight IN LOCAL MODE
      ENTITY flight
        FIELDS ( currencycode )
        WITH CORRESPONDING #( keys )
      RESULT DATA(flights).
    
    " Validar cada registro
    LOOP AT flights INTO DATA(flight).
      
      " Verificar si código de moneda existe
      exists = abap_false.
      
      SELECT SINGLE
        FROM i_currency
        FIELDS @abap_true
        WHERE currency = @flight-currencycode
        INTO @exists.
      
      IF exists = abap_false.
        
        " Marcar como fallido
        failed_record-%tky = flight-%tky.
        APPEND failed_record TO failed-flight.
        
        " Reportar mensaje de error
        reported_record-%tky = flight-%tky.
        reported_record-%msg = new_message(
          id       = '/LRN/S4D400'
          number   = '102'
          severity = if_abap_behv_message=>severity-error
          v1       = flight-currencycode
        ).
        APPEND reported_record TO reported-flight.
        
      ENDIF.
      
    ENDLOOP.
    
  ENDMETHOD.
  
ENDCLASS.
```

### Conceptos Clave

#### Validation Signature

```abap
METHODS validateprice FOR VALIDATE ON SAVE
  IMPORTING keys FOR flight~validateprice.
```

**Parámetros implícitos** (no se declaran):
- `failed`: Tabla para marcar entidades fallidas
- `reported`: Tabla para mensajes de error
- `keys`: Entidades a validar

#### READ ENTITIES

```abap
READ ENTITIES OF zr_##flight IN LOCAL MODE
  ENTITY flight
    FIELDS ( price )
    WITH CORRESPONDING #( keys )
  RESULT DATA(flights).
```

**Funcionalidad**:
- Lee datos del **buffer transaccional** (no de BD)
- `IN LOCAL MODE`: Sin verificaciones de autorización
- `FIELDS ( price )`: Solo campos necesarios
- `WITH CORRESPONDING #( keys )`: Entidades a leer
- `RESULT`: Tabla con los datos

#### Failed y Reported

**failed-flight**:
```abap
failed_record-%tky = flight-%tky.
APPEND failed_record TO failed-flight.
```
- Marca la entidad como fallida
- Operación no se ejecutará
- `%tky`: Transactional Key (incluye key fields + draft info)

**reported-flight**:
```abap
reported_record-%tky = flight-%tky.
reported_record-%msg = new_message( ... ).
APPEND reported_record TO reported-flight.
```
- Mensaje de error para el usuario
- Se muestra en la UI
- Puede incluir placeholders (`v1`, `v2`, etc.)

#### Message Class

```abap
new_message(
  id       = '/LRN/S4D400'
  number   = '101'
  severity = if_abap_behv_message=>severity-error
)
```

**Componentes**:
- `id`: Message class (tabla T100)
- `number`: Número de mensaje
- `severity`: error / warning / info / success
- `v1`, `v2`, `v3`, `v4`: Placeholders en el mensaje

### Resultado en UI

**Validación fallida**:
- Botón "Save" deshabilitado
- Mensaje de error mostrado
- Campo marcado en rojo
- Cambios no se guardan

---

## Solution 21: Adjust the User Interface

**Objetivo**: Personalizar la UI del Fiori app modificando behavior projection y metadata extension.

### Código Completo

#### Behavior Projection: `ZC_##FLIGHT`
```abap
projection;
strict ( 2 );

define behavior for ZC_##FLIGHT alias Flight
{
  // use create;  " Comentado - sin botón Create
  use update;
  // use delete;  " Comentado - sin botón Delete

  field ( readonly ) PlaneTypeID;
}
```

#### Metadata Extension: `ZC_##FLIGHT`
```abap
@Metadata.layer: #CORE

@UI: {
  headerInfo: {
    typeName: 'Flight',
    typeNamePlural: 'Flights'
  }
}

annotate view ZC_##FLIGHT with
{
  @UI.facet: [
    {
      id: 'Flight',
      purpose: #STANDARD,
      type: #IDENTIFICATION_REFERENCE,
      label: 'Flight',
      position: 10
    }
  ]

  " Selection fields (filtros en list page)
  @UI.selectionField: [{ position: 10 }]
  CarrierID;

  @UI.selectionField: [{ position: 20 }]
  ConnectionID;

  " Campos en object page
  @UI.lineItem: [{ position: 10 }]
  @UI.identification: [{ position: 10 }]
  CarrierID;

  @UI.lineItem: [{ position: 20 }]
  @UI.identification: [{ position: 20 }]
  ConnectionID;

  @UI.lineItem: [{ position: 30 }]
  @UI.identification: [{ position: 30 }]
  FlightDate;

  @UI.lineItem: [{ position: 40 }]
  @UI.identification: [{ position: 40 }]
  PlaneTypeID;

  @UI.lineItem: [{ position: 50 }]
  @UI.identification: [{ position: 50 }]
  Price;

  @UI.lineItem: [{ position: 60 }]
  @UI.identification: [{ position: 60 }]
  CurrencyCode;

  " Campos ocultos
  @UI.hidden: true
  LocalCreatedBy;

  @UI.hidden: true
  LocalCreatedAt;

  @UI.hidden: true
  LocalLastChangedBy;

  @UI.hidden: true
  LocalLastChangedAt;

  @UI.hidden: true
  LastChangedAt;
}
```

#### Projection View: `ZC_##FLIGHT` (Value Help)
```abap
@AccessControl.authorizationCheck: #CHECK
@EndUserText.label: 'Projection View for Flight'

define root view entity ZC_##FLIGHT
  as projection on ZR_##FLIGHT
{
  key CarrierID,
  key ConnectionID,
  key FlightDate,
      @Consumption.valueHelpDefinition: [{
        entity: { name: 'I_CurrencyStdVH', element: 'Currency' }
      }]
      CurrencyCode,
      PlaneTypeID,
      Price,
      LocalCreatedBy,
      LocalCreatedAt,
      LocalLastChangedBy,
      LocalLastChangedAt,
      LastChangedAt
}
```

### Conceptos Clave

#### Behavior Projection vs Behavior Definition

**Behavior Definition** (ZR_##FLIGHT):
```abap
create;
update;
delete;
```
- Define capacidades del BO
- Todas las operaciones disponibles

**Behavior Projection** (ZC_##FLIGHT):
```abap
// use create;  " Deshabilitado
use update;
// use delete;  " Deshabilitado
```
- Restringe operaciones para un consumidor
- Subset del behavior definition

**Resultado**:
- BO sigue soportando create/delete internamente
- UI específica no expone esos botones

#### UI Annotations

**@UI.selectionField**:
```abap
@UI.selectionField: [{ position: 10 }]
CarrierID;
```
- Campo de filtro en list page
- Posición determina orden

**@UI.lineItem**:
```abap
@UI.lineItem: [{ position: 10 }]
```
- Columna en tabla de list page

**@UI.identification**:
```abap
@UI.identification: [{ position: 10 }]
```
- Campo en object page (detalle)
- Posición determina orden vertical

**@UI.hidden**:
```abap
@UI.hidden: true
LocalCreatedBy;
```
- Campo no visible en UI
- Datos siguen en el backend

#### Value Help

```abap
@Consumption.valueHelpDefinition: [{
  entity: { name: 'I_CurrencyStdVH', element: 'Currency' }
}]
CurrencyCode;
```

**Funcionalidad**:
- Dropdown/Search Help en campo
- Lista de valores válidos
- `I_CurrencyStdVH`: CDS view estándar
- `Currency`: Campo key de la vista

**Resultado en UI**:
- Ícono F4 junto al campo
- Click abre popup con búsqueda
- Selección de valor válido

### Resultado Final

**List Page**:
- Sin botón "Create"
- Sin botón "Delete"
- 2 filtros: CarrierID, ConnectionID
- Columnas ordenadas

**Object Page**:
- Sin botón "Delete"
- Campos en orden: Carrier → Connection → Date → **Plane** → Price → Currency
- PlaneTypeID read-only en edit mode
- Currency con value help (F4)
- Campos administrativos ocultos

---

## 📝 Notas Finales del Curso

### Shortcuts de Eclipse (Resumen)

| Acción | Shortcut | Descripción |
|--------|----------|-------------|
| Activar | `Ctrl + F3` | Activa objeto ABAP |
| Ejecutar | `F9` | Ejecuta como console app |
| Abrir objeto | `Ctrl + Shift + A` | Abre desarrollo ABAP |
| Quick fix | `Ctrl + 1` | Sugerencias de corrección |
| Code completion | `Ctrl + Space` | Autocompletado |
| Firma completa | `Shift + Enter` | Inserta parámetros |
| Comentar/Descomentar | `Ctrl + <` / `Ctrl + Shift + <` | Agrega/quita `*` |
| Navegar a definición | `F3` | Va a definición |
| Tooltip | `F2` | Muestra descripción |
| Breakpoint | `Ctrl + Shift + B` | Toggle breakpoint |
| Step Into | `F5` | Debugger: entra en método |
| Step Over | `F6` | Debugger: ejecuta línea |
| Resume | `F8` | Debugger: continua |

### Convenciones de Nombres

- `##`: Tu número de grupo (ej: 01, 02, 99)
- **Packages**: `ZS4D400_##`, `ZS4D400_##_RAP`
- **Global Classes**: `ZCL_##_NOMBRE`
- **Local Classes**: `lcl_nombre`
- **CDS Views (Restricted)**: `ZR_##Nombre`
- **CDS Views (Consumption)**: `ZC_##Nombre`
- **Behavior Pools**: `ZBP_R_##NOMBRE`, `ZBP_C_##NOMBRE`
- **Database Tables**: `Z##NOMBRE`
- **Services**: `ZUI_##NOMBRE_O4`

### Recursos de Aprendizaje

- **SAP Help Portal**: help.sap.com
- **SAP Community**: community.sap.com
- **SAP API Business Hub**: api.sap.com
- **ABAP Keyword Documentation**: Accesible con F1 en Eclipse
- **SAP Learning Hub**: learning.sap.com

---

**🎓 Fin del Curso S4D400 - Basic ABAP Programming**

Este documento cubre todos los 21 ejercicios del curso, enfocándose en el código completo y conceptos clave. Para navegación SAP GUI/Eclipse, consultar el material oficial del curso.
