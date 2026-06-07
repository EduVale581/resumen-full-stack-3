# 📚 Guía de Arquitectura & Desarrollo de Software

> Documentación completa sobre microservicios, arquitecturas, frameworks, patrones de diseño y buenas prácticas para el desarrollo moderno.

---

## 📖 Contenido

| # | Tema | Descripción |
|---|---|---|
| 01 | [Microservicios](./01_microservicios.md) | Qué son, comparativa con monolitos y ciclo de vida |
| 02 | [Arquetipos — Frameworks](./02_arquetipos.md) | Frameworks Frontend y Backend con sus lenguajes |
| 03 | [Patrones de Diseño](./03_patrones_diseno.md) | Circuit Breaker, CQRS, Saga, Sidecar y más |
| 04 | [API Gateway](./04_api_gateway.md) | Enrutamiento, autenticación, rate limiting y caché |
| 05 | [Database per Service](./05_database_per_service.md) | Patrón de base de datos por microservicio |
| 06 | [Testing](./06_testing.md) | Pirámide de tests, contract testing y chaos testing |
| 07 | [Tipos de Arquitectura](./07_tipos_arquitectura.md) | SPA, SSR, SSG, Serverless, Hexagonal y más |
| 08 | [GitFlow & Git](./08_gitflow_comandos_errores.md) | Modelo de ramas, comandos esenciales y errores comunes |
| 09 | [Buenas Prácticas & Conclusión](./09_buenas_practicas_conclusion.md) | SOLID, DRY, KISS, YAGNI, TDD y cierre general |

---

## 🚀 Cómo usar esta guía

Esta guía está pensada para ser leída de forma **progresiva** (del 01 al 09) o como **referencia puntual** según el tema que necesites.

```
Nuevo en el tema → Lee del 01 al 09 en orden
Referencia rápida → Salta directamente al documento que necesitas
Onboarding equipo → Comparte el repositorio completo
```

---

## 🗺️ Mapa conceptual

```
                    ┌─────────────────┐
                    │  MICROSERVICIOS │
                    └────────┬────────┘
                             │
          ┌──────────────────┼──────────────────┐
          ▼                  ▼                  ▼
    ┌──────────┐      ┌──────────────┐    ┌──────────┐
    │Frameworks│      │  Patrones de │    │API Gateway│
    │Front/Back│      │   Diseño     │    │           │
    └──────────┘      └──────────────┘    └──────────┘
          │                  │                  │
          ▼                  ▼                  ▼
    ┌──────────┐      ┌──────────────┐    ┌──────────┐
    │Arquitec- │      │Database per  │    │ Testing  │
    │turas     │      │Service       │    │          │
    └──────────┘      └──────────────┘    └──────────┘
                             │
                    ┌────────┴────────┐
                    ▼                 ▼
             ┌──────────┐    ┌──────────────┐
             │  GitFlow │    │   Buenas     │
             │  & Git   │    │  Prácticas   │
             └──────────┘    └──────────────┘
```

---

## 📄 Licencia

MIT — Libre para usar y compartir con atribución.
