# 📚 Handbook de Desarrollo – Estudio Contable SAIPE

> Repositorio central de estándares, procesos y plantillas para bots internos.

## 🚀 Inicio Rápido

- 📖 **Documentación**: Disponible en [`/docs`](./docs)
- 🔄 **Contribuciones**: Cambios via Pull Requests (ver [`guia_principiantes_pr.md`](docs/guia_principiantes_pr.md))
- 👥 **Revisores**: Cualquier desarrollador que no haya subido los cambios

## ⭐ Regla de Oro

<div align="center">

### 🔄 **1 PR = 1 Revisión de Otro Dev**

> **No se mergea sin review**

</div>

---

## 📋 Contenido

- **Documentación**: Guías y estándares de desarrollo
- **Plantillas**: Templates para bots y procesos
- **Checklists**: Listas de verificación para releases
- **Runbooks**: Procedimientos operativos

---

## ✅ Checklist para abrir y mergear un Pull Request

**Antes de abrir el PR**
- [ ] Rama creada desde `main` con nombre claro (`feat/...`, `fix/...`, `docs/...`)
- [ ] Commits descriptivos (ej. `docs: agrega sección de releases`)
- [ ] Cambios acotados a un tema (evitar “PRs omnibus”)

**Descripción del PR**
- [ ] Resumen breve del cambio y motivo
- [ ] ¿Impacta el proceso de release/soporte/seguridad? (sí/no)
- [ ] Archivos clave tocados (lista corta)
- [ ] Enlaces de referencia (si aplica)

**Revisión previa (autor)**
- [ ] Pasé un vistazo final a los diffs (no quedaron TODOs ni borradores)
- [ ] Enlaces internos verificados (no hay links rotos)
- [ ] Índice actualizado si agregué/renombré docs (`docs/index.md`)
- [ ] Imágenes/archivos añadidos en carpetas correctas (p. ej. `docs/plantillas/`)

**Reglas del equipo**
- [ ] Obtuve **al menos 1 revisión** de otro dev (regla interna)
- [ ] Se resolvieron todas las conversaciones del PR

**Post-merge**
- [ ] Eliminé la rama (`Delete branch`)
- [ ] Si corresponde, **exporté a PDF** y copié a `H:\SISTEMAS\desarrollos\00-GUIAS`
- [ ] Aviso breve en el canal interno (Slack interno)

### Convenciones
- **Ramas**: `feat/<tema>`, `fix/<tema>`, `docs/<tema>`, `chore/<tema>`
- **Commits**: `type(scope): descripción` (ej. `docs(handbook): agrega checklist de PR`)
- **Scope** sugeridos: `handbook`, `estandar-bots`, `releases`, `soporte`, `seguridad`, `plantillas`

Última revisión: 01-09-2025

<div align="center">

**Desarrollado con ❤️ por el equipo de SAIPE**

</div>
