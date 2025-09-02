# Runbook – {BOT}

## 1. Información general
- **Responsable técnico:** {Nombre / contacto}  
- **Última versión instalada:** vX.Y.Z (fecha YYYY-MM-DD)  
- **Ubicación del ejecutable:**  
  ```
  \\servidor\desarrollos\releases\{bot}\latest\main_gui.exe
  ```

---

## 2. Insumos y salidas
- **Entrada(s):** {archivos_entrada}, formato, ubicación  
- **Salida(s):** carpeta `{OUTPUT_DIR}` (por defecto: `./salidas/`)  
- **Logs:** carpeta `{LOG_DIR}` (por defecto: `./logs/`), archivo principal `app.log`  

---

## 3. Ejecución
1. Verificar que `.env` esté presente y válido  
2. Abrir `main_gui.exe`  
3. Seleccionar insumo y ejecutar  
4. Confirmar archivo de salida generado  

---

## 4. Chequeos rápidos (5 minutos)
- [ ] Conectividad a `{BASE_URL}`  
- [ ] `FIREFOX_PATH` existe (si aplica)  
- [ ] Permisos de escritura en `OUTPUT_DIR`  
- [ ] `credenciales.xlsx` accesible (si aplica)  

---

## 5. Errores frecuentes
| Código / Mensaje | Causa común | Acción sugerida |
|------------------|-------------|-----------------|
| ERR-NET-01       | Sitio caído o timeout | Probar en navegador; reintentar en 15 min |
| ERR-LOGIN-02     | Credencial inválida   | Verificar fila en `credenciales.xlsx` |
| ERR-PATH-03      | Ruta no encontrada    | Revisar `.env` (`OUTPUT_DIR`, `FIREFOX_PATH`) |

---

## 6. Escalamiento
- Si el problema persiste: adjuntar `app.log` y archivo de entrada (si procede) y escalar a {canal_soporte}.  

---

## 7. Procedimientos
### 7.1 Rotado de logs
- Los logs se rotan automáticamente a `{LOG_DIR}/app.YYYY-MM-DD.log` (retención sugerida: 90 días).  

### 7.2 Actualización de versión
1. Copiar nueva `vX.Y.Z` a `\\servidor\desarrollos\releases\{bot}\vX.Y.Z\`  
2. Actualizar `latest` al nuevo directorio  
3. Ejecutar **smoke test** (ver sección 4)  
4. Registrar en `RELEASE.md`  

---

## 8. Anexos
- Estructura de carpetas estándar  
- Variables de `.env` y significado  
