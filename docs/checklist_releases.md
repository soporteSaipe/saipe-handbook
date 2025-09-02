# ✅ Checklist de Release de Bots (actualizado)

Cada nueva versión de un bot debe seguir estos pasos antes de distribuirse a los contadores.

---

## 1. Preparación
- [ ] Partir de la rama `main` actualizada  
  ```bash
  git checkout main
  git pull origin main
  ```
- [ ] Confirmar que el bot corre correctamente en entorno local
- [ ] Revisar y, si corresponde, actualizar dependencias en `pyproject.toml`
- [ ] Regenerar `requirements-freeze.txt` con:
  ```bash
  pip freeze > requirements-freeze.txt
  ```
- [ ] Actualizar `.env.example` si hubo cambios en variables

---

## 2. Versión
- [ ] Asignar número de versión usando **SemVer** (`vMAJOR.MINOR.PATCH`)  
  - **MAJOR**: cambios incompatibles  
  - **MINOR**: nueva funcionalidad compatible  
  - **PATCH**: bugfixes o mejoras menores  
- [ ] Actualizar `RELEASE.md` con nueva entrada (`vX.Y.Z`, fecha, cambios, versiones de dependencias)
- [ ] Taggear versión en Git:
  ```bash
  git tag vX.Y.Z -m "release: vX.Y.Z"
  git push origin vX.Y.Z
  ```

---

## 3. Build
- [ ] Generar ejecutable con PyInstaller:
  ```bash
  pyinstaller pyinstaller.spec --noconfirm --clean
  ```
- [ ] Verificar que se crea `dist/main_gui.exe`
- [ ] Testear el `.exe` en una PC limpia / similar a la de los contadores
- [ ] Si se usan `assets/`, verificar que se cargan con `resource_path`

---

## 4. Publicación en servidor
- [ ] Ejecutar script `tools/make_release.bat` o `make_release.ps1`, por ejemplo:
  ```bat
  tools\make_release.bat bot-afip-retenciones 1.0.0 \\servidor\desarrollos\releases
  ```
- [ ] Validar que se creó la carpeta:
  ```
  \\servidor\desarrollos\releases\<bot>\vX.Y.Z\
  ```
- [ ] Confirmar que `latest/` apunta a esa versión
- [ ] Mantener versiones anteriores (no borrar releases viejos)

---

## 5. Documentación
- [ ] Exportar guía rápida de uso a PDF y colocar en la carpeta del release
- [ ] Registrar release en el handbook central (Wiki → sección “Releases”)
- [ ] Avisar al equipo interno del release (ejemplo: canal de WhatsApp/Teams interno)

---

## 6. Post-release
- [ ] Monitorear uso en los primeros días (errores reportados, logs)
- [ ] Si hay bugfix → crear `vX.Y.(PATCH+1)` siguiendo este mismo proceso

---

## 📑 Registro de Releases (Changelog Centralizado)
*(Ejemplo de tabla en handbook central)*

| Bot        | Versión | Fecha       | Cambios principales                  | Responsable |
|------------|---------|-------------|--------------------------------------|-------------|
| bot_x      | v1.0.0  | 2025-09-01  | Primera release estable              | Ezequiel Z. |
| bot_y      | v0.9.2  | 2025-08-15  | Fix exportación Excel                | Gonzalo C.  |
| bot_z      | v2.1.0  | 2025-08-01  | Nuevo módulo AFIP + mejoras logging  | Marcos B.   |

---

> Cada nuevo release debe agregarse a esta tabla con versión, fecha, cambios y responsable.
