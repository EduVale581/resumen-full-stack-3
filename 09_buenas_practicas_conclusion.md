# ✅ Buenas Prácticas de Programación & Conclusión

> Principios, patrones y hábitos que todo desarrollador debe aplicar para escribir código limpio, mantenible y escalable.

---

## 📐 Principios Fundamentales

### 📖 01 · Código Limpio (Clean Code)

El código se lee más veces de las que se escribe. Nombres claros, funciones pequeñas y sin comentarios obvios.

```js
// ❌ Mal
function fn(x) { return x * 0.21; }

// ✅ Bien
function calcularIVA(precio) {
  const IVA = 0.21;
  return precio * IVA;
}
```

**Reglas clave:**
- Nombres descriptivos para variables, funciones y clases
- Funciones que hacen UNA sola cosa
- Sin comentarios que expliquen código que debería ser autoexplicativo
- Máximo 20 líneas por función

---

### ♻️ 02 · DRY — Don't Repeat Yourself

Cada pieza de conocimiento debe tener una sola representación. Elimina duplicación extrayendo abstracciones.

```js
// ❌ Duplicado
logUser("INFO", "Acceso");
logAdmin("INFO", "Acceso");

// ✅ Abstraído
function log(role, msg) { ... }
log("user", "Acceso");
log("admin", "Acceso");
```

---

### 💎 03 · KISS — Keep It Simple, Stupid

La solución más simple que funciona es la mejor. Evita sobreingeniería. Añade complejidad solo cuando sea necesario.

```js
// ❌ Sobreingeniería
new AbstractFactoryBuilder()
  .withStrategy(new ConcreteStrategy())
  .withObserver(...)
  .build();

// ✅ Simple y directo
const result = processData(input);
```

---

### 🎯 04 · YAGNI — You Aren't Gonna Need It

No implementes funcionalidades especulativas. Construye solo lo que se necesita ahora. El futuro cambia.

```js
// ❌ Especulativo (nadie lo pidió)
function exportToPDF() {}
function exportToExcel() {}
function exportToCSV() {}   // ← este sí es el requerimiento

// ✅ Solo lo necesario
function exportToCSV() {}
```

---

### 🧪 05 · TDD — Test-Driven Development

Escribe el test antes que el código. **Red → Green → Refactor**. Garantiza que el código hace lo que debe hacer.

```js
// 1. RED: escribe el test (falla porque no existe la función)
expect(sumar(2, 3)).toBe(5); // ✗ FAIL

// 2. GREEN: implementa el mínimo para pasar
function sumar(a, b) { return a + b; }
expect(sumar(2, 3)).toBe(5); // ✓ PASS

// 3. REFACTOR: mejora sin romper el test
```

---

### 🌿 06 · Control de Versiones (Git)

Commits pequeños y descriptivos. Ramas por feature. Pull Requests con revisión. Nunca commitear directamente a main.

```bash
# ❌ Mal commit
git commit -m "fixes"

# ✅ Conventional Commits
git commit -m "feat(auth): add JWT refresh token"
git commit -m "fix(api): handle null user response"
git commit -m "docs(readme): update setup instructions"
```

---

## 🏗️ Principios SOLID

Los 5 principios fundamentales del diseño orientado a objetos:

| Letra | Principio | Descripción |
|---|---|---|
| **S** | Single Responsibility | Una clase = una razón para cambiar. Un solo propósito bien definido. |
| **O** | Open / Closed | Abierto a extensión, cerrado a modificación. Extiende sin romper. |
| **L** | Liskov Substitution | Las subclases deben poder reemplazar a su clase base sin romper el programa. |
| **I** | Interface Segregation | Muchas interfaces específicas son mejor que una interfaz general enorme. |
| **D** | Dependency Inversion | Depende de abstracciones, no de implementaciones concretas. |

### Ejemplo: Dependency Inversion

```typescript
// ❌ Mal: depende de implementación concreta
class OrderService {
  private db = new MySQLDatabase(); // acoplado a MySQL
}

// ✅ Bien: depende de abstracción
interface Database { save(data: any): void; }

class OrderService {
  constructor(private db: Database) {} // inyectado, intercambiable
}
```

---

## 🌐 Otras buenas prácticas

### 📁 Estructura de proyecto clara
```
src/
├── controllers/    # Capa de entrada HTTP
├── services/       # Lógica de negocio
├── repositories/   # Acceso a datos
├── models/         # Entidades del dominio
├── utils/          # Utilidades transversales
└── tests/          # Tests espejando la estructura src/
```

### 🔐 Seguridad básica
- Nunca hardcodear secretos en el código
- Usar variables de entorno (`.env`) y nunca commitearlas
- Validar y sanitizar siempre los inputs del usuario
- Principio de mínimo privilegio en permisos

### 📝 Documentación útil
- README claro con: qué es, cómo instalar, cómo ejecutar, cómo testear
- Documentar el "por qué" de decisiones no obvias, no el "qué"
- OpenAPI/Swagger para APIs

### 🔍 Code Review efectivo
- Revisar lógica, no solo syntax
- Comentarios constructivos y específicos
- PRs pequeños (< 400 líneas) son revisados mejor y más rápido

---

## 🏁 Conclusión: El camino del desarrollador moderno

A lo largo de esta guía hemos recorrido el ecosistema completo del desarrollo moderno:

| Tema | Concepto clave |
|---|---|
| **Microservicios** | Desacopla servicios para escalar de forma independiente y con resiliencia |
| **Arquetipos / Frameworks** | Elige según el equipo, el problema y el contexto — no solo por popularidad |
| **Patrones de diseño** | Circuit Breaker, CQRS, Saga… soluciones probadas a problemas conocidos |
| **API Gateway** | Un punto de entrada, múltiples servicios. Seguridad y routing centralizado |
| **Database per Service** | Autonomía de datos = autonomía de equipos. La DB correcta para cada caso |
| **Testing** | Pirámide de tests: muchos unitarios, algunos integración, pocos E2E |
| **Arquitecturas** | SPA, SSR, Serverless, Event-Driven… cada una tiene su momento |
| **Buenas prácticas** | SOLID, DRY, KISS, YAGNI y código limpio son la base de todo buen sistema |

---

> 💬 *"La arquitectura no es sobre tecnología. Es sobre decisiones de negocio."*

Ninguna tecnología es una bala de plata. El conocimiento profundo de los principios te permite **elegir la herramienta correcta para cada problema**, en lugar de adaptar el problema a la herramienta que conoces.

El mejor código es el que tu equipo puede leer, entender, modificar y desplegar con confianza — hoy y dentro de dos años.
