# Estrategia de Branching

**Última actualización:** 2026-01-11  
**Versión:** 1.0

> **⚠️ IMPORTANTE:** Este documento define la estrategia de branching que debe seguirse en todo el proyecto. Todos los desarrolladores (y IAs) deben seguir estas convenciones consistentemente.

## Estrategia Elegida: GitHub Flow

### Justificación

Se ha elegido **GitHub Flow** como estrategia de branching para este proyecto por las siguientes razones:

1. **Simplicidad:** Proyecto pequeño/mediano con equipo pequeño
2. **Flexibilidad:** Permite iteración rápida y deployment continuo
3. **Alineación con herramientas:** Integración natural con GitHub y Linear
4. **Mantenibilidad:** Menos complejidad que Git Flow, más estructura que Trunk-Based
5. **Adecuado para el contexto:** Proyecto en fase inicial con desarrollo activo

### Comparación con Otras Estrategias

#### GitHub Flow ✅ (Elegida)
- **Ventajas:**
  - Simple y directo
  - Ideal para proyectos pequeños/medianos
  - Deployment continuo fácil
  - Menos overhead administrativo
- **Desventajas:**
  - Menos estructura para proyectos muy grandes
  - No separa explícitamente desarrollo de producción

#### Git Flow
- **Ventajas:**
  - Muy estructurado
  - Separación clara de desarrollo/producción
  - Ideal para proyectos grandes con releases complejos
- **Desventajas:**
  - Demasiado complejo para este proyecto
  - Más overhead administrativo
  - No necesario para el tamaño actual del equipo

#### Trunk-Based Development
- **Ventajas:**
  - Muy simple
  - Ideal para equipos muy pequeños
- **Desventajas:**
  - Falta de estructura para features grandes
  - Dificulta trabajo en paralelo
  - No integra bien con Linear/issues

## Estructura de Branches

### Branch Principal

- **`main`** - Branch principal y de producción
  - Siempre debe estar en estado deployable
  - Protegido (requiere Pull Request para cambios)
  - Contiene el código estable y listo para producción

### Branches de Desarrollo

Todas las ramas de desarrollo se crean desde `main` y se integran de vuelta mediante Pull Requests.

## Convenciones de Nombres de Branches

### Formato General

Las ramas deben seguir el formato:

```
[tipo]/[issue-id]-[descripcion-corta]
```

O alternativamente (si no hay issue):

```
[tipo]/[descripcion-corta]
```

### Tipos de Branches

#### 1. Features (`feature/`)
Para nuevas funcionalidades y características.

**Formato:**
- `feature/DNT-XXX-nombre-descriptivo`
- `feature/authentication-endpoint`

**Ejemplos:**
- `feature/DNT-240-value-generation-api`
- `feature/user-authentication`
- `rafaceitunoalvarez/dnt-240-feature-value-generation-api` (con prefijo de usuario si aplica)

#### 2. Fixes (`fix/`)
Para corrección de bugs.

**Formato:**
- `fix/DNT-XXX-descripcion-bug`
- `fix/login-error`

**Ejemplos:**
- `fix/DNT-245-null-pointer-exception`
- `fix/memory-leak-rag-system`

#### 3. Documentation (`docs/`)
Para cambios en documentación.

**Formato:**
- `docs/DNT-XXX-descripcion`
- `docs/update-readme`

**Ejemplos:**
- `docs/DNT-233-definir-estrategia-branching`
- `docs/api-documentation`

#### 4. Chores (`chore/`)
Para tareas de mantenimiento, configuración, etc.

**Formato:**
- `chore/DNT-XXX-descripcion`
- `chore/update-dependencies`

**Ejemplos:**
- `chore/DNT-234-configurar-gitignore`
- `chore/update-docker-compose`

#### 5. Refactor (`refactor/`)
Para refactorización de código sin cambiar funcionalidad.

**Formato:**
- `refactor/DNT-XXX-descripcion`
- `refactor/value-engine-structure`

**Ejemplos:**
- `refactor/DNT-250-modularize-core`
- `refactor/extract-common-utils`

### Reglas de Nomenclatura

1. **Usar kebab-case** (minúsculas con guiones)
2. **Incluir ID de issue cuando sea posible** (facilita tracking)
3. **Descripciones cortas y descriptivas** (máximo 50 caracteres)
4. **Evitar caracteres especiales** excepto guiones
5. **No usar espacios** en nombres de branches

### Integración con Linear

- **Preferir incluir ID de issue:** `feature/DNT-XXX-descripcion`
- **Linear genera nombres automáticos:** `rafaceitunoalvarez/dnt-XXX-descripcion`
- **Ambos formatos son aceptables** si son consistentes

## Flujo de Trabajo

### 1. Crear Branch desde Main

```bash
# Asegurarse de estar en main actualizado
git checkout main
git pull origin main

# Crear nueva rama
git checkout -b feature/DNT-XXX-nombre-descriptivo
```

### 2. Trabajar en la Rama

- Hacer commits frecuentes y descriptivos
- Push regular a la rama remota
- Mantener la rama actualizada con `main` si es necesario

```bash
# Trabajar y hacer commits
git add .
git commit -m "feat: Implementar funcionalidad X"

# Push a la rama
git push origin feature/DNT-XXX-nombre-descriptivo
```

### 3. Actualizar con Main (si es necesario)

Si `main` ha avanzado mientras trabajas:

```bash
# Desde tu rama de feature
git checkout feature/DNT-XXX-nombre-descriptivo
git pull origin main
# Resolver conflictos si los hay
git push origin feature/DNT-XXX-nombre-descriptivo
```

### 4. Crear Pull Request

- **SIEMPRE** crear Pull Request antes de mergear
- Enlazar con el issue en Linear: `Closes DNT-XXX`
- Incluir descripción clara de los cambios
- Mencionar cualquier breaking change

### 5. Revisión y Merge

- Esperar aprobación de revisión
- Asegurarse de que los tests pasan
- Mergear cuando esté aprobado

## Pull Requests

### Requisitos para Merge

1. **Aprobación de revisión** (al menos 1 aprobador)
2. **Tests pasando** (si aplica)
3. **Sin conflictos** con `main`
4. **Issue en Linear** movido a "In Review" o "Done"
5. **Descripción clara** de cambios

### Estrategia de Merge

**Método recomendado:** **Squash and Merge**

- Combina todos los commits en uno solo
- Mantiene `main` limpio y fácil de seguir
- Permite mensaje de commit descriptivo
- Facilita rollback si es necesario

**Alternativas:**
- **Merge commit:** Si se quiere preservar historial completo de la rama
- **Rebase and merge:** Si se quiere historial lineal (más complejo)

### Mensajes de Commit en PRs

El mensaje del commit de merge debe seguir el formato:

```
[tipo]: Descripción corta

Descripción detallada de los cambios realizados.

Closes DNT-XXX
```

**Tipos de commit:**
- `feat:` - Nueva funcionalidad
- `fix:` - Corrección de bug
- `docs:` - Cambios en documentación
- `chore:` - Tareas de mantenimiento
- `refactor:` - Refactorización
- `test:` - Añadir o modificar tests
- `style:` - Cambios de formato (no afectan código)

### Template de Pull Request

```markdown
## Descripción
Breve descripción de los cambios realizados.

## Tipo de Cambio
- [ ] Nueva funcionalidad
- [ ] Corrección de bug
- [ ] Documentación
- [ ] Refactorización
- [ ] Otro

## Issue Relacionado
Closes DNT-XXX

## Checklist
- [ ] Código implementado y probado
- [ ] Tests añadidos/actualizados (si aplica)
- [ ] Documentación actualizada (si aplica)
- [ ] Sin conflictos con main
- [ ] Issue en Linear actualizado
```

## Estrategia de Releases

### Versionado Semántico

El proyecto seguirá **Semantic Versioning (SemVer)**: `MAJOR.MINOR.PATCH`

- **MAJOR:** Cambios incompatibles con versiones anteriores
- **MINOR:** Nueva funcionalidad compatible hacia atrás
- **PATCH:** Correcciones de bugs compatibles

### Proceso de Release

1. **Preparar Release:**
   - Asegurarse de que `main` está estable
   - Actualizar `CHANGELOG.md` (si existe)
   - Actualizar versión en `package.json`

2. **Crear Tag:**
   ```bash
   git tag -a v1.0.0 -m "Release v1.0.0"
   git push origin v1.0.0
   ```

3. **Crear Release en GitHub:**
   - Usar la interfaz de GitHub o GitHub CLI
   - Incluir notas de release
   - Enlazar con issues cerrados

### Branches de Release (Opcional)

Para releases mayores, se puede crear una rama temporal:

- `release/v1.0.0` - Para preparar release
- Solo para releases complejos que requieren múltiples cambios
- Mergear a `main` cuando esté listo

### Hotfixes

Para correcciones urgentes en producción:

1. Crear branch desde `main`: `hotfix/DNT-XXX-descripcion`
2. Implementar fix
3. Crear PR y mergear rápidamente
4. Crear tag de patch release: `v1.0.1`

## Protección de Branches

### Branch `main`

**Configuración recomendada:**
- ✅ Requerir Pull Request antes de merge
- ✅ Requerir aprobación de revisión (1 aprobador mínimo)
- ✅ Requerir que los checks de CI pasen (si están configurados)
- ✅ No permitir force push
- ✅ No permitir eliminar la rama

### Otras Ramas

- No requieren protección especial
- Se pueden eliminar después de merge

## Integración con Linear

### Workflow Recomendado

1. **Crear Issue en Linear** → Obtener ID (ej: DNT-XXX)
2. **Crear Branch** usando el ID: `feature/DNT-XXX-descripcion`
3. **Trabajar en la rama** y hacer commits
4. **Crear Pull Request** enlazando con `Closes DNT-XXX`
5. **Mover Issue a "In Review"** cuando PR esté listo
6. **Mover Issue a "Done"** cuando PR esté mergeado

### Enlaces en Commits

- Usar `Closes DNT-XXX` en mensajes de commit para cerrar issues automáticamente
- Usar `Refs DNT-XXX` para referenciar sin cerrar

## Buenas Prácticas

### Do's ✅

- ✅ Crear branches desde `main` actualizado
- ✅ Usar nombres descriptivos y consistentes
- ✅ Hacer commits frecuentes y pequeños
- ✅ Escribir mensajes de commit claros
- ✅ Crear Pull Requests para todos los cambios
- ✅ Mantener branches actualizados con `main`
- ✅ Eliminar branches después de merge

### Don'ts ❌

- ❌ Trabajar directamente en `main`
- ❌ Mergear sin Pull Request
- ❌ Usar nombres de branches genéricos (`test`, `fix`, etc.)
- ❌ Hacer commits grandes sin sentido
- ❌ Dejar branches huérfanas sin mergear
- ❌ Force push a `main`

## Ejemplos de Flujo Completo

### Ejemplo 1: Nueva Feature

```bash
# 1. Crear branch desde main
git checkout main
git pull origin main
git checkout -b feature/DNT-240-value-generation-api

# 2. Trabajar y hacer commits
git add .
git commit -m "feat: Implementar endpoint de generación de valores"
git push origin feature/DNT-240-value-generation-api

# 3. Crear Pull Request en GitHub
# - Título: "feat: Implementar endpoint de generación de valores"
# - Descripción: "Closes DNT-240"
# - Revisar y aprobar

# 4. Mergear (squash and merge)
# 5. Eliminar branch
git branch -d feature/DNT-240-value-generation-api
git push origin --delete feature/DNT-240-value-generation-api
```

### Ejemplo 2: Fix de Bug

```bash
# 1. Crear branch
git checkout main
git pull origin main
git checkout -b fix/DNT-245-null-pointer-exception

# 2. Implementar fix
git add .
git commit -m "fix: Corregir null pointer en ValueEngine"
git push origin fix/DNT-245-null-pointer-exception

# 3. Crear PR y mergear
```

## Resumen

- **Estrategia:** GitHub Flow
- **Branch principal:** `main`
- **Convención:** `[tipo]/DNT-XXX-descripcion` o `[tipo]/descripcion`
- **Merge:** Squash and Merge (recomendado)
- **Releases:** Tags semánticos desde `main`
- **Integración:** Linear issues enlazados con branches

## Referencias

- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Semantic Versioning](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

**Nota:** Esta estrategia debe seguirse consistentemente. Cualquier cambio a esta estrategia debe ser documentado y comunicado al equipo.
