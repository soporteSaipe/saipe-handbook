# Machete – Pull Requests (PR) en GitHub

## Flujo de trabajo
```
git checkout main && git pull
git checkout -b feat/mi-cambio
# ...editar archivos...
git add -A
git commit -m "feat: mi cambio"
git push -u origin HEAD
```

- Crear PR en la web:  
  `https://github.com/soporteSaipe/<REPO>/compare/main...<rama>`  
- O con CLI:  
  `gh pr create -B main -t "feat: mi cambio" -b "Descripción"`

---

## Checklist del PR
- [ ] Cambios acotados  
- [ ] README / docs actualizados si aplica  
- [ ] Sin TODOs ni credenciales  
- [ ] 1 revisión recibida  
- [ ] Todas las conversaciones resueltas  

_Post-merge_  
- [ ] Merge con botón verde en GitHub  
- [ ] Delete branch (en GitHub y local)  
- [ ] Aviso en canal interno (Slack)  

## Borrar rama
```
git checkout main
git pull origin main
git branch -d <tu-rama>
git push origin --delete <tu-rama>
```

---

## No hacer
- `git push origin main`
- Reusar ramas viejas después de un merge

---

## Regla de oro
**Un cambio = una rama = un PR.**
