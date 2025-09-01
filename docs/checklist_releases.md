# Checklist de Release de Bots

Cada nueva versión de un bot debe seguir estos pasos antes de distribuirse a los contadores.

---

## 1. Preparación
- [ ] Partir de la rama `main` actualizada (`git checkout main && git pull origin main`)
- [ ] Confirmar que el código compila y funciona en entorno local
- [ ] Revisar dependencias en `pyproject.toml` / `requirements.txt`
- [ ] Actualizar `.env.example` si hubo cambios en variables

---

## 2. Versión
- [ ] Asignar número de versión según semver (`vMAJOR.MINOR.PATCH`)
  - `MAJOR`: cambios incompatibles
  - `MINOR`: nueva funcionalidad compatible
  - `PATCH`: bugfixes o mejoras menores
- [ ] Actualizar `README.md` con número de versión

---

## 3. Build
- [ ] Generar ejecutable con PyInstaller usando el `.spec` del proyecto
  ```
  pyinstaller pyinstaller.spec --noconfirm --clean
  ```
- [ ] Verificar que el ejecutable se crea en `dist/`
- [ ] Testear el `.exe` en una PC limpia / similar a la de los contadores

---

## 4. Release en servidor
- [ ] Crear carpeta en `\\servidor\desarrollos\releases\<bot>\vX.Y.Z\`
- [ ] Copiar:
  - `.exe` final
  - carpeta `icons/` o `assets/` si corresponde
  - cualquier dependencia externa requerida (ej: navegador portable)
- [ ] Mantener versiones anteriores (no borrar releases viejos)

---

## 5. Documentación
- [ ] Exportar guía rápida de uso a PDF y colocar en la misma carpeta de release
- [ ] Actualizar handbook (`org-handbook/docs/releases.md`) con la nueva versión y fecha
- [ ] Avisar al equipo interno del release (ejemplo: canal de WhatsApp/Teams interno)

---

## 6. Post-release
- [ ] Monitorear uso en los primeros días (errores reportados, logs)
- [ ] Si hay bugfix → crear `vX.Y.(PATCH+1)` siguiendo mismo proceso

---

## 📑 Registro de Releases (Changelog Centralizado)

| Bot        | Versión | Fecha       | Cambios principales                  | Responsable |
|------------|---------|-------------|--------------------------------------|-------------|
| bot_x      | v1.0.0  | 2025-09-01  | Primera release estable              | Ezequiel Z. |
| bot_y      | v0.9.2  | 2025-08-15  | Fix exportación Excel                | Gonzalo C.  |
| bot_z      | v2.1.0  | 2025-08-01  | Nuevo módulo AFIP + mejoras logging  | Marcos B.   |

> Cada nuevo release debe agregarse a esta tabla con versión, fecha, cambios y responsable.
