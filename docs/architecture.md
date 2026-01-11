# Arquitectura del Proyecto: Sistema de Generación de Valores Nietzscheano

**Última actualización:** 2026-01-11  
**Versión:** 1.0

> **⚠️ IMPORTANTE:** Este documento define la estructura completa del proyecto. Debe ser consultado antes de crear cualquier archivo nuevo para mantener la organización y escalabilidad del proyecto.

## Estructura de Carpetas

### Estructura Completa

```
IA-newvalue/
├── .github/                    # Configuración de GitHub (workflows, templates)
│   └── workflows/              # GitHub Actions workflows
├── src/                        # Código fuente principal
│   ├── config/                 # Configuración del sistema
│   │   ├── env.ts             # Variables de entorno
│   │   ├── logger.ts          # Configuración de logging (Pino)
│   │   └── database.ts        # Configuración de conexiones DB
│   ├── types/                  # Tipos TypeScript
│   │   ├── result.ts          # Patrón Result<T, E>
│   │   ├── value.ts           # Tipos de Value
│   │   ├── phase.ts           # Tipos de Phase
│   │   └── index.ts           # Exports centralizados
│   ├── core/                   # Componentes core del sistema
│   │   ├── orchestrator.ts    # Orchestrator principal
│   │   ├── value-engine.ts    # ValueEngine con FSM
│   │   ├── dialectical-system.ts  # Sistema dialéctico
│   │   └── nihilism-monitor.ts    # NihilismMonitor (Observer)
│   ├── modules/                # Módulos de fases
│   │   ├── deconstruction/    # Módulo de deconstrucción genealógica
│   │   │   ├── index.ts
│   │   │   └── genealogist.ts
│   │   ├── nihilistic/        # Módulo de fase nihilista
│   │   │   ├── index.ts
│   │   │   └── nihilism-processor.ts
│   │   ├── creative/          # Módulo de creación de valores
│   │   │   ├── index.ts
│   │   │   └── value-creator.ts
│   │   └── evaluation/        # Módulo de evaluación (eterno retorno)
│   │       ├── index.ts
│   │       └── eternal-return-evaluator.ts
│   ├── agents/                 # Agentes filosóficos
│   │   ├── zarathustra.ts     # Agente Zarathustra
│   │   ├── genealogist.ts     # Agente Genealogist
│   │   ├── dionysus.ts        # Agente Dionysus
│   │   ├── apollo.ts          # Agente Apollo
│   │   ├── last-man.ts        # Agente LastMan
│   │   └── base-agent.ts      # Clase base para agentes
│   ├── llm/                    # Integración con LLM
│   │   ├── client.ts          # Cliente LLM (OpenAI SDK)
│   │   ├── lm-studio.ts       # Adaptador LM Studio
│   │   ├── decorators.ts      # Decorators (cache, retry)
│   │   └── prompts/           # Prompts del sistema
│   │       ├── deconstruction.ts
│   │       ├── nihilistic.ts
│   │       ├── creative.ts
│   │       └── evaluation.ts
│   ├── embeddings/             # Sistema de embeddings
│   │   ├── transformer.ts     # Transformers.js wrapper
│   │   ├── encoder.ts         # Encoder de embeddings
│   │   └── index.ts
│   ├── db/                     # Bases de datos
│   │   ├── postgres/          # PostgreSQL con pgvector
│   │   │   ├── client.ts
│   │   │   ├── schema.ts      # Drizzle schema
│   │   │   └── migrations/   # Migraciones
│   │   ├── neo4j/             # Neo4j graph database
│   │   │   ├── client.ts
│   │   │   └── queries.ts
│   │   └── redis/             # Redis (cache y colas)
│   │       ├── client.ts
│   │       └── cache.ts
│   ├── rag/                    # Sistema RAG
│   │   ├── document-processor.ts  # Procesador de documentos
│   │   ├── chunker.ts         # Chunker de textos
│   │   ├── retriever.ts       # Retriever de embeddings
│   │   └── index.ts
│   ├── monitoring/             # Monitoreo y métricas
│   │   ├── prometheus.ts      # Métricas Prometheus
│   │   ├── metrics.ts         # Definición de métricas
│   │   └── health.ts           # Health checks
│   ├── api/                    # API REST (Fastify)
│   │   ├── server.ts          # Servidor Fastify
│   │   ├── routes/            # Rutas de la API
│   │   │   ├── values.ts      # Endpoints de valores
│   │   │   ├── health.ts      # Health check endpoint
│   │   │   └── index.ts
│   │   ├── middleware/         # Middleware
│   │   │   ├── error-handler.ts
│   │   │   └── logger.ts
│   │   └── types/             # Tipos de la API
│   │       └── requests.ts
│   ├── queues/                 # Colas de procesamiento (BullMQ)
│   │   ├── queue-manager.ts   # Gestor de colas
│   │   ├── jobs/              # Jobs de procesamiento
│   │   │   ├── value-generation.ts
│   │   │   └── index.ts
│   │   └── workers/           # Workers
│   │       └── value-worker.ts
│   ├── utils/                  # Utilidades
│   │   ├── errors.ts          # Manejo de errores
│   │   ├── validation.ts      # Validación
│   │   └── helpers.ts         # Funciones auxiliares
│   └── index.ts                # Entry point principal
├── data/                       # Datos del proyecto
│   ├── corpus/                # Corpus de Nietzsche
│   │   ├── raw/               # Textos originales
│   │   └── processed/         # Textos procesados
│   ├── prompts/               # Prompts del sistema
│   │   ├── deconstruction.md
│   │   ├── nihilistic.md
│   │   ├── creative.md
│   │   └── evaluation.md
│   └── exports/               # Exports de datos generados
├── tests/                      # Tests
│   ├── unit/                  # Tests unitarios
│   │   ├── core/
│   │   ├── modules/
│   │   ├── agents/
│   │   └── utils/
│   ├── integration/           # Tests de integración
│   │   ├── api/
│   │   ├── db/
│   │   └── queues/
│   ├── fixtures/              # Datos de prueba
│   └── helpers/               # Helpers para tests
├── scripts/                    # Scripts de utilidad
│   ├── setup/                 # Scripts de setup
│   ├── migration/             # Scripts de migración
│   └── seed/                  # Scripts de seed
├── docs/                       # Documentación
│   ├── project-context.md     # Contexto del proyecto
│   ├── architecture.md        # Este documento
│   └── api/                   # Documentación de API
│       └── endpoints.md
├── .env.example               # Ejemplo de variables de entorno
├── .gitignore                 # Git ignore
├── package.json               # Dependencias y scripts
├── pnpm-lock.yaml             # Lock file de pnpm
├── tsconfig.json              # Configuración TypeScript
├── tsconfig.build.json        # Configuración TypeScript para build
├── vitest.config.ts           # Configuración Vitest
├── drizzle.config.ts         # Configuración Drizzle ORM
├── prometheus.yml             # Configuración Prometheus
├── docker-compose.yml         # Docker Compose para servicios
├── Dockerfile                 # Dockerfile para la aplicación
└── README.md                   # README principal
```

## Descripción Detallada de Carpetas

### `src/` - Código Fuente Principal

#### `src/config/`
**Propósito:** Configuración centralizada del sistema.

**Archivos:**
- `env.ts`: Carga y validación de variables de entorno
- `logger.ts`: Configuración de logging con Pino
- `database.ts`: Configuración de conexiones a bases de datos

#### `src/types/`
**Propósito:** Definiciones de tipos TypeScript compartidas.

**Archivos:**
- `result.ts`: Implementación del patrón `Result<T, E>` para manejo de errores
- `value.ts`: Tipos relacionados con valores generados
- `phase.ts`: Tipos relacionados con las fases del proceso
- `index.ts`: Exports centralizados de todos los tipos

#### `src/core/`
**Propósito:** Componentes core del sistema que orquestan el proceso.

**Archivos:**
- `orchestrator.ts`: Orquestador principal que coordina las fases
- `value-engine.ts`: Motor de generación de valores con FSM (Máquina de Estados Finitos)
- `dialectical-system.ts`: Sistema dialéctico para el proceso de creación
- `nihilism-monitor.ts`: Monitor que observa y clasifica fases nihilistas (Observer Pattern)

#### `src/modules/`
**Propósito:** Módulos que implementan cada fase del proceso.

**Subcarpetas:**
- `deconstruction/`: Módulo de deconstrucción genealógica
- `nihilistic/`: Módulo de fase nihilista
- `creative/`: Módulo de creación de valores nuevos
- `evaluation/`: Módulo de evaluación con criterio del "eterno retorno"

#### `src/agents/`
**Propósito:** Agentes filosóficos que representan diferentes perspectivas nietzscheanas.

**Archivos:**
- `base-agent.ts`: Clase base para todos los agentes
- `zarathustra.ts`: Agente Zarathustra (perspectiva del superhombre)
- `genealogist.ts`: Agente Genealogist (deconstrucción genealógica)
- `dionysus.ts`: Agente Dionysus (creatividad dionisíaca)
- `apollo.ts`: Agente Apollo (orden y estructura)
- `last-man.ts`: Agente LastMan (perspectiva del último hombre)

#### `src/llm/`
**Propósito:** Integración con modelos de lenguaje.

**Archivos:**
- `client.ts`: Cliente LLM usando OpenAI SDK
- `lm-studio.ts`: Adaptador para LM Studio local
- `decorators.ts`: Decorators para cache y retry
- `prompts/`: Carpeta con prompts específicos por fase

#### `src/embeddings/`
**Propósito:** Sistema de embeddings para RAG.

**Archivos:**
- `transformer.ts`: Wrapper para Transformers.js
- `encoder.ts`: Encoder de embeddings
- `index.ts`: Exports

#### `src/db/`
**Propósito:** Integración con bases de datos.

**Subcarpetas:**
- `postgres/`: PostgreSQL con pgvector (vector database)
- `neo4j/`: Neo4j (graph database)
- `redis/`: Redis (cache y colas)

#### `src/rag/`
**Propósito:** Sistema RAG (Retrieval-Augmented Generation) con corpus de Nietzsche.

**Archivos:**
- `document-processor.ts`: Procesador de documentos
- `chunker.ts`: Chunker de textos para embeddings
- `retriever.ts`: Retriever de embeddings similares
- `index.ts`: Exports

#### `src/monitoring/`
**Propósito:** Monitoreo y métricas del sistema.

**Archivos:**
- `prometheus.ts`: Integración con Prometheus
- `metrics.ts`: Definición de métricas
- `health.ts`: Health checks

#### `src/api/`
**Propósito:** API REST usando Fastify.

**Estructura:**
- `server.ts`: Servidor Fastify principal
- `routes/`: Rutas de la API
- `middleware/`: Middleware (error handling, logging)
- `types/`: Tipos específicos de la API

#### `src/queues/`
**Propósito:** Colas de procesamiento con BullMQ.

**Estructura:**
- `queue-manager.ts`: Gestor de colas
- `jobs/`: Definición de jobs
- `workers/`: Workers que procesan los jobs

#### `src/utils/`
**Propósito:** Utilidades compartidas.

**Archivos:**
- `errors.ts`: Manejo de errores
- `validation.ts`: Validación de datos
- `helpers.ts`: Funciones auxiliares

### `data/` - Datos del Proyecto

#### `data/corpus/`
**Propósito:** Corpus de textos de Nietzsche.

**Subcarpetas:**
- `raw/`: Textos originales sin procesar
- `processed/`: Textos procesados y listos para RAG

#### `data/prompts/`
**Propósito:** Prompts del sistema en formato Markdown.

**Archivos:**
- `deconstruction.md`: Prompts de deconstrucción
- `nihilistic.md`: Prompts de fase nihilista
- `creative.md`: Prompts de creación
- `evaluation.md`: Prompts de evaluación

#### `data/exports/`
**Propósito:** Exports de datos generados por el sistema.

### `tests/` - Tests

#### `tests/unit/`
**Propósito:** Tests unitarios de componentes individuales.

**Estructura:**
- `core/`: Tests de componentes core
- `modules/`: Tests de módulos
- `agents/`: Tests de agentes
- `utils/`: Tests de utilidades

#### `tests/integration/`
**Propósito:** Tests de integración entre componentes.

**Estructura:**
- `api/`: Tests de API
- `db/`: Tests de bases de datos
- `queues/`: Tests de colas

#### `tests/fixtures/`
**Propósito:** Datos de prueba y fixtures.

#### `tests/helpers/`
**Propósito:** Helpers y utilidades para tests.

### `scripts/` - Scripts de Utilidad

#### `scripts/setup/`
**Propósito:** Scripts de configuración inicial del proyecto.

#### `scripts/migration/`
**Propósito:** Scripts de migración de bases de datos.

#### `scripts/seed/`
**Propósito:** Scripts para poblar bases de datos con datos iniciales.

### `docs/` - Documentación

**Archivos:**
- `project-context.md`: Contexto del proyecto (fuente única de verdad)
- `architecture.md`: Este documento (estructura del proyecto)
- `api/endpoints.md`: Documentación de endpoints de la API

## Archivos de Configuración

### `package.json`
**Propósito:** Dependencias y scripts del proyecto.

**Dependencias principales:**
- `fastify`: Framework web
- `openai`: SDK de OpenAI
- `@xenova/transformers`: Embeddings
- `drizzle-orm`: ORM
- `bullmq`: Sistema de colas
- `vitest`: Testing framework
- `pino`: Logging
- `prom-client`: Métricas Prometheus

### `tsconfig.json`
**Propósito:** Configuración TypeScript con modo strict.

**Configuración clave:**
- `strict: true`
- `target: ES2022`
- `module: ESNext`
- `moduleResolution: bundler`

### `tsconfig.build.json`
**Propósito:** Configuración TypeScript específica para builds de producción.

### `vitest.config.ts`
**Propósito:** Configuración de Vitest para tests.

### `drizzle.config.ts`
**Propósito:** Configuración de Drizzle ORM para migraciones y queries.

### `prometheus.yml`
**Propósito:** Configuración de Prometheus para métricas.

### `docker-compose.yml`
**Propósito:** Configuración de servicios con Docker Compose.

**Servicios incluidos:**
- PostgreSQL 15+ con pgvector
- Neo4j 5.x
- Redis 7.x
- Prometheus
- Grafana

### `.env.example`
**Propósito:** Ejemplo de variables de entorno necesarias.

**Variables principales:**
- `DATABASE_URL`: URL de PostgreSQL
- `NEO4J_URI`: URI de Neo4j
- `REDIS_URL`: URL de Redis
- `OPENAI_API_KEY`: API key de OpenAI (o LM Studio)
- `LM_STUDIO_URL`: URL de LM Studio local
- `NODE_ENV`: Entorno (development, production)

### `.gitignore`
**Propósito:** Archivos y carpetas ignorados por Git.

**Incluye:**
- `node_modules/`
- `.env`
- `dist/`
- `build/`
- Logs
- Archivos temporales

## Convenciones de Organización

### Nomenclatura de Archivos

- **Archivos TypeScript:** `kebab-case.ts` (ej: `value-engine.ts`)
- **Carpetas:** `kebab-case` (ej: `value-engine/`)
- **Clases:** `PascalCase` (ej: `ValueEngine`)
- **Funciones/variables:** `camelCase` (ej: `generateValue`)
- **Constantes:** `UPPER_SNAKE_CASE` (ej: `MAX_RETRIES`)

### Estructura de Módulos

Cada módulo debe tener:
- `index.ts`: Exports principales del módulo
- Archivos de implementación con nombres descriptivos
- Tests correspondientes en `tests/`

### Imports

- Usar imports absolutos desde `src/` cuando sea posible
- Agrupar imports: externos, internos, tipos
- Usar `type` para imports de tipos

### Exports

- Cada carpeta debe tener un `index.ts` que exporte los elementos públicos
- Usar named exports en lugar de default exports cuando sea posible

## Flujo de Trabajo con la Estructura

### Crear un Nuevo Módulo

1. Crear carpeta en `src/modules/` o `src/agents/`
2. Crear `index.ts` con exports
3. Implementar archivos necesarios
4. Crear tests en `tests/unit/` o `tests/integration/`
5. Actualizar documentación si es necesario

### Añadir un Nuevo Agente

1. Crear archivo en `src/agents/`
2. Extender `base-agent.ts`
3. Implementar métodos específicos del agente
4. Crear tests en `tests/unit/agents/`
5. Documentar el agente

### Añadir un Nuevo Endpoint de API

1. Crear ruta en `src/api/routes/`
2. Añadir middleware si es necesario
3. Crear tipos en `src/api/types/`
4. Crear tests en `tests/integration/api/`
5. Documentar en `docs/api/endpoints.md`

## Validación de la Estructura

Antes de considerar la estructura completa, verificar:

- [ ] Todas las carpetas principales están definidas
- [ ] Todos los archivos de configuración están identificados
- [ ] La estructura es escalable y mantenible
- [ ] Las convenciones están claramente definidas
- [ ] El flujo de trabajo está documentado

## Próximos Pasos

Una vez validada esta estructura:

1. Crear los archivos de configuración base
2. Inicializar las carpetas principales
3. Configurar las herramientas de desarrollo
4. Comenzar la implementación siguiendo esta estructura

---

**Nota:** Esta estructura debe mantenerse actualizada conforme el proyecto evoluciona. Cualquier cambio significativo debe ser documentado y comunicado al equipo.
