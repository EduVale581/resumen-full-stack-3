# 🌐 API Gateway

> El guardián y orquestador de entrada a tu ecosistema de microservicios. Punto de entrada único para todos los clientes.

---

## 🏗️ Arquitectura

```
        📱 App móvil
        🖥️ Web App
        🔌 3rd Party        ← Todos los clientes
        🤖 IoT / Bot
              ↓ ↓ ↓ ↓
    ┌─────────────────────────────────────┐
    │           🌐 API GATEWAY            │
    │  Auth/JWT · Rate Limit · Routing    │
    │  Load Balancing · SSL · Caché       │
    │  Logging · Transformación de datos  │
    └─────────────────────────────────────┘
              ↓ enruta a...
   ┌────┬────┬────┬────┬────┐
   │Auth│Ped.│Pag.│Cat.│Not.│  ← Microservicios
   │:3001│:3002│:3003│:3004│:3005│
   └────┴────┴────┴────┴────┘
```

---

## ⚙️ ¿Qué hace el API Gateway?

### 🔀 Enrutamiento
Dirige cada request al microservicio correcto según la ruta y método HTTP.

```
GET  /api/users      →  Servicio Auth     :3001
POST /api/orders     →  Servicio Pedidos  :3002
POST /api/payments   →  Servicio Pagos    :3003
GET  /api/products   →  Servicio Catálogo :3004
```

### 🔐 Autenticación & Autorización
Valida tokens JWT o API Keys **antes** de que la petición llegue a los microservicios. Los servicios internos confían en el gateway.

```
Cliente → Gateway (valida JWT) → Servicio ✓
Cliente → Gateway (JWT inválido) → 401 Unauthorized ✗
```

### 🚦 Rate Limiting
Limita el número de requests por cliente/IP para proteger los servicios del abuso.

```
Plan Free:    100 req/min
Plan Pro:   1.000 req/min
Plan Biz:  10.000 req/min
→ 429 Too Many Requests si se supera
```

### ⚡ Caché
Almacena respuestas frecuentes en memoria, reduciendo la carga en los microservicios.

```
Request → Gateway → ¿En caché? → Sí → Responde directo (ms)
                              ↓ No
                          Microservicio → Guarda en caché
```

### ⚖️ Load Balancing
Distribuye el tráfico entre múltiples instancias del mismo microservicio.

```
Gateway → Instancia 1 (33%)
        → Instancia 2 (33%)
        → Instancia 3 (33%)
```

### 🔒 SSL/TLS Termination
Gestiona los certificados HTTPS. Los microservicios internos se comunican en HTTP plano (red interna segura).

---

## 🛠️ Herramientas populares

| Gateway | Descripción | Mejor para |
|---|---|---|
| **Kong** | Open source, plugins extensibles | Producción enterprise |
| **AWS API Gateway** | Managed, integración AWS nativa | Proyectos en AWS |
| **NGINX** | Alto rendimiento, muy configurable | Control total |
| **Traefik** | Auto-discovery con Docker/K8s | Contenedores |
| **Apigee** | Enterprise, analytics avanzados | Grandes empresas |

---

## ⚠️ Anti-patrones a evitar

- **God Gateway**: no pongas lógica de negocio en el gateway
- **Acoplamiento excesivo**: el gateway no debe conocer detalles internos de los servicios
- **Single point of failure**: despliega siempre en alta disponibilidad (mínimo 2 réplicas)
