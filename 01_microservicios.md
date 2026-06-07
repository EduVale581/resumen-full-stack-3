# 🧩 ¿Qué son los Microservicios?

> Un estilo arquitectónico donde una aplicación se construye como un conjunto de servicios pequeños, independientes y desplegables por separado.

---

## 🧱 Monolito vs ⚡ Microservicios

| | Monolito | Microservicios |
|---|---|---|
| **Estructura** | Todo en un solo proceso | Servicios pequeños e independientes |
| **Despliegue** | Un único deploy gigante | Cada servicio se despliega por separado |
| **Escalado** | Toda la app o nada | Solo el servicio que lo necesita |
| **Tecnología** | Un único stack | Cada servicio elige el suyo |
| **Fallo** | Un error puede tumbar todo | El fallo se aísla en un servicio |

### Ejemplo de un monolito
```
[ UI · Lógica de negocio · Base de datos · Auth · Pagos · Notificaciones · Reportes · Cache ]
                          ↓ Un solo despliegue gigante ↓
```

### Ejemplo de microservicios
```
👤 Auth   |  💳 Pagos   |  📦 Pedidos
🔔 Alertas |  📊 Reports |  🛒 Catálogo
     ↓ Cada uno: deploy, DB y equipo propios ↓
```

---

## ✅ Características clave

### 🔀 Independencia
Cada servicio se despliega, escala y actualiza de forma autónoma sin afectar a los demás.

### ⚙️ Tecnología libre
Cada equipo elige su stack: Node.js, Python, Go, Java… según las necesidades del servicio.

### 📡 Comunicación via API
Los servicios se comunican mediante APIs REST, gRPC o mensajería asíncrona (Kafka, RabbitMQ).

### 🚀 Escalado granular
Solo escalas el servicio que lo necesita, ahorrando recursos e infraestructura.

### 🛡️ Tolerancia a fallos
Si un servicio falla, los demás continúan funcionando. El sistema es resiliente por diseño.

### 👥 Equipos autónomos
Cada equipo es dueño de su servicio completo: desarrollo, despliegue y operación.

---

## 🔄 Ciclo de vida de un microservicio

```
① Diseño  →  ② Desarrollo  →  ③ Testing  →  ④ Contenedor  →  ⑤ Despliegue  →  ⑥ Monitoreo
```

---

## 📡 Formas de comunicación

| Tipo | Protocolo | Cuándo usarlo |
|---|---|---|
| Síncrona | REST / HTTP | Respuesta inmediata requerida |
| Síncrona | gRPC | Alta performance, contratos estrictos |
| Asíncrona | Kafka / RabbitMQ | Eventos, desacoplamiento, alta carga |

---

## ⚠️ Retos a considerar

- **Complejidad operacional**: más servicios = más piezas que gestionar
- **Latencia de red**: las llamadas entre servicios tienen overhead
- **Consistencia de datos**: sin transacciones ACID globales
- **Observabilidad**: logs y trazas distribuidas son más difíciles
- **Testing**: las pruebas de integración son más complejas
