# Modificación de ZTR_0027 - Procesamiento de Archivos Existentes

## Resumen del Cambio

La función `ZTR_0027` ha sido modificada para procesar archivos que **ya están generados** en la ruta de AL11, en lugar de generarlos desde un Proxy.

---

## Flujo Original (Antes)

### Entrada
- **Parámetro**: `I_INPUT TYPE ZINTTSA_ENVIAR_OMFCUENTAS_ECC` (datos del Proxy)

### Proceso
1. **Obtener ruta de AL11**: Usa `FILE_GET_NAME` con logical filename `'Z_FI_000005'`
2. **Construir nombre de archivo**: 
   - Extrae información de `i_input-tsa_enviar_omfcuentas_ecc_req-bgr00-group`
   - Construye: `ruta_base + '/' + sy-uzeit + nombre_del_input`
3. **Generar archivo**: 
   - Abre archivo para **OUTPUT** (escritura)
   - Escribe registro BGR00 (cabecera)
   - Escribe registros BBKPF y BBSEG desde el input del Proxy
   - Cierra el archivo
4. **Procesar archivo**: 
   - Ejecuta `rfbibl00` con el archivo generado
   - Crea job para procesamiento
   - Ejecuta `rsbdcsub` VIA JOB
5. **Lógica Calypso**: 
   - Valida configuración
   - Registra en tabla `ZTFI_1786`

### Salida
- Archivo generado en AL11
- Job creado para procesamiento
- Registro en `ZTFI_1786` (si aplica Calypso)

---

## Flujo Nuevo (Después)

### Entrada
- **Parámetro 1**: `IV_LOGICAL_FILENAME TYPE FILENAME-FILEINTERN OPTIONAL` (logical filename de AL11, por defecto `'Z_FI_000005'`)
- **Parámetro 2**: `IV_FILE_NAME TYPE STRING` (nombre del archivo específico a procesar)

### Proceso
1. **Obtener ruta de AL11**: Usa `FILE_GET_NAME` con logical filename (igual que original)
2. **Construir ruta completa**: 
   - Concatena: `ruta_base + '/' + iv_file_name`
3. **Leer archivo existente**: 
   - Abre archivo para **INPUT** (lectura)
   - Lee registro BGR00 para extraer `lv_group`
   - Lee primer registro BBKPF para extraer `lv_xblnr` y `lv_blart`
   - Cierra el archivo
4. **Procesar archivo**: 
   - Ejecuta `rfbibl00` con el archivo existente (igual que original)
   - Crea job para procesamiento (igual que original)
   - Ejecuta `rsbdcsub` VIA JOB (igual que original)
5. **Lógica Calypso**: 
   - Valida configuración (igual que original)
   - Registra en tabla `ZTFI_1786` (igual que original)

### Salida
- Archivo procesado (ya existía, no se genera)
- Job creado para procesamiento
- Registro en `ZTFI_1786` (si aplica Calypso)

---

## Comparación Detallada

| Aspecto | Código Original | Código Nuevo |
|---------|----------------|--------------|
| **Origen de datos** | Proxy (`I_INPUT`) | Archivo existente en AL11 |
| **Generación de archivo** | ✅ Sí (OUTPUT) | ❌ No |
| **Lectura de archivo** | ❌ No | ✅ Sí (INPUT) |
| **Obtención de `lv_group`** | Del input: `bgr00-group` | Del archivo: primer registro BGR00 |
| **Obtención de `lv_xblnr`** | Del input: `bbkpf-xblnr` | Del archivo: primer registro BBKPF |
| **Obtención de `lv_blart`** | Del input: `bbkpf-blart` | Del archivo: primer registro BBKPF |
| **Construcción de `lv_jobnam`** | `i_input-filenam(2) + lv_group + sy-uzeit` | `iv_file_name(2) + lv_group + sy-uzeit` |
| **Procesamiento rfbibl00** | ✅ Igual | ✅ Igual |
| **Lógica Calypso** | ✅ Igual | ✅ Igual |
| **Gestión de Jobs** | ✅ Igual | ✅ Igual |

---

## Ejemplo de Uso

### Código Original
```abap
DATA: ls_input TYPE zinttsa_enviar_omfcuentas_ecc.
" ... llenar ls_input desde Proxy ...
CALL FUNCTION 'ZTR_0027'
  EXPORTING
    i_input = ls_input.
" → Genera archivo y lo procesa
```

### Código Nuevo
```abap
CALL FUNCTION 'ZTR_0027'
  EXPORTING
    iv_logical_filename = 'Z_FI_000005'  " Opcional, usa este por defecto
    iv_file_name        = '103837RB_SettleDer_01010116102817508406825371708020250625_103802'.
" → Procesa archivo existente
```

---

## Puntos Importantes a Revisar

### 1. Lectura de `lv_group` desde BGR00
- **Código**: Líneas 117-145
- **Marcador**: `*** NUEVO_JG:`
- **Revisar**: Validar que las posiciones de lectura sean correctas según el formato real del archivo
- **Formato esperado**: `stype(1) + group(14) + mandt(3) + usnam(12) + ...`

### 2. Lectura de `lv_xblnr` y `lv_blart` desde BBKPF
- **Código**: Líneas 147-163
- **Marcador**: `*** NUEVO_JG:`
- **Revisar**: Validar posiciones aproximadas (línea 135: `+19(16)` y línea 137: `+35(2)`)
- **Formato esperado**: Registro tipo '2' con estructura BBKPF

### 3. Construcción de `lv_jobnam`
- **Código**: Líneas 165-172
- **Marcador**: `*** NUEVO_JG:`
- **Revisar**: En el original usa `i_input-filenam(2)`, validar si usar `iv_file_name(2)` es correcto

---

## Archivos Modificados

- `Modify Code/ZTR_0027.txt` - Función principal modificada

## Archivos Originales (Referencia)

- `Objetos ABAP/ZTR_0027/ZTR_0027.txt` - Código original

---

## Notas de Implementación

1. **Parámetros en SE37**: Al implementar en SAP, definir los parámetros en la definición de la función:
   - `IV_LOGICAL_FILENAME` (opcional, tipo `FILENAME-FILEINTERN`)
   - `IV_FILE_NAME` (obligatorio, tipo `STRING`)

2. **Validación de posiciones**: Antes de poner en producción, validar con un archivo real las posiciones de lectura de:
   - `lv_group` desde BGR00
   - `lv_xblnr` y `lv_blart` desde BBKPF

3. **Compatibilidad**: El código mantiene toda la lógica de Calypso, `rfbibl00` y jobs igual que el original, solo cambia el origen de los datos (archivo en lugar de Proxy).

