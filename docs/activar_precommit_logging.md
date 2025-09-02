# Instructivo – Activar pre-commit y logging en un nuevo bot

Este documento explica cómo configurar los hooks de pre-commit y el logging estándar cuando se crea un nuevo bot a partir del `bot-template`.

---

## 1. Pre-commit + Ruff (calidad de código)

### 1.1 Instalación inicial (por desarrollador)
En cada PC de desarrollo, instalar una sola vez:

```bash
pip install pre-commit ruff
```

### 1.2 Activación en el repo del bot
Dentro de la carpeta del bot recién clonado:

```bash
pre-commit install
```

Esto registra los hooks definidos en `.pre-commit-config.yaml`.  
A partir de ahora, **cada commit** va a disparar automáticamente:

- Ruff → chequeo de estilo y errores comunes.
- Fix de espacios al final de línea.
- Fix de saltos de línea.

Si algún chequeo falla, el commit se cancela hasta corregirlo.

---

## 2. Logging estándar

El template ya incluye `src/<bot>/infra/logging_setup.py`.  
Para activarlo en el bot, agregar al inicio del archivo principal (ej: `main_gui.py`):

```python
from infra.logging_setup import setup_logging

# Inicializar logging
setup_logging("./logs", level="INFO")
```

Esto genera:
- Archivo `logs/app.log` (rotación automática, 5 backups, máx. 2 MB).
- Salida en consola (útil en desarrollo).
- Formato uniforme:
  ```
  2025-09-02 12:34:56 | INFO | nombre_modulo | Mensaje
  ```

---

## 3. Checklist rápido (para cada bot nuevo)
- [ ] Ejecuté `pip install pre-commit ruff` (una sola vez en mi PC).  
- [ ] Ejecuté `pre-commit install` dentro del repo del bot.  
- [ ] Verifiqué que al hacer commit, los hooks corren.  
- [ ] Agregué `setup_logging("./logs")` en el `main_gui.py` o entrypoint del bot.
