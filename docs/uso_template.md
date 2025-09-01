# 📂 Instructivo – Uso del Template de Bots

Este documento explica cómo crear un nuevo bot a partir del repositorio `bot-template`.

---

## 1. Crear un nuevo repositorio desde el template

1. Ir a [github.com/soporteSaipe/bot-template]([https://github.com](https://github.com/soporteSaipe/bot-template)).  
2. Asegurarse que está marcado como **Template repository** (Settings → General → Features → ☑️ Template repository).  
3. En la barra de GitHub, hacer clic en **Use this template** → **Create a new repository**.  
4. Completar:
   - **Repository name:** `bot-nombre` (ej: `bot-santafe`, `bot-afip-retenciones`).  
   - **Visibility:** Private.  
   - Crear repo.

---

## 2. Primeros pasos en el nuevo bot

1. Clonar el repo nuevo:
   ```bash
   git clone https://github.com/soporteSaipe/<NUEVO-REPO>.git
   cd <NUEVO-REPO>
   ```

2. Editar archivos iniciales:
   - `README.md`: completar qué hace el bot, requisitos, cómo correrlo.  
   - `RELEASE.md`: dejar versión inicial `v0.1.0`.  
   - `.env.example`: ajustar variables (URL base, paths).  
   - `pyinstaller.spec`: cambiar `bot_x` por el nombre real del bot.  
   - Carpetas en `src/bot_x/`: renombrar a `src/<nombre-bot>/`.

3. Confirmar estructura:
   ```text
   bot-nombre/
   ├─ src/<nombre-bot>/
   │  ├─ ui/
   │  ├─ core/
   │  ├─ infra/
   │  └─ __init__.py
   ├─ assets/
   ├─ config/ (vacío, aquí va credenciales.xlsx)
   ├─ .env.example
   ├─ README.md
   ├─ RELEASE.md
   ├─ pyinstaller.spec
   └─ build.bat / build.ps1
   ```

4. Primer commit:
   ```bash
   git add .
   git commit -m "chore: inicializa bot con template"
   git push origin main
   ```

---

## 3. Reglas para cada bot
- Cada bot **debe** mantener actualizado su `README.md`, `.env.example` y `RELEASE.md`.  
- Los `.exe` se publican en `H:\SISTEMAS\Accesos programas SAIPE\Sistemas\<bot>\`.  
- El handbook central no guarda código, solo lineamientos.
