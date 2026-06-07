# 🧪 Testing en Microservicios

> Una estrategia de testing robusta es fundamental para garantizar calidad en sistemas distribuidos. La pirámide de testing guía el balance correcto.

---

## 🔺 La Pirámide de Testing

```
           ▲
          /E2E\          ≈ 5%   — Lentos, costosos, pocos
         /──────\
        / Integr. \      ≈ 15%  — Interacción entre servicios
       /────────────\
      / Componente   \   ≈ 30%  — Servicio en aislamiento
     /────────────────\
    /    Unitarios      \  ≈ 50%  — Rápidos, baratos, muchos
   /──────────────────────\
```

---

## ⚡ Tests Unitarios — 50%

Prueban **funciones y clases de forma aislada**. Son la base de la pirámide: rápidos, baratos y deben ser abundantes.

**Características:**
- Sin dependencias externas (todo mockeado)
- Se ejecutan en milisegundos
- Alta cobertura del código

**Herramientas:** `Jest` · `JUnit` · `Pytest` · `Vitest` · `Go test`

```js
// Ejemplo Jest
describe('calcularIVA', () => {
  it('debe calcular el 21% correctamente', () => {
    expect(calcularIVA(100)).toBe(21);
  });
});
```

---

## 🧩 Tests de Componente — 30%

Prueban un **microservicio completo en aislamiento**, con sus dependencias externas mockeadas (otras APIs, bases de datos).

**Características:**
- Validan el comportamiento del servicio end-to-end internamente
- Dependencias externas simuladas con mocks/stubs
- Más lentos que unitarios pero más realistas

**Herramientas:** `WireMock` · `MockServer` · `Testcontainers`

```java
// WireMock: simula servicio externo
stubFor(get("/users/1")
  .willReturn(okJson("{\"name\": \"Ana\"}")));
```

---

## 🔗 Tests de Integración — 15%

Prueban la **interacción real entre dos o más servicios** o componentes. Incluyen los Contract Tests.

**Características:**
- Usan infraestructura real (BD, brokers)
- Más lentos y frágiles
- Validan que los contratos entre servicios se cumplen

**Herramientas:** `Pact` · `Spring Contract` · `Testcontainers`

---

## 🖥️ Tests E2E (End-to-End) — 5%

Validan **flujos completos del usuario** en un entorno lo más cercano a producción posible.

**Características:**
- Los más costosos de mantener
- Los más lentos de ejecutar
- Usan la UI o la API real del sistema completo

**Herramientas:** `Cypress` · `Playwright` · `Selenium`

```js
// Ejemplo Playwright
test('usuario puede hacer login', async ({ page }) => {
  await page.goto('/login');
  await page.fill('#email', 'user@test.com');
  await page.click('button[type=submit]');
  await expect(page).toHaveURL('/dashboard');
});
```

---

## 🎯 Estrategias especiales en microservicios

### 📜 Contract Testing
Verifica que el **contrato entre consumidor y proveedor** de una API se mantiene válido. Evita breaking changes en producción.

```
Consumidor define: "Necesito { id, name, email }"
Proveedor valida: "Mi respuesta cumple ese contrato" ✓
```

**Herramientas:** `Pact` · `Spring Cloud Contract`

---

### 🎭 Consumer-Driven Contracts
El **consumidor define el contrato** que necesita. El proveedor debe cumplirlo y lo valida automáticamente en su CI.

---

### 🐒 Chaos Testing
Inyecta **fallos deliberados en producción** para validar la resiliencia del sistema y detectar puntos débiles reales.

```
Mata instancias aleatorias → ¿Sigue funcionando? ✓
Introduce latencia artificial → ¿El Circuit Breaker actúa? ✓
```

**Herramientas:** `Chaos Monkey` · `Gremlin` · `LitmusChaos`

---

### 🏋️ Performance Testing
Prueba la **capacidad del sistema bajo carga**. Identifica cuellos de botella antes de que lleguen a producción.

```
Escenario: 1.000 usuarios concurrentes durante 10 min
Métricas:  Latencia p95, p99 · Throughput · Error rate
```

**Herramientas:** `k6` · `Gatling` · `JMeter` · `Locust`

---

## 📊 Métricas objetivo de calidad

| Métrica | Objetivo |
|---|---|
| **Code Coverage** | ≥ 80% |
| **Tiempo tests unitarios** | < 5 segundos |
| **Flaky tests** | 0 (cero tolerancia) |
| **Pipeline CI/CD** | Automático en cada PR |
| **Contract tests** | En cada build del proveedor |

---

## 🚀 Pipeline de testing recomendado

```
PR abierto
    ↓
① Tests unitarios       (< 1 min)
    ↓
② Tests de componente   (< 5 min)
    ↓
③ Contract tests        (< 3 min)
    ↓
④ Tests de integración  (< 15 min)
    ↓
⑤ Deploy a staging
    ↓
⑥ Tests E2E             (< 30 min)
    ↓
⑦ Deploy a producción ✓
```
