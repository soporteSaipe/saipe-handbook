# Guía para principiantes – Pull Requests (PR) en GitHub

Esta guía explica cómo trabajar con ramas y Pull Requests en GitHub para integrar cambios de forma ordenada.

---

## Conceptos clave
- **Rama (`branch`)**: línea de trabajo aislada de `main`.
- **PR (Pull Request)**: propuesta para integrar tu rama a `main`, que se revisa y aprueba antes del merge.
- **Merge**: acción que mete los cambios de tu rama en `main`.

> Regla de oro: **un cambio = una rama = un PR**. No se “reciclan” ramas ni PRs.

---

## 1) Flujo estándar (línea de comandos)

### A. Prepararte
```
git checkout main
git pull origin main
```

### B. Crear tu rama de trabajo
```
git checkout -b <tipo>/<descripcion-corta>
# ejemplos: feat/nuevo-readme, fix/typo-soporte, docs/checklist-pr
```

### C. Hacer cambios y commitear
```
# editás archivos…
git add -A
git commit -m "feat(handbook): agrega checklist de PR"
```

### D. Subir tu rama (¡no a main!)
```
git push -u origin NOMBRE_RAMA
```

### E. Crear el PR
- **Con CLI (GitHub CLI):**
```
gh pr create -B main -t "feat: agrega checklist PR" -b "Descripción breve del cambio"
```
- **Desde la web:**  
Abrir  
`https://github.com/<ORG>/<REPO>/compare/main...<tu-rama>?expand=1`  
→ botón **Create pull request**.

### F. Pedir y recibir revisión
- Asigná un/a revisor/a.  
- Resolvés comentarios si los hay.

### G. Mergear y limpiar
1. Botón **Merge pull request** → **Confirm merge**.  
2. **Delete branch** (en el PR).  
3. En tu repo local:
```
git checkout main
git pull origin main
git branch -d <tu-rama>
git push origin --delete <tu-rama>
```

---

## 2) Flujo desde la web (sin terminal)
1. Abrí un archivo (ej. `README.md`) → **Edit** (lápiz).  
2. Hacé un cambio chico.  
3. Abajo: **Create a new branch for this commit** → `docs/mi-cambio`.  
4. **Propose changes** → **Create pull request**.  
5. Pedí revisión → **Merge pull request** → **Delete branch**.

---

## 3) Nombres y mensajes (convenciones)
- **Ramas**: `<tipo>/<descripcion-corta>`  
  - `feat/` (nueva funcionalidad), `fix/`, `docs/`, `chore/`.
- **Commits**: `tipo(scope): descripción`  
  - Ejemplo: `docs(handbook): agrega checklist de PR`.

---

## 4) Checklist del PR
Completar en la descripción:

- [ ] Cambios acotados (un tema por PR)  
- [ ] README/Índice actualizado si aplica  
- [ ] Enlaces internos revisados (no rotos)  
- [ ] Sin TODOs ni credenciales  
- [ ] Pedí **1 revisión** (regla interna)  
- [ ] Todas las conversaciones resueltas  

_Post-merge_  
- [ ] Eliminé la rama  
- [ ] Avisé en el canal interno si corresponde  

---

## 5) Mantener tu rama al día (si `main` avanzó)
```
git fetch origin
git checkout <tu-rama>
git rebase origin/main          # o: git merge origin/main
# resolvé conflictos si aparecen
git push --force-with-lease     # necesario si usaste rebase
```

---

## 6) Problemas comunes

**“No veo el botón Create pull request”**  
- Usá la URL: `https://github.com/<ORG>/<REPO>/compare/main...<tu-rama>`  
- Verificá que haya cambios.  
- Confirmá que base = `main`, compare = tu rama.

**“Mi PR dice Out-of-date with base branch”**  
- Actualizá tu rama (sección 5) y volvé a pushear.

**“Ya hice un PR con esta rama y no me aparece otro”**  
- Los PR **no se reciclan**. Creá **una rama nueva** para el siguiente cambio.

**“Cometí el error de pushear a main”**  
- Revertí el commit o abrí un PR que corrija.  
- Activá un “airbag” local:
```
# .git/hooks/pre-push (crear archivo y chmod +x)
#!/bin/sh
branch=$(git rev-parse --abbrev-ref HEAD)
if [ "$branch" = "main" ]; then
  echo "Bloqueado: no pushear a main. Usá rama + PR."
  exit 1
fi
```

---

## 7) Resumen rápido
```
# empezar
git checkout main && git pull
git checkout -b feat/mi-cambio

# trabajar
git add -A
git commit -m "feat: mi cambio"
git push -u origin HEAD

# abrir PR
# web: https://github.com/<ORG>/<REPO>/compare/main...feat/mi-cambio
# o CLI:
gh pr create -B main -t "feat: mi cambio" -b "Descripción"

# tras aprobar
# (botón Merge en GitHub)
git checkout main && git pull
git branch -d feat/mi-cambio
git push origin --delete feat/mi-cambio
```

---

## 8) FAQ rápido

**¿Cuándo se pide PR?**  
Cuando tu rama tiene cambios respecto de `main` y querés integrarlos. El PR aparece en la comparación.

**¿Puedo reusar una rama después de mergear su PR?**  
No. Una vez mergeada, la rama se elimina. Para cambios nuevos, rama nueva.

**¿Qué pasa si hago `git push origin main`?**  
Si la protección está bien configurada, GitHub lo bloquea. Si no, evitá hacerlo: siempre trabajá con ramas + PR.

**¿Quién aprueba el PR?**  
Otro dev del equipo (mínimo 1). Es la regla interna y la configuración de protección.
