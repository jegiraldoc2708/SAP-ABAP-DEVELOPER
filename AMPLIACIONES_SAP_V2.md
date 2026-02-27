# Ampliaciones SAP — Guía para Desarrolladores ABAP Junior

> **Sistema de referencia:** SAP ERP 6.0 EHP7 · Mandante 810 · Oracle · Unicode
> **Audiencia:** Desarrolladores ABAP que conocen la sintaxis básica pero aún no han tocado ampliaciones en producción.

---

## ¿Qué es una Ampliación?

Una **ampliación** (enhancement) es código propio que se agrega a un programa SAP estándar **sin modificar el fuente original**.

| | Modificación | Ampliación |
|---|---|---|
| Cambia código SAP | ✅ Sí | ❌ No |
| Sobrevive upgrades | ❌ No (se pierde) | ✅ Sí |
| SAP la soporta | ❌ No | ✅ Sí |
| Riesgo | Alto | Bajo |

**Regla de oro:** Si SAP provee un punto de ampliación → úsalo. Solo modifica código estándar cuando no queda otra opción.

---

## Evolución de las Ampliaciones SAP

SAP ha ido modernizando su mecanismo de ampliaciones a lo largo de las versiones:

```
R/3 clásico          ERP 6.0            EHP+ / S/4HANA
─────────────        ──────────         ──────────────
User Exits     →     Classic BAdIs  →   New BAdIs (Enhancement Framework)
(CMOD/SMOD)          (SE18/SE19)        (SE18/SE19) + Enhancement Spots
```

En tu sistema **ERP6 EHP7** coexisten los cuatro tipos y todos son válidos.

---

## Tipos de Ampliaciones

### 1. User Exits (Exits de Usuario)

**¿Qué son?**
Rutinas vacías (`FORM ... ENDFORM`) que SAP dejó dentro de sus programas para que el cliente las llene. Son los más antiguos y los más simples.

**Transacciones clave:**
- `SMOD` — Ver los exits disponibles por módulo
- `CMOD` — Crear un proyecto y activar los exits

**Cómo funciona por dentro:**
En el código estándar SAP existe una llamada como:
```abap
CALL CUSTOMER-FUNCTION '002'
  EXPORTING
    us_vbak = vbak
  CHANGING
    es_vbak = vbak.
```
El número `'002'` corresponde al exit. SAP genera un function module vacío (`EXIT_SAPMV45A_002`) con un include (nombre visible en SMOD → Components) donde tú escribes tu código.

**Cuándo usarlo:** ✅ Cuando encuentras el exit exacto que necesitas. Es la opción más común en proyectos legacy de ERP6.
**Cuándo NO:** ❌ No admite múltiples implementaciones activas del mismo exit.

---

### 2. Classic BAdIs (Business Add-Ins Clásicos)

**¿Qué son?**
SAP define una interfaz ABAP (por ejemplo `IF_EX_MD_ADD_COL_SCRN`) y tú creas una clase que la implementa. Más orientado a objetos que los User Exits.

**Transacciones clave:**
- `SE18` — Ver la definición del BAdI
- `SE19` — Crear tu implementación

**Cómo funciona:**
```abap
" En el código estándar SAP:
GET BADI lv_mi_badi.
CALL BADI lv_mi_badi->mi_metodo
  EXPORTING iv_param = lv_valor.
```

**Cuándo usarlo:** ✅ Cuando el exit estándar es un Classic BAdI. Frecuente en módulos como MM, PM, WM.
**Cuándo NO:** ❌ No permite múltiples instancias activas del mismo BAdI (limitación del tipo clásico).

---

### 3. New BAdIs — Enhancement Framework ⭐ Recomendado

**¿Qué son?**
La evolución moderna de los BAdIs. Usan el Enhancement Framework introducido en ERP 6.0. Soportan múltiples implementaciones activas simultáneas y filtros por contexto.

**Transacciones clave:**
- `SE18` — Ver definición (misma Tcode, diferente tipo internamente)
- `SE19` — Crear implementación
- En SE18 se distinguen porque muestran "Enhancement Spot" como contenedor

**Diferencias vs Classic BAdI:**
| Característica | Classic BAdI | New BAdI |
|---|---|---|
| Múltiples impl. activas | ❌ No | ✅ Sí |
| Filtros de instancia | ❌ No | ✅ Sí |
| Contenedor | `IF_BADI_*` | Enhancement Spot |
| Llamada interna | `GET BADI` / `CALL BADI` | `GET BADI` (igual sintaxis) |

**Cuándo usarlo:** ✅ En ERP6 EHP7, siempre que el punto de ampliación sea un New BAdI. Busca en SE18 antes de modificar código.

---

### 4. Enhancement Spots — Puntos de Mejora

**¿Qué son?**
Permiten insertar código ABAP en **cualquier punto** de un programa estándar, incluso donde SAP no preparó un exit ni un BAdI.

**Dos subtipos:**

#### 4a. Enhancement Spot Implícito
SAP **automáticamente** genera puntos al inicio, fin de programas, function modules, métodos, etc. No necesitas que SAP lo haya preparado.

```abap
" Puntos implícitos disponibles en cualquier FM:
"   → Al principio del FM
"   → Al final del FM
"   → Antes/después de cada FORM
```

Cómo acceder: En SE37 (Function Module) → menú `Enhancement` → `Enhance`.
En el editor aparecen barras amarillas donde puedes insertar código.

#### 4b. Enhancement Spot Explícito
SAP marca puntos específicos en el código con la sentencia `ENHANCEMENT-POINT`. Tú implementas código para esos puntos.

```abap
" En código estándar (solo para referencia, no lo escribes tú):
ENHANCEMENT-POINT MY_EXIT_POINT SPOTS ZMI_ENHANCEMENT_SPOT.

" En tu implementación:
ENHANCEMENT 1 ZMI_IMPL.
  " Tu código aquí
  WRITE: / 'Punto de mejora activo'.
ENDENHANCEMENT.
```

**Cuándo usar Enhancement Spots:**
✅ Cuando no existe ni User Exit, ni BAdI para lo que necesitas.
⚠️ Usar con cuidado: al ser tan flexible, puede generar problemas en upgrades si SAP cambia la lógica circundante.

---

## Tabla Resumen Comparativa

| Tipo | Upgrade-safe | Múltiples impl. | Desde versión | Dónde buscar | Recomendación |
|---|:---:|:---:|---|---|---|
| User Exit (CMOD) | ✅ | ❌ | R/3 3.x | SMOD | OK en legacy |
| Classic BAdI | ✅ | ❌ | R/3 4.6 | SE18 | OK si ya existe |
| New BAdI | ✅ | ✅ | ERP 6.0 | SE18 | **⭐ Preferido** |
| Enh. Spot Implícito | ⚠️ Riesgo medio | ✅ | ERP 6.0 | SE37/SE80 | Solo si no hay otro |
| Enh. Spot Explícito | ✅ | ✅ | ERP 6.0 | SE18 | OK si SAP lo puso |

---

## Ejemplo Práctico Completo: User Exit en SD (Pedido de Venta)

> **Objetivo:** Controlar qué tipos de pedido se pueden crear. Si el usuario intenta crear un pedido con un tipo no permitido → mensaje de error y bloqueo.

> **¿Por qué este exit?** `V45A0002` se dispara cuando se ingresa o cambia el tipo de pedido en VA01. Su parámetro de entrada es `I_TVAK` (estructura del tipo de pedido), que tiene el campo `AUART`. Es el exit correcto para validaciones basadas en el tipo de documento.

### Paso 1 — Encontrar el Exit en SMOD

1. Ir a `SMOD`
2. Buscar el exit `V45A0002`
3. Hacer clic en **Detalles** → ver los componentes:
   - Función: `EXIT_SAPMV45A_002`
   - Include de código: el nombre exacto lo muestra SMOD en la columna **Include** (**verificar en SMOD antes de codificar**)
   - Parámetro disponible: `I_TVAK` (tipo: `TVAK`) → campo clave: `I_TVAK-AUART`

> **Tip:** En SMOD el nombre del exit es `V45A0002` (nombre corto). El function module real se llama `EXIT_SAPMV45A_002`.

### Paso 2 — Crear el Proyecto en CMOD

1. Ir a `CMOD`
2. Crear proyecto: `ZSD_VALIDACIONES` → Enter
3. En la pantalla del proyecto:
   - Texto: `Validaciones SD - Pedidos de Venta`
   - Clic en **Enhancement Assignments** (Asignaciones de ampliaciones)
4. Agregar el exit: `V45A0002` → Enter → Guardar
5. Volver a la pantalla principal del proyecto
6. Clic en **Components** (Componentes) → ver el include `ZXVVAZU02`
7. Hacer doble clic en `ZXVVAZU02` para abrirlo en el editor

### Paso 3 — Escribir el Código en el Include

El sistema abre el editor ABAP en el include del exit. Escribir el siguiente código:

```abap
*----------------------------------------------------------------------*
* Include: (nombre visible en SMOD → Components)                       *
* User Exit: EXIT_SAPMV45A_002                                         *
* Descripción: Validación de tipo de pedido permitido                  *
* Desarrollador: <tu nombre>   Fecha: <fecha>                          *
*----------------------------------------------------------------------*

* Solo se permiten los tipos de pedido OR (estándar) y ZOR (cliente Z)
* I_TVAK-AUART contiene el tipo de pedido ingresado por el usuario
IF i_tvak-auart NE 'OR' AND
   i_tvak-auart NE 'ZOR'.

  MESSAGE |Tipo de pedido '{ i_tvak-auart }' no está habilitado. Use OR o ZOR.|
    TYPE 'E'.
  " TYPE 'E' = Error → bloquea la selección del tipo
  " TYPE 'W' = Warning → permite continuar con confirmación
  " TYPE 'I' = Info → solo muestra mensaje
ENDIF.
```

> **Nota:** Ajusta los tipos de pedido permitidos (`'OR'`, `'ZOR'`) según los que existan en tu sistema. Puedes verificarlos en `OVAU`.

**Activar:** `Ctrl+F3` → Activar el include.

### Paso 4 — Activar el Proyecto en CMOD

1. Volver a `CMOD` → abrir el proyecto `ZSD_VALIDACIONES`
2. Clic en **Activate** (Activar el proyecto completo)
3. Confirmar la activación

> ⚠️ Si no activas el proyecto, el código no tiene efecto aunque el include esté activo.

### Paso 5 — Probar en VA01

1. Ir a `VA01`
2. En el campo **Tipo de pedido** ingresar un tipo **NO permitido** (ej. `BV` — Pedido contado)
3. Presionar **Enter**
4. El sistema debe mostrar: `Tipo de pedido 'BV' no está habilitado. Use OR o ZOR.` ✅
5. Cambiar el tipo a `OR` → presionar Enter → el exit no bloquea → continúa normalmente ✅

---

### ¿Qué pasó técnicamente?

```
VA01 (usuario graba)
  └── SAPMV45A (programa estándar SAP)
        └── CALL CUSTOMER-FUNCTION '002'
              └── EXIT_SAPMV45A_002 (function module generado)
                    └── INCLUDE ZXVVAZU02  ← aquí está TU código
```

SAP ejecutó el `CALL CUSTOMER-FUNCTION '002'` al ingresar/cambiar el tipo de pedido, pasando `I_TVAK` con los datos del tipo seleccionado. El include del exit evaluó `I_TVAK-AUART` y bloqueó los tipos no permitidos.

---

## Bonus: Validación de BSTNK al Grabar (Enhancement Spot Implícito)

**Objetivo:** Si el usuario intenta grabar un pedido sin llenar el campo "Su pedido nro." (`BSTNK`) → error y bloqueo del grabado.

**Punto de inserción:** FORM `USEREXIT_SAVE_DOCUMENT_PREPARE` en el include `MV45AFZZ` del programa `SAPMV45A`.

### Paso 1 — Navegar al Include MV45AFZZ

1. Ir a `SE38`
2. Ingresar programa: `SAPMV45A` → Display
3. En el menú del editor: `Goto` → `Include` → buscar `MV45AFZZ`
4. Alternativamente: en SE80, expandir `SAPMV45A` → `Includes` → doble clic en `MV45AFZZ`
5. Localizar el FORM:
```abap
FORM userexit_save_document_prepare.
* aquí insertaremos el Enhancement Spot
ENDFORM.
```

### Paso 2 — Activar el Modo Enhancement

1. Dentro del editor con `MV45AFZZ` abierto
2. Menú: `Enhancement` → `Enhance`
3. El editor muestra **barras amarillas** al inicio y fin de cada FORM/ENDFORM — esos son los puntos implícitos disponibles
4. Hacer clic en la **barra amarilla al inicio** del FORM `USEREXIT_SAVE_DOCUMENT_PREPARE`

### Paso 3 — Escribir el Código

El sistema crea automáticamente un Enhancement y abre el editor. Escribir:

```abap
*----------------------------------------------------------------------*
* Enhancement Spot Implícito en MV45AFZZ                               *
* FORM: USEREXIT_SAVE_DOCUMENT_PREPARE                                 *
* Descripción: Validar que BSTNK esté informado antes de grabar        *
* Desarrollador: <tu nombre>   Fecha: <fecha>                          *
*----------------------------------------------------------------------*

" VBAK es variable global de SAPMV45A → accesible aquí directamente
IF vbak-bstnk IS INITIAL.
  MESSAGE 'El número de pedido de cliente (BSTNK) es obligatorio.'
    TYPE 'E'.
  " TYPE 'E' = Error → bloquea el grabado
  " TYPE 'W' = Warning → permite continuar con confirmación
ENDIF.
```

**Activar:** `Ctrl+F3`

### Paso 4 — Probar en VA01

1. Ir a `VA01` → ingresar tipo `OR` → Enter
2. Llenar los datos mínimos (cliente, material, cantidad)
3. **Intentar grabar SIN llenar el campo "Su pedido nro."**
4. El sistema debe mostrar: `El número de pedido de cliente (BSTNK) es obligatorio.` ✅
5. Llenar el campo → grabar → funciona correctamente ✅

---

## Tips para Trabajar en el Sistema ERP6 EHP7

| Necesidad | Solución |
|---|---|
| Buscar exits disponibles por programa | `SMOD` → filtrar por nombre de programa |
| Buscar BAdIs disponibles | `SE18` → búsqueda por área funcional |
| Ver qué exits/BAdIs usa una transacción | En debugging activar breakpoint en `CALL CUSTOMER-FUNCTION` |
| Paquete para objetos de prueba | `$TMP` (local, sin transporte) o pedir paquete Z al BASIS |
| Crear transporte | `SE10` → crear orden de customizing |
| Ver includes de un exit | `SMOD` → ir al exit → pestaña Components |

---

## Flujo de Decisión para Elegir el Tipo de Ampliación

```
¿Necesitas ampliar un programa SAP?
        │
        ▼
¿Existe un BAdI (SE18)?
   ├─ Sí → ¿Es New BAdI? → Sí → ✅ Usa New BAdI (SE19)
   │                      → No → ✅ Usa Classic BAdI (SE19)
   │
   └─ No → ¿Existe un User Exit (SMOD)?
              ├─ Sí → ✅ Usa User Exit (CMOD)
              │
              └─ No → ¿Puedes usar Enhancement Spot?
                         ├─ Spot Explícito disponible → ✅ Úsalo
                         └─ Ninguno → ⚠️  Enhancement Spot Implícito
                                          (último recurso)
```

---

*Documento generado para formación interna · Sistema ERP6EHP7 · Mandante 810*
