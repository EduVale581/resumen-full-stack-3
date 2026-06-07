# 🌿 GitFlow, Comandos Git & Errores Comunes

> Estrategia de ramas, comandos fundamentales y los errores más comunes en equipos de desarrollo moderno.

---

## 🔀 GitFlow — Modelo de Ramas

GitFlow es una estrategia de ramificación que define un modelo estricto de ramas para gestionar features, releases y hotfixes de forma ordenada.

### Las 5 ramas de GitFlow

| Rama | Color | Propósito |
|---|---|---|
| `main` | 🟠 | Código en producción. Solo recibe merges de release y hotfix. **Siempre estable.** |
| `develop` | 🟣 | Integración continua. Base para features. Próxima versión en construcción. |
| `feature/*` | 🔵 | Una rama por funcionalidad. Sale de develop, vuelve a develop via PR. |
| `release/*` | 🟢 | Preparación de versión: bugfixes y docs. Merge a main y develop al cerrar. |
| `hotfix/*` | 🔴 | Corrección urgente en producción. Sale de main, merge a main y develop. |

### Diagrama de flujo

```
main     ●─────────────────────────●──────────────●
          \                       / \             /
develop    ●────●────●────●──────●───●────●────●
                |    |         /      \
feature/A       ●────●        /        \
                              /          \
feature/B            ●────●  /            \
                            /              \
release/1.1               ●────●           |
                                           |
hotfix/bug                               ●────●
```

---

## 🚀 GitFlow Paso a Paso

### Paso 01 — Iniciar el proyecto

```bash
git init
git flow init
# develop se crea automáticamente
# Responde las preguntas de configuración (puedes dejar los defaults)
```

### Paso 02 — Crear una nueva feature

```bash
# Crear rama feature desde develop
git flow feature start login
# → crea y cambia a feature/login

# ... desarrollas tu feature ...
git add .
git commit -m "feat(auth): add login form"

# Cerrar feature: merge a develop y elimina la rama
git flow feature finish login
```

**Sin git-flow instalado:**
```bash
git checkout develop
git checkout -b feature/login
# ... desarrollas ...
git checkout develop
git merge --no-ff feature/login
git branch -d feature/login
```

### Paso 03 — Crear una release

```bash
git flow release start 1.1.0
# → crea release/1.1.0 desde develop

# Corriges bugs menores, actualizas versión en package.json, etc.
git commit -m "chore: bump version to 1.1.0"

# Cerrar release: merge a main Y a develop, crea tag automático
git flow release finish 1.1.0
git push origin main develop --tags
```

### Paso 04 — Hotfix urgente en producción

```bash
git flow hotfix start fix-auth-token
# → crea hotfix/fix-auth-token desde main

# Corriges el bug crítico
git commit -m "fix(auth): correct token expiration logic"

# Cerrar hotfix: merge a main Y develop, crea tag
git flow hotfix finish fix-auth-token
git push origin main develop --tags
```

---

## 💻 Comandos Git Esenciales

### 📁 Repositorio & Configuración

```bash
git init                          # Inicializar repo en carpeta actual
git clone <url>                   # Clonar repositorio remoto
git clone <url> --depth 1         # Clonar solo el último commit (shallow)
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git remote -v                     # Ver repositorios remotos vinculados
git remote add origin <url>       # Vincular repositorio remoto
git status                        # Ver estado de archivos modificados
git log --oneline                 # Historial de commits resumido
git log --oneline --graph --all   # Historial con árbol de ramas
```

### 💾 Stage & Commit

```bash
git add .                         # Agregar todos los cambios al stage
git add <archivo>                 # Agregar archivo específico
git add -p                        # Agregar cambios de forma interactiva (por hunks)
git commit -m "mensaje"           # Confirmar cambios con mensaje
git commit --amend                # Modificar el último commit (sin pushear)
git commit --amend --no-edit      # Agregar cambios al último commit sin editar mensaje
git diff                          # Ver cambios no staged
git diff --staged                 # Ver cambios en stage (listos para commit)
git stash                         # Guardar cambios temporalmente
git stash pop                     # Recuperar cambios guardados
git stash list                    # Ver lista de stashes
```

### 🌿 Ramas (Branches)

```bash
git branch                        # Listar ramas locales
git branch -a                     # Listar ramas locales y remotas
git branch <nombre>               # Crear nueva rama (sin cambiar a ella)
git checkout -b <nombre>          # Crear y cambiar a nueva rama
git switch -c <nombre>            # Crear y cambiar a nueva rama (sintaxis moderna)
git checkout <rama>               # Cambiar a otra rama
git switch <rama>                 # Cambiar a otra rama (sintaxis moderna)
git branch -d <nombre>            # Eliminar rama local (solo si está mergeada)
git branch -D <nombre>            # Eliminar rama local forzado
git push origin --delete <rama>   # Eliminar rama remota
git branch -m <nuevo-nombre>      # Renombrar rama actual
```

### 🔀 Merge, Rebase & Historial

```bash
git merge <rama>                  # Fusionar rama en la actual
git merge --no-ff <rama>          # Merge con commit de merge explícito
git merge --squash <rama>         # Squash todos los commits en uno
git rebase <rama>                 # Reorganizar commits sobre otra rama
git rebase -i HEAD~3              # Rebase interactivo sobre últimos 3 commits
git cherry-pick <hash>            # Aplicar commit específico a rama actual
git revert <hash>                 # Crear commit inverso (deshace cambios, seguro)
git reset --soft HEAD~1           # Deshacer último commit, manteniendo cambios staged
git reset --mixed HEAD~1          # Deshacer último commit, cambios en working dir
git reset --hard HEAD~1           # ⚠️ Deshacer último commit y cambios (destructivo)
```

### 🌐 Remoto (Remote)

```bash
git fetch --all                   # Descargar cambios sin fusionar
git pull origin <rama>            # Traer y fusionar cambios remotos
git pull --rebase origin <rama>   # Traer cambios y rebase (historial limpio)
git push origin <rama>            # Subir rama al repositorio remoto
git push -u origin <rama>         # Subir rama y vincular como upstream
git push --force-with-lease       # Push forzado seguro (falla si alguien hizo push)
git push origin <rama> --tags     # Subir rama y todos los tags
```

### 🏷️ Tags

```bash
git tag                           # Listar todos los tags
git tag v1.0.0                    # Crear tag ligero
git tag -a v1.0.0 -m "Release"   # Crear tag anotado (recomendado)
git push origin --tags            # Subir todos los tags al remoto
git tag -d v1.0.0                 # Eliminar tag local
```

---

## 🔥 Errores Comunes de Hoy

### 1. Merge conflict sin resolver

**Mensaje de error:**
```
CONFLICT (content): Merge conflict in src/auth.js
Automatic merge failed; fix conflicts and then commit the result.
```

**Causa:** Dos ramas modificaron la misma línea. Ocurre al hacer merge o pull sin sincronizar develop primero.

**Solución:**
```bash
git fetch origin
git rebase origin/develop

# Resolver conflictos en el editor (buscar <<<<<<, =======, >>>>>>>)
# Editar el archivo, quitar los marcadores y dejar el código correcto

git add .
git rebase --continue
```

---

### 2. Push forzado en rama compartida

**Mensaje de error:**
```
! [rejected] main → main (non-fast-forward)
hint: Updates were rejected because the tip of your current branch is behind its remote.
```

**Causa:** Se usó `git push --force` en main o develop, sobreescribiendo el historial de otros desarrolladores.

**Solución:**
```bash
# Nunca --force en ramas compartidas (main, develop)
# Usa --force-with-lease: falla si alguien hizo push desde tu último fetch
git push --force-with-lease

# Si el problema es que tu rama está desactualizada:
git pull --rebase origin main
git push origin main
```

---

### 3. Credenciales / Secretos en commits

**El problema:**
```diff
+ API_KEY=sk-prod-abc123xyz
+ DB_PASSWORD=supersecret2024
+ AWS_SECRET=AKIAIOSFODNN7EXAMPLE
```

**Causa:** Se committean archivos `.env` o configs con secretos. Una vez en el historial, son públicos aunque se borren.

**Prevención:**
```bash
# .gitignore — ANTES de hacer el primer commit
.env
.env.local
.env.production
*.key
secrets/
```

**Si ya se commiteó:**
```bash
# Eliminar del historial (destructivo, requiere coordinación del equipo)
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch .env' HEAD

# O usar git-filter-repo (más moderno)
pip install git-filter-repo
git filter-repo --path .env --invert-paths

# Rotar TODOS los secretos comprometidos inmediatamente
```

---

### 4. Deshacer commit ya pusheado

**El problema:**
```bash
# ❌ NUNCA hacer esto en ramas compartidas
git reset --hard HEAD~1
git push --force
# → Destruye el historial de otros desarrolladores
```

**Solución correcta:**
```bash
# ✅ Usar revert: crea un commit inverso (seguro)
git revert <commit-hash>
git push origin main

# El historial queda intacto, solo se añade un commit que deshace el anterior
```

---

### 5. Archivos grandes en el repositorio

**Mensaje de error:**
```
remote: error: File videos/demo.mp4 is 106.50 MB;
exceeds GitHub's file size limit of 100.00 MB
```

**Causa:** Binarios, videos, modelos ML o `node_modules` commiteados por accidente.

**Solución:**
```bash
# Usar Git LFS para binarios grandes
git lfs install
git lfs track "*.mp4" "*.zip" "*.pdf" "*.psd"
git add .gitattributes
git commit -m "chore: add git lfs tracking"

# .gitignore para dependencias
node_modules/
vendor/
__pycache__/
*.pyc
.DS_Store
dist/
build/
```

---

### 6. Rama divergida (diverged)

**Mensaje de error:**
```
Your branch and 'origin/feature/login' have diverged,
and have 3 and 5 different commits each, respectively.
```

**Causa:** La rama local y la remota avanzaron por separado. Ocurre al trabajar en la misma rama desde dos máquinas.

**Solución:**
```bash
git fetch origin

# Opción A: Rebase (historial limpio, recomendado)
git rebase origin/feature/login
git push --force-with-lease

# Opción B: Merge (conserva todos los commits)
git merge origin/feature/login
git push origin feature/login
```

---

## 💡 Pro Tips & Hábitos Esenciales

### 📝 Conventional Commits
Usa el estándar para que los changelogs y semver sean automáticos:

```
feat(scope):     nueva funcionalidad
fix(scope):      corrección de bug
chore(scope):    tareas de mantenimiento
docs(scope):     cambios en documentación
test(scope):     agregar o modificar tests
refactor(scope): refactoring sin cambiar comportamiento
perf(scope):     mejoras de rendimiento
ci(scope):       cambios en CI/CD
```

**Ejemplo completo:**
```bash
git commit -m "feat(auth): add Google OAuth2 login

- Add passport-google-oauth20 strategy
- Create /auth/google and /auth/google/callback routes
- Store user profile in session

Closes #142"
```

### 🔍 Pull Requests pequeños
- PRs de menos de 400 líneas son revisados **2x más rápido**
- Un PR = una funcionalidad o fix
- Divide features grandes en sub-tareas

### 🛡️ Branch Protection Rules
Configura en GitHub/GitLab para proteger `main` y `develop`:
- Requerir al menos 1 review aprobado
- Requerir que el CI pase (tests, lint)
- No permitir push directo (solo via PR)
- Requerir que la rama esté actualizada antes de mergear

### 🔄 Sincroniza seguido
```bash
# Al menos una vez al día en features largas
git pull --rebase origin develop
```

### 🏷️ Tags semánticos
```bash
# Semver: MAJOR.MINOR.PATCH
git tag -a v1.2.3 -m "Release v1.2.3 - Add payment module"
git push origin --tags
```

### 🤖 Git Hooks con Husky
```bash
# Instalar Husky
npm install --save-dev husky

# pre-commit: ejecutar lint y tests rápidos
# .husky/pre-commit
npm run lint && npm run test:unit

# commit-msg: validar conventional commits
# .husky/commit-msg
npx commitlint --edit $1
```

---

## 📋 Referencia rápida — Comandos de rescate

```bash
# ¿Commiteé en la rama equivocada?
git cherry-pick <hash>              # Aplica el commit en la rama correcta
git reset --soft HEAD~1             # Deshace el commit en la rama incorrecta

# ¿Olvidé agregar un archivo al último commit?
git add archivo-olvidado.js
git commit --amend --no-edit

# ¿Necesito descartar todos los cambios locales?
git checkout -- .                   # Descarta cambios en working directory
git clean -fd                       # Elimina archivos sin trackear

# ¿Ver qué cambió en un commit específico?
git show <hash>

# ¿Buscar en qué commit se introdujo un bug?
git bisect start
git bisect bad                      # Commit actual es malo
git bisect good v1.0.0              # Esta versión era buena
# Git hace checkout automático a commits intermedios, tú marcas good/bad
```
