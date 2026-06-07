# 🧩 Arquetipos: Frameworks & Tecnologías

> Los frameworks más utilizados en el ecosistema de desarrollo moderno, organizados por su capa de aplicación y el lenguaje base que los sustenta.

---

## 🖥️ Frontend — Interfaz de Usuario

> Ejecutan en el navegador · Renderizan UI · Gestionan estado

### ⚛️ React
- **Lenguaje:** JavaScript / TypeScript
- **Creado por:** Meta
- **Descripción:** Biblioteca de UI basada en componentes y Virtual DOM. El más popular del mercado.
- **Tags:** `JSX` `Hooks` `SPA` `SSR`

### 💚 Vue.js
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Framework progresivo con curva de aprendizaje suave. Combina lo mejor de React y Angular.
- **Tags:** `Options API` `Composition API` `Nuxt`

### 🔴 Angular
- **Lenguaje:** TypeScript
- **Creado por:** Google
- **Descripción:** Framework completo. Incluye todo de fábrica: routing, forms, HTTP, inyección de dependencias.
- **Tags:** `RxJS` `DI` `Decorators`

### 🟠 Svelte
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Compila a JS vanilla sin runtime. Sin Virtual DOM. El más rápido en rendimiento puro del navegador.
- **Tags:** `Compilado` `SvelteKit` `Reactivo`

### ▲ Next.js
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Meta-framework sobre React. SSR, SSG, ISR y App Router. El estándar para producción con React.
- **Tags:** `SSR` `SSG` `API Routes`

### 📱 React Native
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Desarrollo móvil nativo para iOS y Android usando componentes React. Un código, dos plataformas.
- **Tags:** `iOS` `Android` `Expo`

### 🐦 Flutter
- **Lenguaje:** Dart
- **Creado por:** Google
- **Descripción:** SDK para apps multiplataforma: móvil, web y desktop desde un único codebase.
- **Tags:** `Widgets` `Cross-platform` `Dart`

### 🟦 Astro
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Framework orientado a contenido. Envía 0 JS por defecto. Usa islands architecture para hidratación selectiva.
- **Tags:** `MPA` `Islands` `SSG`

---

## ⚙️ Backend — Lógica de Servidor

> Ejecutan en servidor · Gestionan datos · Exponen APIs

### 🟩 Node.js + Express
- **Lenguaje:** JavaScript / TypeScript
- **Descripción:** Runtime JS en servidor. Express es su framework web minimalista. Ideal para APIs REST rápidas y microservicios.
- **Tags:** `REST` `NPM` `Event Loop`

### 🍃 Spring Boot
- **Lenguaje:** Java / Kotlin
- **Descripción:** El framework Java más usado en enterprise. Ecosistema completo: seguridad, datos, cloud, mensajería.
- **Tags:** `JPA` `Security` `Cloud`

### 🐍 Django
- **Lenguaje:** Python
- **Descripción:** Framework "batteries included". ORM potente, admin auto-generado, autenticación integrada.
- **Tags:** `ORM` `Admin` `MVT`

### ⚡ FastAPI
- **Lenguaje:** Python
- **Descripción:** API framework moderno y rápido con tipado estático. Genera documentación OpenAPI automáticamente.
- **Tags:** `Async` `OpenAPI` `Pydantic`

### 💎 Ruby on Rails
- **Lenguaje:** Ruby
- **Descripción:** Convention over configuration. Productividad extrema para MVPs. ORM ActiveRecord, scaffolding automático.
- **Tags:** `MVC` `ActiveRecord` `Gems`

### 🦄 NestJS
- **Lenguaje:** TypeScript
- **Descripción:** Framework Node.js con arquitectura Angular-like. Módulos, controladores, servicios y DI de fábrica.
- **Tags:** `DI` `Decorators` `Módulos`

### 🦀 Actix / Axum
- **Lenguaje:** Rust
- **Descripción:** Frameworks web en Rust. Rendimiento extremo, seguridad de memoria garantizada y concurrencia sin GC.
- **Tags:** `Async` `Performance` `Safe`

### 🐹 Gin / Fiber
- **Lenguaje:** Go (Golang)
- **Descripción:** Frameworks minimalistas en Go. Concurrencia nativa con goroutines. Compilado y ultraligero para microservicios.
- **Tags:** `Goroutines` `Compilado` `gRPC`

---

## 🌐 Lenguajes más usados

| Lenguaje | Uso principal |
|---|---|
| **JavaScript** | Frontend + Backend (Node.js) |
| **TypeScript** | Frontend + Backend tipado |
| **Python** | Backend + IA / ML / Data |
| **Java** | Backend enterprise, Android |
| **Go** | Backend microservicios, CLI |
| **Rust** | Backend sistemas, WebAssembly |
| **Ruby** | Backend rápido (startups) |
| **Dart** | Móvil / Desktop con Flutter |

---

## 💡 ¿Cuál elegir?

No existe un framework perfecto. La elección depende del equipo, el problema y el contexto.

**Frontend:**
- React → ecosistemas grandes, gran comunidad
- Vue → curva de aprendizaje suave
- Angular → proyectos enterprise
- Svelte → máxima performance

**Backend:**
- Node/NestJS → equipo que ya conoce JS/TS
- Spring Boot → Java enterprise
- FastAPI/Django → equipos Python
- Go/Rust → máxima performance y eficiencia

> 💬 En microservicios, **cada servicio puede usar su propio stack** según sus necesidades específicas.
