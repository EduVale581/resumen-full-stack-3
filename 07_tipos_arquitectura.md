# 🏗️ Tipos de Arquitectura: Front & Back

> Los patrones arquitectónicos que definen cómo se estructura y organiza el software moderno.

---

## 🖥️ Arquitecturas Frontend

### 📄 SPA — Single Page Application

Una sola página HTML que actualiza el DOM dinámicamente con JS. No recarga la página completa al navegar.

**Frameworks:** React · Vue · Angular

```
Browser → index.html (vacío)
        → bundle.js (toda la app)
        → Renderiza en el cliente (JS)
```

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| UX fluida, tipo app nativa | SEO complicado sin SSR |
| Rico en interactividad | Tiempo de carga inicial mayor |
| Fácil de separar de la API | Bundle grande si no se optimiza |

**Úsalo en:** Apps con mucha interacción, dashboards, herramientas tipo Gmail o Notion.

---

### 🖥️ SSR — Server Side Rendering

El servidor genera el HTML completo en cada petición. Mejor SEO y tiempo de primera carga visible.

**Frameworks:** Next.js · Nuxt · Remix · SvelteKit

```
Request → Servidor genera HTML completo
        → HTML listo llega al navegador (hidratado)
```

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| Excelente SEO | Mayor carga en el servidor |
| Primera carga rápida (FCP) | Más complejo de cachear |
| Mejor en conexiones lentas | Requiere servidor Node.js |

**Úsalo en:** E-commerce, blogs, apps con SEO crítico.

---

### 🧊 SSG — Static Site Generation

Las páginas se generan en tiempo de build, no en runtime. Velocidad máxima, sin servidor. Se sirve desde CDN.

**Frameworks:** Astro · Next.js · Gatsby · Hugo

```
Build time: datos → generador → HTML estáticos
Runtime:    CDN sirve los archivos directamente
```

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| Velocidad máxima | Contenido estático (requiere rebuild) |
| Sin servidor necesario | No apto para datos en tiempo real |
| Muy barato de hospedar | Build lento en sitios muy grandes |

**Úsalo en:** Portafolios, documentación, landing pages, blogs.

---

### 🏝️ Islands Architecture

Página mayormente estática con "islas" interactivas. Hidrata solo los componentes que lo necesitan.

**Frameworks:** Astro · Fresh (Deno) · Qwik

```
🟦 HTML estático  (0 JS)
⚡ Isla interactiva (JS mínimo — solo este componente)
🟦 HTML estático  (0 JS)
⚡ Isla carrito   (JS reactivo)
```

**Úsalo en:** Sitios de contenido con componentes interactivos puntuales.

---

### 🧩 Micro Frontends

Divide el frontend en aplicaciones independientes. Cada equipo despliega su UI de forma autónoma.

**Herramientas:** Module Federation (Webpack 5) · single-spa · Qiankun

```
Shell App (contenedor)
├── Team A: Checkout  (React)   → deploy independiente
├── Team B: Catálogo  (Vue)     → deploy independiente
└── Team C: Perfil    (Angular) → deploy independiente
```

**Úsalo en:** Grandes organizaciones, portales corporativos con múltiples equipos autónomos.

---

### 📱 PWA — Progressive Web App

Web app con capacidades nativas: offline, notificaciones push, instalable en el dispositivo sin app store.

**Tecnologías clave:** Service Worker · Web App Manifest · Cache API

```
Service Worker intercepta requests:
├── Cache offline-first
├── Push notificaciones
└── Instalable en el OS del usuario
```

**Úsalo en:** Apps con usuarios móviles, áreas con mala conectividad, reducción de costos de app stores.

---

## ⚙️ Arquitecturas Backend

### 🧱 Monolítica

Toda la aplicación en un único proceso desplegable. Simple al inicio, puede volverse difícil de escalar.

**Frameworks:** Django · Ruby on Rails · Spring MVC · Laravel

```
[ UI + Lógica de negocio + Acceso a datos ] → un solo proceso
DB ←──────────────────────────────────────→ App → HTTP
```

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| Simple de desarrollar | Difícil de escalar partes individuales |
| Fácil de debuggear | Deploy todo o nada |
| Sin latencia de red interna | Riesgo de acoplamiento alto |

**Úsalo en:** MVPs, equipos pequeños, dominio de negocio simple.

---

### ⚡ Microservicios

Servicios pequeños e independientes, cada uno con su propia DB y proceso de despliegue autónomo.

**Frameworks:** Spring Boot · NestJS · FastAPI · Go/Gin

```
Auth ─┐
Pedidos─┼──▶ API Gateway ←── Clientes
Pagos ──┘
Cada servicio: DB propia + deploy independiente
```

**Úsalo en:** Sistemas grandes, alta demanda, múltiples equipos, escalado diferenciado por servicio.

---

### ☁️ Serverless / FaaS

Funciones que ejecutan bajo demanda. Sin gestión de servidores. Pagas solo lo que usas. Escala automáticamente.

**Plataformas:** AWS Lambda · Vercel Functions · Cloudflare Workers · Azure Functions

```
Evento ──▶ fn() ejecuta ──▶ respuesta
Sin servidor activo cuando no hay tráfico
Escala: 0 → ∞ automáticamente
```

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| Sin gestión de infraestructura | Cold starts (latencia inicial) |
| Escalado automático | Límites de tiempo de ejecución |
| Pago por uso | Difícil de testear localmente |

**Úsalo en:** Procesos batch, webhooks, APIs de bajo tráfico o muy variable.

---

### 🔄 Event-Driven

Los servicios se comunican a través de eventos asíncronos. Máximo desacoplamiento entre productor y consumidor.

**Herramientas:** Apache Kafka · RabbitMQ · AWS EventBridge · NATS

```
Productor ──▶ Event Bus (topic)
Bus ──▶ Consumidor A (reacciona)
Bus ──▶ Consumidor B (reacciona)
→ Desacoplados: sin dependencia directa
```

**Úsalo en:** Flujos de alta carga, integraciones complejas, auditoría, sistemas en tiempo real.

---

### 📋 Hexagonal / Ports & Adapters (Clean Architecture)

El dominio de negocio al centro, sin dependencias externas. Los Adapters son intercambiables.

```
       [ HTTP ]    [ CLI ]
           ↕ (Adapters)
[ Puerto ] [ DOMINIO ] [ Puerto ]
           ↕ (Adapters)
       [ DB ]    [ Queue ]
```

**Úsalo en:** Lógica de negocio compleja, alta testabilidad requerida, sistemas con larga vida útil.

---

### 📊 CQRS + Event Sourcing

Separa lecturas de escrituras. El estado se reconstruye reproduciendo eventos inmutables almacenados.

```
Command (escritura) ──▶ Write DB ──▶ Genera Evento ──▶ Event Store
                                                              ↓
Query (lectura) ──▶ Read DB (proyección optimizada) ←─────────
```

**Úsalo en:** Auditoría, sistemas financieros, alta carga de lectura vs escritura.

---

## 📊 Comparativa general

| Dimensión | Frontend | Backend |
|---|---|---|
| **Responsabilidad** | Presentación, UX, estado del cliente | Lógica de negocio, datos, seguridad |
| **Lenguajes** | JS / TS / Dart / WASM | Python, Java, Go, Rust, Ruby, JS/TS |
| **Entorno** | Navegador, móvil, desktop | Servidor, contenedor, función cloud |
| **Tendencia** | Hidratación parcial, Edge rendering | Serverless, Event-driven, WASM |
| **Escalado** | CDN, caché, lazy loading | Horizontal, réplicas, sharding |
