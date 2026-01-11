# Arquitectura del Proyecto: Sistema de Generación de Valores Nietzscheano

**Última actualización:** 2026-01-11  
**Versión:** 1.0

> **⚠️ IMPORTANTE:** Este documento define la estructura completa del proyecto, incluyendo organización de carpetas, archivos de configuración y convenciones. Debe ser consultado antes de crear cualquier archivo nuevo en el proyecto.

## Introducción

Este documento describe la arquitectura y estructura completa del Sistema de Generación de Valores Nietzscheano. El proyecto implementa un sistema de IA experimental que genera valores filosóficos nuevos mediante un proceso de cuatro fases inspirado en la filosofía de Nietzsche.

### Propósito del Documento

- Definir la estructura completa de directorios y archivos del proyecto
- Identificar todos los archivos de configuración necesarios
- Establecer convenciones de organización y nomenclatura
- Guiar la implementación futura del proyecto

### Visión General de la Arquitectura

El sistema está organizado en módulos funcionales que implementan:
1. **Deconstrucción genealógica** de conceptos morales existentes
2. **Fase nihilista** (vacío conceptual necesario)
3. **Creación de valores genuinamente nuevos**
4. **Evaluación** con criterio del "eterno retorno"

La arquitectura utiliza:
- Sistema multi-agente con personajes nietzscheanos
- RAG (Retrieval-Augmented Generation) con corpus de Nietzsche
- Procesamiento en background mediante colas
- API REST para interacción externa
- Monitoreo y métricas con Prometheus

## Estructura de Directorios

### Árbol Completo de Directorios

```
IA-newvalue/
├── src/                          # Código fuente principal
│   ├── config/                   # Configuración del sistema
│   │   ├── env.ts                # Variables de entorno
│   │   ├── logger.ts             # Configuración de logging (Pino)
│   │   └── database.ts           # Configuración de conexiones DB
│   ├── types/                    # Tipos TypeScript compartidos
│   │   ├── result.ts             # Tipo Result<T, E> para errores
│   │   ├── value.ts              # Tipos relacionados con valores
│   │   ├── phase.ts              # Tipos de fases del proceso
│   │   └── index.ts              # Exports centralizados
│   ├── core/                     # Componentes core del sistema
│   │   ├── orchestrator.ts        # Orchestrator principal
│   │   ├── value-engine.ts        # ValueEngine con FSM
│   │   ├── dialectical-system.ts  # Sistema dialéctico
│   │   ├── nihilism-monitor.ts    # Monitor de nihilismo (Observer)
│   │   └── index.ts
│   ├── modules/                  # Módulos de las 4 fases
│   │   ├── deconstruction/       # Módulo de deconstrucción
│   │   │   ├── deconstruction.ts
│   │   │   └── index.ts
│   │   ├── nihilistic/           # Módulo nihilista
│   │   │   ├── nihilistic.ts
│   │   │   └── index.ts
│   │   ├── creative/             # Módulo creativo
│   │   │   ├── creative.ts
│   │   │   └── index.ts
│   │   └── evaluation/           # Módulo de evaluación
│   │       ├── evaluation.ts
│   │       └── index.ts
│   ├── agents/                   # Agentes filosóficos nietzscheanos
│   │   ├── zarathustra.ts         # Agente Zarathustra
│   │   ├── genealogist.ts         # Agente Genealogist
│   │   ├── dionysus.ts            # Agente Dionysus
│   │   ├── apollo.ts              # Agente Apollo
│   │   ├── last-man.ts            # Agente LastMan
│   │   └── index.ts
│   ├── llm/                      # Integración con LLM
│   │   ├── openai-client.ts        # Cliente OpenAI SDK
│   │   ├── lm-studio-client.ts     # Cliente LM Studio local
│   │   ├── decorators.ts          # Decorators (cache, retry)
│   │   └── index.ts
│   ├── embeddings/               # Sistema de embeddings
│   │   ├── transformer-client.ts  # Cliente Transformers.js
│   │   ├── embedding-service.ts   # Servicio de embeddings
│   │   └── index.ts
│   ├── db/                       # Bases de datos
│   │   ├── postgres/              # PostgreSQL con pgvector
│   │   │   ├── connection.ts
│   │   │   ├── schema.ts          # Schema Drizzle
│   │   │   └── migrations/
│   │   ├── neo4j/                 # Neo4j graph database
│   │   │   ├── connection.ts
│   │   │   └── queries.ts
│   │   └── redis/                # Redis (cache y colas)
│   │       ├── connection.ts
│   │       └── cache.ts
│   ├── rag/                      # Sistema RAG
│   │   ├── document-processor.ts  # Procesador de documentos
│   │   ├── chunker.ts             # Chunker de texto
│   │   ├── retriever.ts           # Retriever de embeddings
│   │   └── index.ts
│   ├── monitoring/                # Monitoreo y métricas
│   │   ├── prometheus.ts          # Métricas Prometheus
│   │   ├── metrics.ts             # Definición de métricas
│   │   └── index.ts
│   ├── api/                       # API REST (Fastify)
│   │   ├── server.ts              # Servidor Fastify
│   │   ├── routes/                # Rutas de la API
│   │   │   ├── values.ts          # Rutas de valores
│   │   │   ├── health.ts          # Health check
│   │   │   └── index.ts
│   │   ├── middleware/            # Middleware
│   │   │   ├── error-handler.ts
│   │   │   └── logger.ts
│   │   └── index.ts
│   ├── queues/                   # Colas de procesamiento (BullMQ)
│   │   ├── queue-config.ts        # Configuración de colas
│   │   ├── value-generation-job.ts # Job de generación
│   │   └── index.ts
│   └── utils/                    # Utilidades compartidas
│       ├── validation.ts
│       ├── formatting.ts
│       └── index.ts
├── data/                         # Datos del proyecto
│   ├── corpus/                   # Corpus de Nietzsche
│   │   ├── texts/                # Textos originales
│   │   └── processed/            # Textos procesados
│   ├── prompts/                  # Prompts del sistema
│   │   ├── deconstruction/
│   │   ├── nihilistic/
│   │   ├── creative/
│   │   └── evaluation/
│   └── exports/                  # Exports y datos generados
│       └── values/               # Valores generados
├── tests/                        # Tests
│   ├── unit/                     # Tests unitarios
│   │   ├── core/
│   │   ├── modules/
│   │   ├── agents/
│   │   └── utils/
│   ├── integration/              # Tests de integración
│   │   ├── api/
│   │   ├── db/
│   │   └── queues/
│   └── fixtures/                 # Fixtures y datos de prueba
│       ├── values.ts
│       └── corpus.ts
├── scripts/                      # Scripts de utilidad
│   ├── setup/                    # Scripts de configuración
│   │   ├── init-db.ts
│   │   └── seed-data.ts
│   ├── migration/                # Scripts de migración
│   │   └── run-migrations.ts
│   └── seed/                      # Scripts de seed
│       └── seed-corpus.ts
├── docs/                         # Documentación
│   ├── architecture.md           # Este documento
│   ├── project-context.md        # Contexto del proyecto
│   └── api/                      # Documentación de API
│       └── endpoints.md
├── .github/                      # Configuración de GitHub
│   └── workflows/                # GitHub Actions
│       ├── ci.yml                # CI/CD
│       └── test.yml
└── [archivos de configuración en raíz]
```

## Estructura Detallada de `src/`

### `src/config/`

**Propósito:** Configuración centralizada del sistema.

**Archivos:**
- `env.ts` - Carga y validación de variables de entorno
- `logger.ts` - Configuración de Pino logger
- `database.ts` - Configuración de conexiones a PostgreSQL, Neo4j y Redis

**Responsabilidades:**
- Cargar variables de entorno desde `.env`
- Validar configuración al inicio
- Exportar configuración tipada para el resto del sistema

### `src/types/`

**Propósito:** Tipos TypeScript compartidos en todo el proyecto.

**Archivos:**
- `result.ts` - Tipo `Result<T, E>` para manejo funcional de errores
- `value.ts` - Tipos `Value`, `ValuePhase`, `ValueMetadata`
- `phase.ts` - Tipos `Phase`, `PhaseState`, `PhaseTransition`
- `index.ts` - Exports centralizados

**Convenciones:**
- Todos los tipos deben ser exportados desde `index.ts`
- Usar tipos estrictos, evitar `any`
- Documentar tipos complejos con JSDoc

### `src/core/`

**Propósito:** Componentes core que orquestan el sistema.

**Componentes principales:**
- **Orchestrator** - Coordina el flujo completo de generación de valores
- **ValueEngine** - Motor principal con FSM para gestionar estados
- **DialecticalSystem** - Sistema dialéctico para síntesis de ideas
- **NihilismMonitor** - Monitor que observa y clasifica fases nihilistas (Observer pattern)

**Relaciones:**
- `Orchestrator` usa `ValueEngine` para gestionar el proceso
- `ValueEngine` coordina los módulos de fases
- `NihilismMonitor` observa todas las fases para detectar nihilismo
- `DialecticalSystem` proporciona síntesis dialéctica

### `src/modules/`

**Propósito:** Módulos que implementan las 4 fases del proceso.

**Módulos:**
1. **deconstruction/** - Deconstrucción genealógica de valores existentes
2. **nihilistic/** - Fase nihilista (vacío conceptual)
3. **creative/** - Creación de valores nuevos
4. **evaluation/** - Evaluación con criterio del "eterno retorno"

**Estructura de cada módulo:**
- Archivo principal con la lógica del módulo
- `index.ts` para exports
- Cada módulo recibe input del módulo anterior
- Cada módulo produce output para el siguiente

### `src/agents/`

**Propósito:** Agentes filosóficos con diferentes perspectivas nietzscheanas.

**Agentes:**
- **Zarathustra** - Perspectiva del superhombre, creación de valores
- **Genealogist** - Análisis genealógico de valores
- **Dionysus** - Perspectiva dionisíaca, creatividad y caos
- **Apollo** - Perspectiva apolínea, orden y forma
- **LastMan** - Perspectiva del último hombre, mediocridad

**Responsabilidades:**
- Cada agente tiene su propia perspectiva filosófica
- Los agentes participan en diferentes fases del proceso
- Los agentes generan contenido usando LLM con prompts específicos

### `src/llm/`

**Propósito:** Integración con modelos de lenguaje.

**Componentes:**
- `openai-client.ts` - Cliente para OpenAI API
- `lm-studio-client.ts` - Cliente para LM Studio local
- `decorators.ts` - Decorators para cache y retry

**Características:**
- Decorators para cache de respuestas
- Decorators para retry automático
- Abstracción común para ambos clientes

### `src/embeddings/`

**Propósito:** Sistema de embeddings para RAG.

**Componentes:**
- `transformer-client.ts` - Cliente Transformers.js
- `embedding-service.ts` - Servicio que genera embeddings

**Responsabilidades:**
- Generar embeddings de texto usando Transformers.js
- Procesar corpus de Nietzsche para embeddings
- Proporcionar embeddings para búsqueda semántica

### `src/db/`

**Propósito:** Integración con bases de datos.

**Bases de datos:**
- **postgres/** - PostgreSQL 15+ con pgvector para vectores
- **neo4j/** - Neo4j 5.x para relaciones gráficas
- **redis/** - Redis 7.x para cache y colas

**Estructura:**
- Cada base de datos tiene su carpeta con `connection.ts`
- PostgreSQL usa Drizzle ORM con schema en `schema.ts`
- Migraciones en `postgres/migrations/`

### `src/rag/`

**Propósito:** Sistema RAG (Retrieval-Augmented Generation).

**Componentes:**
- `document-processor.ts` - Procesa documentos del corpus
- `chunker.ts` - Divide texto en chunks
- `retriever.ts` - Recupera chunks relevantes usando embeddings

**Flujo:**
1. Procesar corpus de Nietzsche
2. Generar embeddings de chunks
3. Almacenar en PostgreSQL con pgvector
4. Recuperar chunks relevantes para contexto

### `src/monitoring/`

**Propósito:** Monitoreo y métricas del sistema.

**Componentes:**
- `prometheus.ts` - Configuración de Prometheus
- `metrics.ts` - Definición de métricas

**Métricas a rastrear:**
- Número de valores generados
- Tiempo de procesamiento por fase
- Frecuencia de fases nihilistas
- Errores y excepciones

### `src/api/`

**Propósito:** API REST para interacción externa.

**Estructura:**
- `server.ts` - Servidor Fastify principal
- `routes/` - Rutas de la API
  - `values.ts` - Endpoints para valores
  - `health.ts` - Health check
- `middleware/` - Middleware personalizado
  - `error-handler.ts` - Manejo de errores
  - `logger.ts` - Logging de requests

**Endpoints principales:**
- `POST /api/values/generate` - Generar nuevo valor
- `GET /api/values/:id` - Obtener valor por ID
- `GET /api/health` - Health check

### `src/queues/`

**Propósito:** Procesamiento en background con BullMQ.

**Componentes:**
- `queue-config.ts` - Configuración de colas
- `value-generation-job.ts` - Job para generación de valores

**Uso:**
- Generación de valores se procesa en background
- Colas Redis para gestión de jobs
- Retry automático en caso de fallos

### `src/utils/`

**Propósito:** Utilidades compartidas.

**Utilidades:**
- `validation.ts` - Validación de datos
- `formatting.ts` - Formateo de texto y datos

## Archivos de Configuración

### Configuración de Node.js/TypeScript

#### `package.json`

**Propósito:** Dependencias y scripts del proyecto.

**Dependencias principales:**
- **Runtime:** Node.js 20 LTS
- **Lenguaje:** TypeScript 5.3+
- **Package Manager:** pnpm

**Dependencias de producción:**
- `fastify` - Framework web
- `@openai/api` - OpenAI SDK
- `@xenova/transformers` - Transformers.js para embeddings
- `drizzle-orm` - ORM para PostgreSQL
- `drizzle-kit` - CLI para Drizzle
- `bullmq` - Sistema de colas
- `ioredis` - Cliente Redis
- `neo4j-driver` - Driver Neo4j
- `pg` y `pgvector` - PostgreSQL con vectores
- `pino` - Logging
- `prom-client` - Métricas Prometheus

**Dependencias de desarrollo:**
- `typescript` - Compilador TypeScript
- `vitest` - Framework de testing
- `@types/node` - Tipos de Node.js
- `tsx` - Ejecutar TypeScript directamente

**Scripts principales:**
- `dev` - Ejecutar en modo desarrollo
- `build` - Compilar TypeScript
- `test` - Ejecutar tests
- `test:watch` - Tests en modo watch
- `lint` - Linter
- `migrate` - Ejecutar migraciones

#### `tsconfig.json`

**Propósito:** Configuración de TypeScript en modo strict.

**Configuración clave:**
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "lib": ["ES2022"],
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "tests"]
}
```

#### `tsconfig.build.json`

**Propósito:** Configuración específica para build de producción.

**Extiende:** `tsconfig.json` con configuraciones optimizadas para producción.

### Configuración de Testing

#### `vitest.config.ts`

**Propósito:** Configuración de Vitest para tests.

**Configuración:**
- Paths para imports
- Setup de tests
- Coverage configuration
- Entorno de testing

#### `vitest.setup.ts`

**Propósito:** Setup global para tests.

**Incluye:**
- Mocks globales
- Configuración de entorno de test
- Helpers compartidos

### Configuración de Base de Datos

#### `drizzle.config.ts`

**Propósito:** Configuración de Drizzle ORM.

**Configuración:**
- Conexión a PostgreSQL
- Ubicación de schema
- Ubicación de migraciones
- Output de migraciones

#### `docker-compose.yml`

**Propósito:** Servicios Docker para desarrollo local.

**Servicios:**
- **postgres** - PostgreSQL 15+ con extensión pgvector
- **neo4j** - Neo4j 5.x graph database
- **redis** - Redis 7.x para cache y colas
- **prometheus** - Prometheus para métricas
- **grafana** - Grafana para visualización

**Puertos:**
- PostgreSQL: 5432
- Neo4j: 7474 (HTTP), 7687 (Bolt)
- Redis: 6379
- Prometheus: 9090
- Grafana: 3000

### Configuración de Monitoreo

#### `prometheus.yml`

**Propósito:** Configuración de Prometheus.

**Incluye:**
- Configuración de scraping
- Targets a monitorear
- Reglas de alertas (si aplica)

### Configuración de Entorno

#### `.env.example`

**Propósito:** Plantilla de variables de entorno.

**Variables principales:**
- `NODE_ENV` - Entorno (development, production, test)
- `PORT` - Puerto del servidor API
- `DATABASE_URL` - URL de PostgreSQL
- `NEO4J_URI` - URI de Neo4j
- `NEO4J_USER` - Usuario Neo4j
- `NEO4J_PASSWORD` - Contraseña Neo4j
- `REDIS_URL` - URL de Redis
- `OPENAI_API_KEY` - API key de OpenAI (opcional)
- `LM_STUDIO_URL` - URL de LM Studio local
- `LOG_LEVEL` - Nivel de logging

#### `.env.local`

**Propósito:** Variables de entorno locales (en `.gitignore`).

**Uso:** Cada desarrollador crea su propio `.env.local` basado en `.env.example`.

### Otros Archivos de Configuración

#### `.gitignore`

**Propósito:** Archivos y carpetas a ignorar por Git.

**Ya existe** (creado en DNT-231) con exclusiones para:
- `node_modules/`
- `.env`, `.env.local`
- `dist/`, `build/`
- Logs y archivos temporales

#### `.editorconfig`

**Propósito:** Configuración consistente del editor.

**Incluye:**
- Indentación (espacios vs tabs)
- Tamaño de indentación
- Encoding de archivos
- Finales de línea

#### `.prettierrc` (Opcional)

**Propósito:** Configuración de Prettier para formateo.

**Si se usa:**
- Configuración de formateo
- Integración con ESLint

#### `.eslintrc.json` (Opcional)

**Propósito:** Configuración de ESLint.

**Si se usa:**
- Reglas de linting
- Integración con TypeScript
- Reglas personalizadas del proyecto

#### `README.md`

**Propósito:** Documentación principal del proyecto.

**Debe incluir:**
- Descripción del proyecto
- Instrucciones de instalación
- Guía de uso
- Estructura del proyecto (referencia a este documento)
- Contribución

## Convenciones de Código

### Estructura de Archivos TypeScript

**Convenciones:**
- Un archivo por clase/función principal
- Archivos en camelCase: `valueEngine.ts`, `nihilismMonitor.ts`
- Clases en PascalCase: `ValueEngine`, `NihilismMonitor`
- Interfaces en PascalCase: `Value`, `Phase`
- Tipos en PascalCase: `Result<T, E>`

**Ejemplo de estructura de archivo:**
```typescript
// Imports externos primero
import { FastifyInstance } from 'fastify';

// Imports internos después
import { ValueEngine } from '../core/value-engine';
import { Result } from '../types/result';

// Tipos e interfaces
interface ValueRequest {
  // ...
}

// Implementación
export class ValueService {
  // ...
}

// Exports
export { ValueService };
```

### Nombres de Archivos y Carpetas

**Carpetas:**
- En minúsculas: `src/core/`, `src/modules/`
- Nombres descriptivos y cortos
- Plural para colecciones: `agents/`, `modules/`

**Archivos:**
- camelCase para archivos de código: `valueEngine.ts`
- kebab-case para archivos de configuración: `vitest.config.ts`
- `index.ts` para exports centralizados

### Patrones de Organización

**Módulos:**
- Cada módulo tiene su carpeta
- `index.ts` exporta la API pública del módulo
- Implementación interna en archivos separados

**Imports:**
- Imports absolutos desde `src/` usando paths en `tsconfig.json`
- Evitar imports relativos profundos (`../../../`)
- Usar barrel exports (`index.ts`) cuando sea apropiado

**Ejemplo de paths en `tsconfig.json`:**
```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@/types/*": ["./src/types/*"],
      "@/core/*": ["./src/core/*"]
    }
  }
}
```

### Patrones de Diseño

**Patrones utilizados:**
- **Result<T, E>** - Manejo funcional de errores
- **FSM (Finite State Machine)** - Para ValueEngine
- **Observer Pattern** - Para NihilismMonitor
- **Strategy Pattern** - Para prompts de diferentes agentes
- **Decorators** - Para cache y retry en LLM clients

## Dependencias y Tecnologías

### Stack Tecnológico Completo

**Runtime y Lenguaje:**
- Node.js 20 LTS
- TypeScript 5.3+ (strict mode)
- pnpm (package manager)

**Backend:**
- Fastify - Framework web rápido
- OpenAI SDK → LM Studio local - LLM
- Transformers.js (@xenova/transformers) - Embeddings
- Drizzle ORM - ORM para PostgreSQL
- BullMQ - Sistema de colas
- ioredis - Cliente Redis
- neo4j-driver - Driver Neo4j
- pg + pgvector - PostgreSQL con vectores

**Testing y Calidad:**
- Vitest - Framework de testing
- Pino - Logging estructurado
- prom-client - Métricas Prometheus

**Infraestructura:**
- Docker Compose - Orquestación de servicios
- PostgreSQL 15+ - Base de datos relacional con vectores
- Neo4j 5.x - Base de datos gráfica
- Redis 7.x - Cache y colas
- Prometheus - Métricas
- Grafana - Visualización

### Versiones Requeridas

**Node.js:** 20.x LTS (mínimo 20.0.0)  
**TypeScript:** 5.3+  
**pnpm:** 8.x+  

**Bases de datos:**
- PostgreSQL: 15+
- Neo4j: 5.x
- Redis: 7.x

### Dependencias Principales por Categoría

**Framework Web:**
- `fastify` - Framework web
- `@fastify/cors` - CORS
- `@fastify/helmet` - Seguridad

**LLM y Embeddings:**
- `openai` - OpenAI SDK
- `@xenova/transformers` - Transformers.js

**Bases de Datos:**
- `drizzle-orm` - ORM
- `drizzle-kit` - CLI
- `pg` - PostgreSQL driver
- `pgvector` - Extensión de vectores
- `neo4j-driver` - Neo4j driver
- `ioredis` - Redis client

**Colas:**
- `bullmq` - Sistema de colas
- `ioredis` - Backend de Redis

**Logging y Monitoreo:**
- `pino` - Logging
- `prom-client` - Métricas

**Testing:**
- `vitest` - Testing framework
- `@vitest/ui` - UI de tests

## Relaciones entre Módulos

### Flujo Principal

```
Orchestrator
    ↓
ValueEngine (FSM)
    ↓
┌─────────────────────────────────────┐
│  Deconstruction Module               │
│  → Nihilistic Module                 │
│  → Creative Module                   │
│  → Evaluation Module                 │
└─────────────────────────────────────┘
    ↓
NihilismMonitor (Observer)
    ↓
RAG System (contexto)
    ↓
Agents (Zarathustra, Genealogist, etc.)
    ↓
LLM (OpenAI/LM Studio)
```

### Dependencias entre Carpetas

- `core/` depende de: `types/`, `modules/`, `agents/`, `llm/`, `rag/`
- `modules/` depende de: `types/`, `agents/`, `llm/`, `rag/`
- `agents/` depende de: `types/`, `llm/`
- `api/` depende de: `core/`, `types/`
- `queues/` depende de: `core/`, `types/`
- `rag/` depende de: `embeddings/`, `db/postgres/`

## Próximos Pasos

Una vez definida esta estructura, los siguientes pasos son:

1. **Crear archivos de configuración** - `package.json`, `tsconfig.json`, etc.
2. **Crear estructura de carpetas** - Crear todas las carpetas definidas
3. **Implementar tipos base** - `src/types/` con tipos fundamentales
4. **Implementar componentes core** - Empezar con `src/core/`
5. **Implementar módulos de fases** - `src/modules/`
6. **Implementar agentes** - `src/agents/`
7. **Implementar API** - `src/api/`
8. **Configurar infraestructura** - Docker Compose, bases de datos

## Referencias

- [Contexto del Proyecto](./project-context.md) - Contexto completo del proyecto
- [Issue DNT-225](https://linear.app/clasificadoria/issue/DNT-225/docs-definir-estructura-completa-del-proyecto) - Issue que define esta estructura

---

**Nota:** Esta estructura debe mantenerse actualizada a medida que el proyecto evoluciona. Cualquier cambio significativo debe ser documentado aquí.
