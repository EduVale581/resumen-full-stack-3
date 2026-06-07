# 🧩 Patrones de Diseño en Microservicios

> Soluciones probadas para problemas recurrentes en arquitecturas distribuidas.

---

## 🛡️ Resiliencia — Fallos y tolerancia

### ⚡ Circuit Breaker
Detiene llamadas a un servicio fallido para evitar una cascada de errores. Tiene tres estados: **cerrado** (normal), **abierto** (bloqueando llamadas) y **semiabierto** (probando recuperación).

```
Estado: OPEN → Fallback activado
Después de timeout → Estado: HALF-OPEN → prueba
Si OK → Estado: CLOSED (vuelve a la normalidad)
```

**Herramientas:** Resilience4j, Hystrix, Polly

---

### 🔄 Retry Pattern
Reintenta automáticamente operaciones fallidas con **backoff exponencial** para evitar sobrecargar el servicio destino.

```
Intento 1 → falla
Intento 2 (espera 2s) → falla
Intento 3 (espera 4s) → ✓ éxito
```

**Herramientas:** Resilience4j, Polly, axios-retry

---

### 🛡️ Bulkhead
Aísla recursos entre servicios (hilos, conexiones) para que el fallo de uno **no consuma los recursos de otros**.

```
Pool A: 10 threads  →  Servicio A (aislado)
Pool B: 10 threads  →  Servicio B (aislado)
```

**Herramientas:** Resilience4j, Hystrix

---

## 🗃️ Datos — Consistencia y estado

### 📝 Saga Pattern
Gestiona **transacciones distribuidas** como una serie de transacciones locales con compensaciones en caso de fallo.

```
Crea orden → Reserva stock → Cobra pago
      ↩ Compensar si alguno falla
```

**Tipos:** Coreografía (eventos) · Orquestación (saga orchestrator)

---

### 🗂️ CQRS (Command Query Responsibility Segregation)
Separa las operaciones de **escritura** (Commands) de las de **lectura** (Queries) usando modelos y bases de datos distintas.

```
Write DB  →  Genera eventos
              ↓
           Read DB (optimizada para consultas)
```

**Herramientas:** Axon Framework, MediatR, EventStoreDB

---

### 📡 Event Sourcing
El estado de la aplicación se determina **reproduciendo una secuencia de eventos** inmutables almacenados.

```
Evento1 + Evento2 + Evento3 = Estado actual reconstruido
```

**Beneficios:** Auditoría completa, reproducción de estado, debugging en el tiempo

---

## 📡 Comunicación — Integración y migración

### 🎭 Sidecar
Despliega capacidades auxiliares (logging, proxy, seguridad) como **contenedor separado** junto al servicio principal.

```
[App Container] + [Sidecar: Envoy] → Service Mesh
```

**Herramientas:** Envoy, Istio, Linkerd

---

### 🔍 Service Discovery
Los servicios se registran y localizan **dinámicamente** sin IPs hardcodeadas.

```
Servicio A → Registry: "¿Dónde está Servicio B?"
Registry  → ip:port dinámico
```

**Tipos:** Client-side (Eureka) · Server-side (AWS ALB, Consul)

---

### 🚦 Strangler Fig
Migra gradualmente un monolito a microservicios **reemplazando funcionalidades una a una**, sin big bang.

```
Monolito  → 80% del tráfico
Micro nuevo → 20% del tráfico
→ Incrementar gradualmente hasta 0/100%
```

---

## 📊 Resumen por categoría

| Categoría | Patrón | Problema que resuelve |
|---|---|---|
| Resiliencia | Circuit Breaker | Cascada de fallos |
| Resiliencia | Retry | Fallos transitorios |
| Resiliencia | Bulkhead | Agotamiento de recursos |
| Datos | Saga | Transacciones distribuidas |
| Datos | CQRS | Lecturas/escrituras desbalanceadas |
| Datos | Event Sourcing | Auditoría y trazabilidad |
| Comunicación | Sidecar | Capacidades transversales |
| Comunicación | Service Discovery | Localización dinámica |
| Comunicación | Strangler Fig | Migración incremental |
