# S4D400 - Unit 4: Ejercicios Prácticos
## Database Reading - Desafío de Análisis e Implementación

> **Modalidad**: Análisis y diseño autónomo  
> **Objetivo**: Desarrollar capacidad analítica y de resolución de problemas  
> **Nivel**: Intermedio-Avanzado - Los estudiantes deben analizar, diseñar e implementar completamente  
> **Tiempo estimado**: 5-6 horas  

---

## 📑 Tabla de Contenidos

- [Instrucciones Generales](#-instrucciones-generales)
- [Formato de Entrega](#-formato-de-entrega)
- [Estándares Obligatorios](#-estándares-obligatorios)
- [Ejercicio 1: Analizador Estadístico de Rutas](#ejercicio-1-analizador-estadístico-de-rutas)
- [Ejercicio 2: Clasificador de Distancias](#ejercicio-2-clasificador-de-distancias)
- [Ejercicio 3: Buscador Multi-Aerolínea](#ejercicio-3-buscador-multi-aerolínea)
- [Ejercicio 4: Generador de Reportes con Información Completa](#ejercicio-4-generador-de-reportes-con-información-completa)

---

## 📋 Instrucciones Generales

### Metodología de Trabajo

1. **Leer la especificación funcional completa** - Entender QUÉ debe hacer
2. **Estudiar el ejemplo de salida en detalle** - Ver el resultado esperado
3. **Analizar el problema** - Identificar qué datos necesitas y cómo procesarlos
4. **Diseñar tu solución** - Planificar en papel antes de codificar
   - ¿Qué SELECT necesito?
   - ¿Qué variables y estructuras necesito?
   - ¿Qué lógica de procesamiento aplicar?
   - ¿Cómo organizar el output?
5. **Implementar paso a paso** - Codificar probando cada componente
6. **Verificar contra el resultado esperado** - Comparar tu output

### Criterios de Evaluación

| Aspecto | Peso |
|---------|------|
| **Funcionalidad correcta** | 40% |
| **Output coincide con ejemplo** | 25% |
| **Estándares de nomenclatura** | 15% |
| **Calidad del código** (legibilidad, comentarios) | 10% |
| **Formato y presentación** | 10% |

### Importante

- ✅ Debes **analizar el problema** y diseñar tu propia solución
- ✅ El **ejemplo de salida** es tu guía principal - ese es el resultado a lograr
- ✅ Las **pistas** están disponibles si te atoras, pero intenta primero resolverlo solo

---

## 📐 Estándares Obligatorios

### Nomenclatura (Cumplimiento Estricto)

**Debes seguir estas convenciones en tu código:**

```
Variables locales:     lv_*    (ejemplo: lv_total_distance, lv_count)
Estructuras locales:   ls_*    (ejemplo: ls_connection, ls_detail)
Tablas locales:        lt_*    (ejemplo: lt_connections, lt_results)
Objetos:               lo_*    (ejemplo: lo_processor, lo_analyzer)
Parámetros IMPORTING:  iv_*, is_*, it_*
Parámetros RETURNING:  rv_*, rs_*, rt_*
Tipos personalizados:  ty_*    (ejemplo: ty_route_details)
Clases locales:        lcl_*   (ejemplo: lcl_processor)
```

**Ejemplos de declaraciones correctas:**
```abap
DATA lv_carrier_id TYPE /dmo/carrier_id.
DATA lv_count TYPE i.
DATA ls_connection TYPE /dmo/connection.
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA lo_processor TYPE REF TO lcl_processor.
```

### Estructura General del Programa

**Para cada ejercicio debes crear**:
1. **Clase Global**: Nombre libre (recomendado: `ZCL_##_EXERCISE_N` donde ## = tu número)
   - Debe implementar interface `if_oo_adt_classrun`
   - El método `main` instancia la clase local y llama a su método de procesamiento

2. **Clase Local**: Nombre libre (recomendado: `lcl_exercise_N_processor`)
   - Contiene la lógica principal del ejercicio
   - Puede tener métodos auxiliares PRIVATE si lo consideras necesario
   - Define tipos personalizados si son necesarios (BEGIN OF ... END OF)

### Reglas de Código

**OBLIGATORIO**:
- ❌ **NO usar** declaraciones inline: `DATA(variable) = valor`
- ✅ **Declarar** todas las variables explícitamente: `DATA variable TYPE tipo.`
- ✅ **Comentar** secciones importantes en español
- ✅ **Verificar** resultados antes de procesar (IS INITIAL, sy-subrc, lines())
- ✅ **Usar** el objeto `out` para imprimir en consola

**Ejemplo de declaración CORRECTA**:
```abap
" Declarar variables
DATA lt_connections TYPE STANDARD TABLE OF /dmo/connection.
DATA ls_connection TYPE /dmo/connection.
DATA lv_count TYPE i.

" Inicializar
lv_count = 0.

" Usar
SELECT ... INTO TABLE @lt_connections.
LOOP AT lt_connections INTO ls_connection.
  lv_count = lv_count + 1.
ENDLOOP.
```

**Ejemplo de declaración INCORRECTA (no hacer esto)**:
```abap
" ❌ NO USAR INLINE
SELECT ... INTO TABLE @DATA(lt_connections).
LOOP AT lt_connections INTO DATA(ls_connection).
  DATA(lv_count) = lv_count + 1.  " ❌ MAL
ENDLOOP.
```

---

## 📦 Formato de Entrega

### Qué Entregar

1. **Código fuente** de cada ejercicio:
   - Clase global completa
   - Clase local completa (tab "Local Types")

2. **Screenshots** del output de consola:
   - Un screenshot por cada ejercicio mostrando la ejecución exitosa
   - El output debe coincidir con el ejemplo mostrado

3. **Documento de diseño** (opcional pero recomendado):
   - Explicación de cómo estructuraste la solución
   - Decisiones de diseño tomadas (nombres de clases, métodos, etc.)
   - Desafíos encontrados y cómo los resolviste

### Cómo Verificar tu Solución

**Antes de entregar, verifica que**:
- ✅ El programa **ejecuta sin errores** de sintaxis
- ✅ El output **coincide exactamente** con el ejemplo mostrado
- ✅ La **nomenclatura** sigue los estándares (lv_, lt_, ls_, lo_)
- ✅ **NO usas** declaraciones inline en ninguna parte
- ✅ El código está **comentado** en secciones importantes
- ✅ **Funciona** con diferentes datos de entrada (prueba con varias aerolíneas)

### Criterios de Evaluación

| Aspecto | Descripción | Peso |
|---------|-------------|------|
| **Funcionalidad** | El programa funciona y produce el output esperado | 40% |
| **Output correcto** | El resultado coincide exactamente con el ejemplo | 25% |
| **Estándares** | Nomenclatura correcta, no inline, comentarios | 15% |
| **Calidad del código** | Legibilidad, organización, verificaciones | 10% |
| **Diseño** | Estructura de clases y métodos apropiada | 10% |

---

## Ejercicio 1: Analizador Estadístico de Rutas

### 🎯 Objetivo del Ejercicio

Desarrollar un sistema que analice las conexiones de una aerolínea y genere estadísticas básicas, practicando:
- Lectura de múltiples registros con SELECT
- Iteración con LOOP
- Acumulación de valores
- Cálculos matemáticos (suma, promedio)

---

### 📝 Especificación Funcional

**¿Qué debe hacer el programa?**

El programa debe analizar todas las rutas de una aerolínea específica y mostrar en consola:

1. **Encabezado** con el código de la aerolínea
2. **Estadísticas calculadas**:
   - Cantidad total de rutas
   - Distancia total acumulada (suma de todas las distancias)
   - Distancia promedio (total ÷ cantidad)
3. **Listado completo** de todas las rutas encontradas:
   - Numeradas secuencialmente
   - Con código de conexión
   - Aeropuerto origen → Aeropuerto destino
   - Distancia en kilómetros

**Aerolínea a analizar**: 'AA' (American Airlines)

**Tabla a consultar**: `/dmo/connection`

---

### 📺 Ejemplo de Salida en Consola

**Cuando ejecutes tu programa con la aerolínea 'AA', debe verse exactamente así:**

```
=== ANÁLISIS DE RUTAS: AA ===
 
Total de rutas: 2
Distancia total: 8270 KM
Distancia promedio: 4135 KM
 
LISTA DE RUTAS:
----------------------------------------
1. Ruta 0017: JFK → SFO (4135 KM)
2. Ruta 0064: SFO → JFK (4135 KM)
```

**Desglose del output**:
- Línea 1: Encabezado con código de aerolínea
- Línea 2: En blanco
- Línea 3: Total de rutas encontradas
- Línea 4: Suma de todas las distancias
- Línea 5: Promedio calculado (8270 ÷ 2 = 4135)
- Línea 6: En blanco
- Línea 7: Título de sección
- Línea 8: Separador visual
- Líneas 9-10: Cada ruta numerada con formato: `número. Ruta ID: ORIGEN → DESTINO (distancia KM)`

**Casos a considerar**:
- Si la aerolínea no tiene rutas, debe mostrar: `"No se encontraron rutas para esta aerolínea"`
- Si pruebas con 'LH' (Lufthansa) deberías ver 5 rutas
- Si pruebas con 'XX' (no existe) deberías ver mensaje de no encontradas

---

### 💡 Pistas de Implementación

**Pista 1: ¿Qué SELECT usar?**

Necesitas un SELECT que:
- Lea de la tabla `/dmo/connection`
- Filtre por `carrier_id` con WHERE
- Guarde en una tabla interna con INTO TABLE
- Recuerda usar `@` antes de las variables

**Pista 2: ¿Cómo acumular en el LOOP?**

En cada iteración del LOOP debes:
- Incrementar el contador en 1
- Sumar la distancia actual al acumulador
- Usa operaciones: `variable = variable + valor`

**Pista 3: ¿Cómo calcular promedio?**

División simple:
- Asegúrate de que el contador NO sea cero (evitar división por cero)
- `promedio = total / contador`

---

### ✅ Checklist de Verificación

- [ ] Clase global con `if_oo_adt_classrun` implementado
- [ ] Clase local para procesamiento
- [ ] Variables con nomenclatura correcta (lv_, lt_, ls_)
- [ ] SELECT trae datos de la aerolínea correcta
- [ ] Validación implementada si no hay datos
- [ ] LOOP acumula correctamente suma y cuenta
- [ ] Cálculo de promedio correcto (con validación de división por cero)
- [ ] Output formateado exactamente como el ejemplo
- [ ] Funciona correctamente con 'AA', 'LH' y aerolíneas sin rutas

---

## Ejercicio 2: Clasificador de Distancias

### 🎯 Objetivo del Ejercicio

Desarrollar un sistema que clasifique rutas por categorías de distancia, practicando:
- Lógica condicional (IF/ELSEIF/ELSE)
- Creación de métodos auxiliares
- Categorización de datos
- Contadores múltiples

---

### 📝 Especificación Funcional

**¿Qué debe hacer el programa?**

El programa debe leer todas las conexiones de una aerolínea, clasificarlas y mostrar:

1. **Clasificar cada ruta** según su distancia en tres categorías:
   - **Corta**: distancia < 3,000 KM
   - **Media**: distancia ≥ 3,000 y ≤ 7,000 KM
   - **Larga**: distancia > 7,000 KM

2. **Mostrar listado** de rutas con categoría visible

3. **Resumen estadístico** al final:
   - Cantidad de rutas por cada categoría
   - Total general

**Aerolínea a analizar**: 'LH' (Lufthansa)

**Tabla a consultar**: `/dmo/connection`

---

### 📺 Ejemplo de Salida en Consola

**Cuando ejecutes tu programa con la aerolínea 'LH', debe verse exactamente así:**

```
=== CLASIFICADOR DE RUTAS: LH ===
 
RUTAS CLASIFICADAS POR DISTANCIA:
------------------------------------------------
1. 0400: FRA → JFK (6162 KM) [Media]
2. 0401: FRA → SFO (9090 KM) [Larga]
3. 0402: FRA → LAX (9481 KM) [Larga]
4. 2402: FRA → GRU (9883 KM) [Larga]
5. 2403: FRA → EZE (11845 KM) [Larga]
 
================================================
RESUMEN:
  • Rutas cortas (< 3000 KM): 0
  • Rutas medias (3000-7000 KM): 1
  • Rutas largas (> 7000 KM): 4
  • TOTAL: 5
```

**Desglose del output**:
- Líneas 1-3: Encabezado y título de sección
- Línea 4: Separador
- Líneas 5-9: Cada ruta con formato: `número. ID: ORIGEN → DESTINO (distancia KM) [Categoría]`
- Línea 10: En blanco
- Línea 11: Separador de resumen
- Línea 12: Título de resumen
- Líneas 13-16: Contadores por categoría y total

**Cómo se clasifican las rutas**:
- **6162 KM** → Media (está entre 3000 y 7000)
- **9090, 9481, 9883, 11845 KM** → Largas (todas > 7000)
- **0 rutas cortas** porque ninguna es < 3000

**Otros casos de prueba**:
- Con 'AA': deberían salir 2 rutas [Media] (4135 KM cada una)
- Con 'UA': deberían salir rutas [Larga]
- El resumen debe sumar correctamente: cortas + medias + largas = TOTAL

---

### 💡 Pistas de Implementación

**Pista 1: Estructura del método auxiliar**

El método de clasificación debe:
- Recibir la distancia como parámetro
- Usar IF/ELSEIF/ELSE para decidir la categoría
- RETORNAR un string: "Corta", "Media" o "Larga"
- Puede ser un método PRIVATE de la clase local

**Pista 2: ¿Cómo llamar al método auxiliar?**

Dentro del LOOP, antes de mostrar la ruta:
- Llama al método pasando la distancia
- Guarda el resultado en una variable
- Usa esa variable en el mensaje de salida y para incrementar el contador

**Pista 3: ¿Cómo incrementar el contador correcto?**

Después de obtener la categoría:
- Usa IF/ELSEIF o CASE para comparar el texto de la categoría
- Incrementa solo el contador correspondiente
- Asegúrate de que cada contador empiece en 0

---

### ✅ Checklist de Verificación

- [ ] Método auxiliar de clasificación implementado
- [ ] Lógica de clasificación correcta (< 3000, 3000-7000, > 7000)
- [ ] Método auxiliar retorna string con categoría
- [ ] Método auxiliar se llama dentro del LOOP principal
- [ ] Tres contadores independientes (cortas, medias, largas)
- [ ] Cada contador incrementa según categoría correcta
- [ ] Resumen muestra las tres categorías con contadores
- [ ] Total calculado correctamente (suma de los tres)
- [ ] Output formateado exactamente como el ejemplo
- [ ] Funciona con 'LH', 'AA' y otras aerolíneas

---

## Ejercicio 3: Buscador Multi-Aerolínea

### 🎯 Objetivo del Ejercicio

Desarrollar un buscador que trabaje con múltiples aerolíneas simultáneamente, practicando:
- Operador IN en cláusula WHERE
- Creación y llenado de tablas internas manualmente
- Detección de cambio de grupo en iteración
- Subtotales y total general

---

### 📝 Especificación Funcional

**¿Qué debe hacer el programa?**

El programa debe buscar y mostrar conexiones de VARIAS aerolíneas a la vez:

1. **Buscar conexiones** de tres aerolíneas específicas:
   - 'AA' (American Airlines)
   - 'UA' (United Airlines)
   - 'DL' (Delta Airlines)

2. **Agrupar resultados** por aerolínea (todas las rutas de AA juntas, luego todas las de UA, etc.)

3. **Mostrar por cada aerolínea**:
   - Encabezado con código de aerolínea
   - Listado de sus rutas
   - Subtotal de rutas de esa aerolínea

4. **Mostrar total general** de todas las rutas encontradas

**Tablas a consultar**: `/dmo/connection`

**Datos de entrada**: Lista fija de carriers hardcodeada en el programa

---

### 📺 Ejemplo de Salida en Consola

**Cuando ejecutes tu programa, debe verse exactamente así:**

```
=== BUSCADOR MULTI-AEROLÍNEA ===
Aerolíneas: AA, UA, DL
 
--- AEROLÍNEA: AA ---
  0017: JFK → SFO (4135 KM)
  0064: SFO → JFK (4135 KM)
  Total: 2 rutas
 
--- AEROLÍNEA: DL ---
  0106: ATL → FRA (7330 KM)
  0956: ATL → FRA (7330 KM)
  Total: 2 rutas
 
--- AEROLÍNEA: UA ---
  0900: SFO → FRA (9090 KM)
  0941: FRA → SFO (9090 KM)
  Total: 2 rutas
 
================================================
TOTAL GENERAL: 6 rutas
```

**Desglose del output**:
- Líneas 1-2: Encabezado general
- Línea 3: En blanco
- **Bloque AA** (líneas 4-7):
  - Línea 4: Encabezado de aerolínea
  - Líneas 5-6: Rutas de AA (indentadas con espacios)
  - Línea 7: Subtotal de AA
- Línea 8: En blanco (separador entre grupos)
- **Bloque DL** (líneas 9-12): Similar a AA
- Línea 13: En blanco
- **Bloque UA** (líneas 14-17): Similar a AA
- Línea 18: En blanco
- Líneas 19-20: Separador y total general

**Aspectos clave a notar**:
- Las rutas están **agrupadas por aerolínea** (todas las de AA, luego todas las de DL, etc.)
- Cada grupo tiene su **subtotal**
- Las rutas dentro de cada grupo están **indentadas** (empiezan con espacios)
- El orden alfabético de carriers: AA → DL → UA
- Total general: 2 + 2 + 2 = 6

**¿Cómo se logra el agrupamiento?**
- SELECT debe tener `ORDER BY carrier_id, connection_id`
- Esto hace que salgan ordenadas por aerolínea
- En el LOOP detectas cuando cambia el carrier_id
- Al cambiar, muestras subtotal del anterior e inicia nuevo bloque

---

### 💡 Pistas de Implementación

**Pista 1: ¿Cómo llenar la tabla de carriers?**

Necesitas declarar una tabla interna del tipo `/dmo/carrier_id` y llenarla con los códigos de las tres aerolíneas: 'AA', 'UA', 'DL'.

**Pista 2: ¿Cómo funciona el operador IN?**

En el WHERE del SELECT:
- `WHERE carrier_id IN @lt_carrier_ids`
- Busca registros donde carrier_id sea CUALQUIERA de los valores en la tabla
- Es equivalente a: carrier_id = 'AA' OR carrier_id = 'UA' OR carrier_id = 'DL'

**Pista 3: ¿Cómo detectar cambio de aerolínea?**

Algoritmo de detección de cambio de grupo:
1. Inicializa una variable `lv_current_carrier` con valor vacío ''
2. En cada iteración del LOOP, compara `ls_connection-carrier_id` con `lv_current_carrier`
3. Si son diferentes = cambió de grupo:
   - Muestra subtotal del grupo anterior (si no es el primer grupo)
   - Muestra encabezado del nuevo grupo
   - Reinicia contador del grupo a 0
   - Actualiza `lv_current_carrier` con el nuevo valor
4. Incrementa contadores
5. Al final del LOOP, no olvides mostrar subtotal del último grupo

---

### ✅ Checklist de Verificación

- [ ] Tabla de carriers creada (tipo STANDARD TABLE OF /dmo/carrier_id)
- [ ] Los 3 carriers agregados correctamente: 'AA', 'UA', 'DL'
- [ ] SELECT usa operador IN con la tabla de carriers
- [ ] ORDER BY incluye carrier_id y connection_id
- [ ] Variable de "carrier actual" para detectar cambios
- [ ] Lógica de detección de cambio de grupo funciona
- [ ] Muestra encabezado al iniciar cada nuevo grupo
- [ ] Muestra subtotal al terminar cada grupo (excepto el primero)
- [ ] Muestra subtotal del último grupo después del LOOP
- [ ] Contador general acumula todas las rutas
- [ ] Output agrupado correctamente por aerolínea
- [ ] Indentación de rutas con espacios
- [ ] Total general correcto (suma de todos los subtotales)

---

## Ejercicio 4: Generador de Reportes con Información Completa

### 🎯 Objetivo del Ejercicio

Desarrollar un sistema de reportes profesional que combine información de múltiples tablas, practicando:
- INNER JOIN para relacionar tablas
- Uso de alias en SELECT
- Tipos personalizados complejos
- Formateo profesional de reportes

---

### 📝 Especificación Funcional

**¿Qué debe hacer el programa?**

El programa debe generar un **reporte profesional** de rutas que incluya información completa de múltiples tablas:

1. **Encabezado del reporte**:
   - Nombre COMPLETO de la aerolínea (no solo el código)
   - Total de conexiones

2. **Detalle de cada ruta** mostrando:
   - Número de ruta y código de conexión
   - **Aeropuerto de origen COMPLETO**:
     - Código (ej: JFK)
     - Nombre completo del aeropuerto
     - Ciudad
   - **Aeropuerto de destino COMPLETO**:
     - Código (ej: SFO)
     - Nombre completo del aeropuerto
     - Ciudad
   - Distancia en kilómetros

3. **Pie del reporte** con mensaje de finalización

**Aerolínea a reportar**: 'AA' (American Airlines)

**Tablas a consultar**: 
- `/dmo/connection` (datos principales de rutas)
- `/dmo/carrier` (para obtener nombre de aerolínea)
- `/dmo/airport` (para obtener nombres de aeropuertos - SE USA 2 VECES)

**Técnica requerida**: INNER JOIN (combinar 3 tablas en un solo SELECT)

---

### 📺 Ejemplo de Salida en Consola

**Cuando ejecutes tu programa con la aerolínea 'AA', debe verse exactamente así:**

```
╔════════════════════════════════════════════════════╗
║   REPORTE DE RUTAS - American Airlines            ║
║   Total de conexiones: 2                          ║
╚════════════════════════════════════════════════════╝
 
──────────────────────────────────────────────────
RUTA 1: AA-0017
──────────────────────────────────────────────────
  ORIGEN:
    Código: JFK
    Aeropuerto: John F. Kennedy International Airport
    Ciudad: New York
  DESTINO:
    Código: SFO
    Aeropuerto: San Francisco International Airport
    Ciudad: San Francisco
  DISTANCIA: 4135 KM
 
──────────────────────────────────────────────────
RUTA 2: AA-0064
──────────────────────────────────────────────────
  ORIGEN:
    Código: SFO
    Aeropuerto: San Francisco International Airport
    Ciudad: San Francisco
  DESTINO:
    Código: JFK
    Aeropuerto: John F. Kennedy International Airport
    Ciudad: New York
  DISTANCIA: 4135 KM
 
══════════════════════════════════════════════════
                  FIN DEL REPORTE                 
══════════════════════════════════════════════════
```

**Desglose del output**:
- **Encabezado** (líneas 1-4):
  - Borde decorativo con símbolos ║ ╔ ╗ ╚ ╝ ═
  - Nombre COMPLETO de la aerolínea ("American Airlines" NO "AA")
  - Total de conexiones
  
- **Por cada ruta** (ejemplo: líneas 6-18):
  - Separador de sección con guiones
  - Título con número de ruta y código (AA-0017)
  - Separador
  - ORIGEN con 3 líneas indentadas:
    - Código del aeropuerto
    - Nombre completo del aeropuerto
    - Ciudad
  - DESTINO con 3 líneas indentadas:
    - Código del aeropuerto
    - Nombre completo del aeropuerto
    - Ciudad
  - Distancia
  - Línea en blanco separadora

- **Pie del reporte** (líneas 29-31):
  - Borde decorativo doble (═)
  - Mensaje centrado "FIN DEL REPORTE"
  - Borde decorativo doble

**De dónde viene cada dato**:
- `American Airlines` → Tabla `/dmo/carrier` campo `name`
- `JFK` → Tabla `/dmo/connection` campo `airport_from_id`
- `John F. Kennedy International Airport` → Tabla `/dmo/airport` campo `name`
- `New York` → Tabla `/dmo/airport` campo `city`
- `4135` → Tabla `/dmo/connection` campo `distance`

**Desafío clave**: Necesitas datos de 3 tablas diferentes en un solo SELECT usando INNER JOIN

**¿Por qué se usa la misma tabla 2 veces?**
- `/dmo/airport` se usa DOS veces:
  - Una vez para el aeropuerto de origen (airport_from_id)
  - Otra vez para el aeropuerto de destino (airport_to_id)
- Se usan ALIAS diferentes para distinguirlas en el SELECT

---

### 💡 Pistas de Implementación

**Pista 1: Estructura general del SELECT con INNER JOIN**

El SELECT debe combinar 3 tablas:
```
1. Tabla principal: /dmo/connection (usa alias 'conn')
   
2. JOIN con /dmo/carrier (usa alias 'car')
   Condición: conn.carrier_id = car.carrier_id
   Para obtener: nombre de la aerolínea
   
3. JOIN con /dmo/airport como ORIGEN (usa alias 'apt_from')
   Condición: conn.airport_from_id = apt_from.airport_id
   Para obtener: nombre y ciudad del aeropuerto origen
   
4. JOIN con /dmo/airport como DESTINO (usa alias 'apt_to')
   Condición: conn.airport_to_id = apt_to.airport_id
   Para obtener: nombre y ciudad del aeropuerto destino
```

Estructura básica del SELECT:
```
SELECT
  FROM tabla_principal AS alias1
  INNER JOIN tabla2 AS alias2
    ON alias1~campo = alias2~campo
  INNER JOIN tabla3 AS alias3
    ON alias1~campo = alias3~campo
  INNER JOIN tabla3 AS alias4
    ON alias1~campo = alias4~campo
  FIELDS
    alias1~campo1,
    alias2~campo2,
    alias3~campo3,
    ...
  WHERE condición
  INTO ...
```

**Pista 2: ¿Cómo acceder a campos de tablas con alias?**

Cuando usas alias, debes acceder a campos así:
- `conn~carrier_id` (campo carrier_id de tabla connection)
- `car~name` (campo name de tabla carrier)
- `apt_from~name` (campo name de airport origen)
- `apt_to~name` (campo name de airport destino)

Puedes renombrar con AS:
- `car~name AS carrier_name`
- `apt_from~name AS from_name`
- `apt_to~city AS to_city`

**Pista 3: ¿Cómo definir las condiciones ON?**

Cada JOIN necesita una condición ON:

JOIN 1 (carrier):
```
ON conn~carrier_id = car~carrier_id
```

JOIN 2 (airport origen):
```
ON conn~airport_from_id = apt_from~airport_id
```

JOIN 3 (airport destino):
```
ON conn~airport_to_id = apt_to~airport_id
```

El patrón es: `campo_tabla_principal = campo_tabla_a_unir`

**Pista 4: ¿Necesito crear un tipo personalizado?**

Sí, porque el resultado combina campos de varias tablas.
Necesitas un tipo que tenga:
- carrier_id, carrier_name (de connection + carrier)
- connection_id (de connection)
- from_code, from_name, from_city (de connection + airport)
- to_code, to_name, to_city (de connection + airport)
- distance (de connection)

Define el tipo con BEGIN OF ... END OF
Luego define la tabla de ese tipo

**Pista 5: ¿Cómo obtener el nombre del carrier para el encabezado?**

Después del SELECT, lee el primer registro:
```
READ TABLE tabla INTO estructura INDEX 1.
IF sy-subrc = 0.
  variable_nombre = estructura-carrier_name.
ENDIF.
```

Así obtienes el nombre de la aerolínea para el encabezado del reporte.

---

### ✅ Checklist de Verificación

- [ ] Tipo personalizado definido con todos los campos necesarios
- [ ] Tabla de ese tipo personalizado definida
- [ ] SELECT combina 3 tablas con INNER JOIN
- [ ] Alias correctos: conn, car, apt_from, apt_to
- [ ] Condiciones ON correctas para cada JOIN
- [ ] Campos seleccionados con alias correcto (conn~, car~, apt_from~, apt_to~)
- [ ] WHERE filtra por carrier_id correcto
- [ ] Lectura del primer registro para obtener carrier_name
- [ ] Encabezado con nombre COMPLETO de aerolínea (no código)
- [ ] Encabezado con bordes decorativos
- [ ] Cada ruta muestra información completa de origen
- [ ] Cada ruta muestra información completa de destino
- [ ] Separadores entre rutas
- [ ] Pie del reporte con mensaje de finalización
- [ ] Output coincide EXACTAMENTE con el ejemplo
- [ ] Funciona con 'AA' y también con 'LH'

---

## 📚 Recursos de Apoyo

### Tablas de la Base de Datos

| Tabla | Campos Principales | Descripción |
|-------|-------------------|-------------|
| `/DMO/CONNECTION` | carrier_id, connection_id, airport_from_id, airport_to_id, distance, distance_unit | Conexiones/Rutas entre aeropuertos |
| `/DMO/CARRIER` | carrier_id, name, currency_code | Información de aerolíneas |
| `/DMO/AIRPORT` | airport_id, name, city, country | Información de aeropuertos |

### Relaciones entre Tablas

```
/DMO/CONNECTION.carrier_id ──→ /DMO/CARRIER.carrier_id
/DMO/CONNECTION.airport_from_id ──→ /DMO/AIRPORT.airport_id
/DMO/CONNECTION.airport_to_id ──→ /DMO/AIRPORT.airport_id
```

### Sintaxis de Referencia (sin código completo)

**SELECT básico**:
- `SELECT ... FROM tabla WHERE condicion INTO TABLE @tabla_interna`

**LOOP**:
- `LOOP AT tabla INTO estructura ... ENDLOOP`
- Usar `sy-tabix` para obtener número de iteración

**Condicionales**:
- `IF condicion ... ELSEIF condicion ... ELSE ... ENDIF`
- `CASE variable WHEN valor ... ENDCASE`

**INNER JOIN**:
- Requiere alias: `FROM tabla1 AS alias1`
- Condición ON: `ON alias1~campo = alias2~campo`
- Acceso a campos: `alias~campo`

---

## 🎯 Consejos Finales

### Antes de Codificar

1. ✅ **Lee toda la especificación funcional** del ejercicio
2. ✅ **Estudia el ejemplo de salida** línea por línea
3. ✅ **Analiza qué datos necesitas** y de dónde vienen
4. ✅ **Dibuja en papel** el flujo del programa y la lógica
5. ✅ **Identifica** qué SELECT necesitas y qué variables declarar
6. ✅ **Planifica el algoritmo** antes de escribir código

### Durante la Implementación

1. ✅ **Implementa por pasos** - no todo a la vez
2. ✅ **Prueba cada sección** antes de continuar
3. ✅ **Usa comentarios** para organizar tu código
4. ✅ **Revisa la nomenclatura** en cada variable (lv_, lt_, ls_, etc.)
5. ✅ **Compara tu output** frecuentemente con el ejemplo esperado

### Al Terminar

1. ✅ **Ejecuta el programa** y verifica el output
2. ✅ **Compara** con el resultado esperado línea por línea
3. ✅ **Revisa** la checklist de verificación
4. ✅ **Prueba** con diferentes datos de entrada
5. ✅ **Documenta** cualquier decisión de diseño

---

## 🏆 Criterios de Éxito

### Un ejercicio está completo cuando:

✅ **Funcionalidad**:
- Ejecuta sin errores
- Produce el output esperado exactamente
- Maneja casos vacíos correctamente

✅ **Output correcto**:
- Coincide línea por línea con el ejemplo
- Formato igual (separadores, indentación, etc.)
- Muestra todos los datos requeridos

✅ **Estándares**:
- Nomenclatura consistente (lv_, lt_, ls_, etc.)
- No declaraciones inline
- Código legible y comentado

✅ **Calidad**:
- Output bien formateado
- Verificaciones de datos implementadas
- Lógica clara y organizada

---

**Última actualización**: Diciembre 2024  
**Modalidad**: Análisis y diseño autónomo - Sin pseudocódigo  
**Tiempo total estimado**: 5-6 horas  
**Dificultad**: Intermedia-Avanzada - Requiere capacidad analítica  

¡Demuestra tu capacidad de análisis y resolución de problemas! 💪🚀🧠
