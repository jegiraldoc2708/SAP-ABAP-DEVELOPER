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

> **Objetivo:** Validar que el campo "Pedido de cliente" (`VBAK-BSTNK`) esté informado al grabar un pedido de venta. Si está vacío → mensaje de error y bloqueo del guardado.

### Paso 1 — Encontrar el Exit en SMOD

1. Ir a `SMOD`
2. Buscar por: `VBAK` en el campo de búsqueda, o filtrar por módulo `SD`
3. Localizar el exit `V45A0002` (exit de usuario para ventas)
4. Hacer clic en **Detalles** → ver los componentes:
   - Función: `EXIT_SAPMV45A_002`
   - Include de código: el nombre exacto lo muestra SMOD en la columna **Include** (típicamente `ZXVVAZU02`, pero varía por sistema — **verificar en SMOD antes de codificar**)
   - Estructura disponible: `VBAK` (cabecera del pedido)

> **Tip:** En SMOD el nombre del exit es `V45A0002` (nombre corto). El function module real se llama `EXIT_SAPMV45A_002`.

> **¿Por qué BSTNK?** Este campo ("Nro. pedido de cliente") **no tiene validación obligatoria en SAP estándar** — es opcional por defecto en VA01. Solo se vuelve obligatorio si lo configuras vía `OVAU` (tipo de pedido) o selección de campos. Por eso es el ejemplo ideal: cualquiera puede probarlo sin riesgo.

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

El sistema abre el editor ABAP en el include `ZXVVAZU02`. Escribir el siguiente código:

```abap
*----------------------------------------------------------------------*
* Include ZXVVAZU02                                                     *
* User Exit: EXIT_SAPMV45A_002                                         *
* Descripción: Validación al grabar pedido de venta                    *
* Desarrollador: <tu nombre>   Fecha: <fecha>                          *
*----------------------------------------------------------------------*

* Verificar que el campo "Pedido de cliente" no esté vacío
IF vbak-bstnk IS INITIAL.
  MESSAGE 'El número de pedido de cliente (campo BSTNK) es obligatorio.'
    TYPE 'E'.
  " TYPE 'E' = Error → bloquea el grabado
  " TYPE 'W' = Warning → permite continuar con confirmación
  " TYPE 'I' = Info → solo muestra mensaje
ENDIF.
```

**Activar:** `Ctrl+F3` → Activar el include.

### Paso 4 — Activar el Proyecto en CMOD

1. Volver a `CMOD` → abrir el proyecto `ZSD_VALIDACIONES`
2. Clic en **Activate** (Activar el proyecto completo)
3. Confirmar la activación

> ⚠️ Si no activas el proyecto, el código no tiene efecto aunque el include esté activo.

### Paso 5 — Probar en VA01

1. Ir a `VA01` → crear pedido tipo OR
2. Llenar los datos mínimos (cliente, material, cantidad)
3. **Intentar grabar SIN llenar el campo "Su pedido nro."** (`BSTNK`)
4. El sistema debe mostrar: `El número de pedido de cliente (campo BSTNK) es obligatorio.`
5. Llenar el campo y grabar → ahora funciona correctamente ✅

---

### ¿Qué pasó técnicamente?

```
VA01 (usuario graba)
  └── SAPMV45A (programa estándar SAP)
        └── CALL CUSTOMER-FUNCTION '002'
              └── EXIT_SAPMV45A_002 (function module generado)
                    └── INCLUDE ZXVVAZU02  ← aquí está TU código
```

SAP ejecutó el `CALL CUSTOMER-FUNCTION '002'` en el momento de grabar, lo que disparó el function module `EXIT_SAPMV45A_002`, que a su vez ejecutó el include `ZXVVAZU02` donde está la validación.

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
