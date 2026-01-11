# Sistema de Generación de Valores Nietzscheano

Sistema de IA experimental que genera valores filosóficos nuevos mediante un proceso de cuatro fases inspirado en la filosofía de Nietzsche.

## Descripción

Este proyecto implementa un sistema de generación de valores filosóficos que utiliza:

1. **Deconstrucción genealógica** de conceptos morales existentes
2. **Fase nihilista** (vacío conceptual necesario)
3. **Creación de valores genuinamente nuevos**
4. **Evaluación** con criterio del "eterno retorno"

## Características

- Sistema multi-agente con personajes nietzscheanos (Zarathustra, Genealogist, Dionysus, Apollo, LastMan)
- RAG (Retrieval-Augmented Generation) con corpus de Nietzsche
- API REST para interacción con el sistema
- Procesamiento en background mediante colas
- Monitoreo y métricas con Prometheus

## Stack Tecnológico

- **Runtime:** Node.js 20 LTS
- **Lenguaje:** TypeScript 5.3+ (strict mode)
- **Package Manager:** pnpm
- **Backend:** Fastify, OpenAI SDK, Transformers.js, Drizzle ORM, BullMQ
- **Bases de Datos:** PostgreSQL 15+ (pgvector), Neo4j 5.x, Redis 7.x
- **Testing:** Vitest
- **Infraestructura:** Docker Compose

## Estado del Proyecto

**Fase actual:** Planificación y diseño arquitectónico

El proyecto está en fase inicial de planificación. La estructura y arquitectura están siendo definidas antes de comenzar la implementación.

## Estructura del Proyecto

```
IA-newvalue/
├── src/          # Código fuente principal
├── data/         # Datos (corpus de Nietzsche, prompts, exports)
├── tests/        # Tests (unit, integration)
├── scripts/      # Scripts de utilidad
└── docs/         # Documentación
```

## Documentación

- [Contexto del Proyecto](./docs/project-context.md) - Contexto completo del proyecto
- [Arquitectura](./docs/architecture.md) - Estructura y arquitectura del sistema

## Repositorio

- **GitHub:** https://github.com/rflvz/nietzsche-ai

## Licencia

[Por definir]

---

**Nota:** Este proyecto está en fase de desarrollo activo. La documentación se actualizará a medida que el proyecto evolucione.
