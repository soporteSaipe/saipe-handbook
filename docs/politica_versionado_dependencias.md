# 📦 Política de Versionado y Dependencias

Este documento define **cómo versionamos** los bots y **cómo mantenemos** sus dependencias para asegurar builds reproducibles y releases estables.

---

## 1) Versionado (SemVer)
Usamos **SemVer**: `vMAJOR.MINOR.PATCH`

- **MAJOR**: cambios incompatibles (rompen uso anterior, cambian UI/flujo, dejan de soportar un insumo).
- **MINOR**: nuevas funciones compatibles (agregan opciones, mejoran rendimiento, soportan un nuevo caso).
- **PATCH**: correcciones de bugs, ajustes menores, mejoras internas sin impacto funcional.

**Reglas:**  
- Cada release **debe** incrementar una sola parte (PATCH/MINOR/MAJOR).  
- La versión se registra en `RELEASE.md` del bot y en el **título del PR** del release.  
- El repo se etiqueta con **tag** `vX.Y.Z`.

**Comandos para taggear:**
```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

**Nombre de carpeta en servidor:**
```
\\servidor\desarrollos\releases\<bot>\vX.Y.Z\
```
Mantener `latest` apuntando a la versión vigente.

---

## 2) Flujo de Release (resumen)
1. Rama `release/vX.Y.Z` desde `main`.
2. Actualizar `RELEASE.md` y README si aplica.
3. Generar build con `pyinstaller.spec` y probar “smoke test”.
4. PR → 1 review → Merge.
5. Crear tag `vX.Y.Z`.
6. Copiar a servidor y actualizar `latest`.
7. Registrar en el **changelog central** (handbook).

---

## 3) Estrategia de dependencias

### 3.1 Objetivo
- **Reproducible hoy y dentro de 1 año.**
- Actualizaciones **controladas**, no a cada commit.

### 3.2 PyPI (librerías Python)
- En `pyproject.toml` usar rangos **compatibles** (ejemplo):
  ```toml
  [project]
  requires-python = ">=3.11,<3.13"
  dependencies = [
    "pyside6>=6.6,<7",
    "playwright>=1.46,<2",
    "pandas>=2.2,<3",
    "python-dotenv>=1.0,<2",
    "ruff>=0.5,<1",
  ]
  ```
- Para builds reproducibles, generar un **congelado** al publicar:
  ```bash
  pip freeze > requirements-freeze.txt
  ```
  Ese archivo se adjunta al release (sirve de evidencia de versiones exactas).

> Alternativa más avanzada (opcional): usar `pip-tools` o `uv` para lockfiles. Por ahora, con `requirements-freeze.txt` alcanza.

### 3.3 Navegador y drivers
- **Firefox portable / Chromium**: fijar versión por release y documentarla en `RELEASE.md`.  
- **Playwright**: tras instalar, sincronizar binarios:
  ```bash
  playwright install
  ```
- Si se usa Selenium + geckodriver/chromedriver, registrar versiones exactas en `RELEASE.md`.

### 3.4 Archivos externos
- `credenciales.xlsx`, plantillas Excel/CSV u otros insumos **no versionados**: indicar hash o fecha en `RELEASE.md` si su formato cambia.

---

## 4) Cadencia de actualización
- **Trimestral (cada 3 meses)**: revisar dependencias y navegadores.
- **Urgente**: cuando el sitio destino cambia (AFIP, ARBA, etc.) o aparece un bug crítico.

**Checklist trimestral:**
- [ ] Crear rama `chore/dep-update-YYYYQX`  
- [ ] Actualizar rangos en `pyproject.toml` **solo si es necesario**  
- [ ] `pip install -U -r requirements-freeze.txt` y re-evaluar compatibilidad  
- [ ] Regenerar `requirements-freeze.txt`  
- [ ] Probar smoke test y flujo principal  
- [ ] PR con título `chore: dependency refresh YYYY-QX`

---

## 5) Seguridad mínima
- Ejecutar `pip-audit` en PRs de release (opcional, local):
  ```bash
  pip install pip-audit
  pip-audit
  ```
- No subir `.env`, credenciales ni archivos sensibles.
- No loguear claves ni CUIT completos (usar enmascarado).

---

## 6) Compatibilidad de Python
- Objetivo: **Python 3.11** para bots nuevos.  
- Mantener compatibilidad con 3.12 si los paquetes lo soportan.  
- Cuando subamos de versión mayor de Python, hacer un **MINOR** como mínimo si es transparente; **MAJOR** si rompe compatibilidad.

---

## 7) Plantillas de mensajes

### 7.1 Título de PR de release
```
release: vX.Y.Z – {bot} – {resumen corto}
```

### 7.2 Cuerpo del PR (secciones)
- **Cambios**: lista resumida  
- **Impacto**: ¿rompe algo?, ¿requiere nuevo Excel/plantilla?  
- **Versiones**: Python, Playwright/Firefox, librerías claves  
- **Smoke test**: pasos y resultado  
- **Checklist**: copia al servidor, actualización de `latest`, registro en handbook

---

## 8) Decidir el tipo de versión (guía rápida)
- ¿Se cambió un selector de scraping, pero el output es igual? → **PATCH**  
- ¿Se agregó una opción nueva en la UI y sigue todo lo existente? → **MINOR**  
- ¿Se cambió el formato de salida o un flujo clave? → **MAJOR**

---

## 9) Preguntas frecuentes
**¿Por qué no fijar versiones exactas en `pyproject.toml`?**  
Porque dificulta recibir parches de seguridad/compatibilidad. Usamos rangos + `requirements-freeze.txt` por release para reproducibilidad.

**¿Podemos automatizar esto?**  
Sí: más adelante, un workflow de GitHub Actions puede generar `requirements-freeze.txt`, crear el tag y adjuntarlo al release.

---

## 10) Dónde guardar este documento
En el handbook central: `org-handbook/docs/politica_versionado_dependencias.md`.  
Cada bot debe apuntar a este documento desde su `README.md`.
