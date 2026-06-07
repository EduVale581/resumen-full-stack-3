# 🗃️ Database per Service Pattern

> Cada microservicio es dueño exclusivo de su propia base de datos. Ningún otro servicio puede acceder directamente a ella — solo a través de la API del servicio.

---

## ❌ Problema: Base de datos compartida

```
👤 Auth ──┐
📦 Pedidos─┼──▶ 🗃️ Base de datos única
💳 Pagos ──┘

Problema: cambios en el schema afectan a TODOS los servicios
```

**Consecuencias:**
- Un cambio de schema puede romper múltiples servicios
- Los servicios quedan acoplados a través de la base de datos
- No puedes escalar solo el servicio que lo necesita
- Imposible elegir la tecnología óptima para cada caso

---

## ✅ Solución: Database per Service

```
👤 Auth       →  🐘 PostgreSQL  (datos relacionales, ACID)
📦 Pedidos    →  🍃 MongoDB     (documentos JSON flexibles)
💳 Pagos      →  🐬 MySQL       (transacciones financieras)
🔔 Notif.     →  ⚡ Redis        (caché en memoria, velocidad)
```

**Regla de oro:** Ningún servicio puede acceder directamente a la DB de otro. Toda comunicación es a través de la API.

---

## 🏛️ Libertad de elección tecnológica

| Base de datos | Tipo | Cuándo usarla |
|---|---|---|
| **PostgreSQL** | Relacional | Transacciones ACID, datos estructurados, integridad referencial |
| **MongoDB** | Documental | Esquema flexible, documentos JSON, datos heterogéneos |
| **Redis** | Cache / KV | Alta velocidad, sesiones, colas, pub/sub |
| **Neo4j** | Grafos | Relaciones complejas, redes sociales, recomendaciones |
| **Cassandra** | Columnar | Alta disponibilidad, escrituras masivas, distribución global |
| **Elasticsearch** | Búsqueda | Full-text search, logs, analytics en tiempo real |

---

## ✅ Beneficios clave

### 🔒 Encapsulamiento total
El servicio controla completamente su modelo de datos. Puedes cambiar el schema, migrar de DB o reestructurar tablas sin impactar otros servicios.

### 📈 Escalabilidad independiente
Escala solo la base de datos del servicio que está bajo demanda. Si el servicio de catálogo tiene picos, solo escala ese.

### 🛠️ Tecnología óptima para cada caso
Elige la base de datos más adecuada para el patrón de acceso de cada servicio. No fuerces todos los datos en una sola tecnología.

### 🛡️ Aislamiento de fallos
Un problema de rendimiento en la DB de un servicio no degrada a los demás.

---

## ⚠️ Retos y cómo abordarlos

### Transacciones distribuidas
Sin ACID global, usa el **patrón Saga** para mantener consistencia eventual entre servicios.

```
Saga: Crea orden → Reserva stock → Cobra pago
      ↩ Compensar automáticamente si algo falla
```

### Datos compartidos / duplicados
Acepta que algunos datos se replican entre servicios. Es el precio del desacoplamiento. La consistencia eventual es la norma.

### Consultas que cruzan servicios
Usa un **API Aggregator** o el patrón **BFF** (Backend for Frontend) para combinar datos de múltiples servicios en el nivel de aplicación.

---

## 📐 Reglas de diseño

1. **Un servicio = una base de datos** (o schema aislado como mínimo)
2. **Nunca acceso directo** a la DB de otro servicio
3. **Toda comunicación** es a través de APIs o eventos
4. **La DB es un detalle de implementación** — puede cambiar sin afectar a otros
