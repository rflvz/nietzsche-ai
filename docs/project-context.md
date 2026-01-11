# Contexto del Proyecto: Sistema de Generación de Valores Nietzscheano

**Última actualización:** 2026-01-11  
**Versión:** 1.0

> **⚠️ IMPORTANTE:** Este documento es la fuente única de verdad para el contexto del proyecto. Debe mantenerse actualizado y ser referenciado por todos los comandos y procesos que requieran contexto del proyecto.

## Información del Proyecto

### Descripción General

Sistema de IA experimental que genera valores filosóficos nuevos mediante un proceso de cuatro fases inspirado en la filosofía de Nietzsche:

1. **Deconstrucción genealógica** de conceptos morales existentes
2. **Fase nihilista** (vacío conceptual necesario)
3. **Creación de valores genuinamente nuevos**
4. **Evaluación** con criterio del "eterno retorno"

**Importante**: Sistema sin restricciones morales por diseño filosófico. El nihilismo es feature, no bug.

### Objetivos del Proyecto

- Generar valores filosóficos nuevos mediante proceso sistemático de 4 fases
- Implementar sistema multi-agente con personajes nietzscheanos (Zarathustra, Genealogist, Dionysus, Apollo, LastMan)
- Crear sistema de RAG (Retrieval-Augmented Generation) con corpus de Nietzsche
- Monitorear y analizar fases nihilistas del sistema
- Proporcionar API REST para interacción con el sistema
- Procesar generación de valores en background mediante colas

### Estructura del Proyecto

> **Estado:** A definir - Proyecto en fase inicial de planificación

La estructura del proyecto será definida en el issue [DNT-225: Definir estructura completa del proyecto](https://linear.app/clasificadoria/issue/DNT-225/docs-definir-estructura-completa-del-proyecto).

Estructura planificada (según diseño inicial):
- `src/` - Código fuente principal
  - `config/` - Configuración (env, logger, database)
  - `types/` - Tipos TypeScript (Result, Value, Phase, etc.)
  - `core/` - Componentes core (Orchestrator, ValueEngine, DialecticalSystem, NihilismMonitor)
  - `modules/` - Módulos de fases (Deconstruction, Nihilistic, Creative, Evaluation)
  - `agents/` - Agentes filosóficos (Zarathustra, Genealogist, Dionysus, Apollo, LastMan)
  - `llm/` - Integración con LLM (OpenAI SDK, LM Studio)
  - `embeddings/` - Sistema de embeddings (Transformers.js)
  - `db/` - Bases de datos (PostgreSQL, Neo4j, Redis)
  - `rag/` - Sistema RAG (document processor, chunker, retriever)
  - `monitoring/` - Monitoreo y métricas (Prometheus)
  - `api/` - API REST (Fastify)
  - `queues/` - Colas de procesamiento (BullMQ)
  - `utils/` - Utilidades
- `data/` - Datos (corpus de Nietzsche, prompts, exports)
- `tests/` - Tests (unit, integration)
- `scripts/` - Scripts de utilidad
- `docs/` - Documentación

### Tecnologías y Herramientas

**Runtime y Lenguaje:**
- Node.js 20 LTS
- TypeScript 5.3+ (strict mode)
- pnpm (package manager)

**Backend:**
- Fastify (API REST)
- OpenAI SDK → LM Studio local (LLM)
- Transformers.js (@xenova/transformers) (Embeddings)
- Drizzle ORM (ORM)
- BullMQ (Queue system)

**Bases de Datos:**
- PostgreSQL 15+ con pgvector (vector database)
- Neo4j 5.x (graph database)
- Redis 7.x (cache y colas)

**Testing y Calidad:**
- Vitest (testing framework)
- Pino (logging)
- prom-client (métricas Prometheus)

**Frontend (fase posterior):**
- Next.js 14

**Infraestructura:**
- Docker Compose (PostgreSQL, Neo4j, Redis, Prometheus, Grafana)

### Estado Actual del Proyecto

**Estado:** Fase de planificación inicial

- ✅ Proyecto creado en Linear
- ✅ Epic de diseño arquitectónico creado
- ✅ 5 issues iniciales de diseño creados y vinculados
- ⏳ Pendiente: Completar issues de diseño antes de implementación
- ⏳ Pendiente: Definir estructura completa del proyecto
- ⏳ Pendiente: Crear diagramas UML
- ⏳ Pendiente: Definir casos de uso
- ⏳ Pendiente: Identificar actores principales
- ⏳ Pendiente: Documentar arquitectura en cursor rules

**Fases del Proyecto:**
1. **Fase 1 - Diseño y Arquitectura** (En progreso): Definición de estructura, diagramas UML, casos de uso
2. **Fase 2 - Setup y Configuración**: Configuración inicial del proyecto
3. **Fase 3 - Implementación Core**: Motor de generación y módulos principales
4. **Fase 4 - Integración**: Integración de componentes y testing
5. **Fase 5 - Documentación y Deploy**: Documentación completa y despliegue

## Información de Linear

### Equipo Principal

- **Nombre:** personal/trabajo
- **ID:** a4e18927-fcfc-49d4-a5f2-947c18c73cbf
- **Creado:** 2025-10-14
- **Última actualización:** 2026-01-08

### Proyecto Principal

**Sistema de Generación de Valores Nietzscheano**

- **ID:** 4d0b8a20-9ca6-48a1-98ae-57279a1a29d3
- **URL:** https://linear.app/clasificadoria/project/sistema-de-generacion-de-valores-nietzscheano-bd208887ba46
- **Resumen:** Sistema de IA experimental que genera valores filosóficos nuevos mediante deconstrucción genealógica, fase nihilista y creación de valores genuinamente nuevos basado en Nietzsche
- **Prioridad:** Medium
- **Estado:** Todo (planned)
- **Creado:** 2026-01-11
- **Última actualización:** 2026-01-11

### Issues Activos

#### Epic Principal

**DNT-224: Epic: Diseño Arquitectónico y Diagramas**
- **ID:** e4bf79de-386f-47ec-b4e1-77bfbf66817d
- **URL:** https://linear.app/clasificadoria/issue/DNT-224/epic-diseno-arquitectonico-y-diagramas
- **Branch:** `rafaceitunoalvarez/dnt-224-epic-diseno-arquitectonico-y-diagramas`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** research, setup, docs
- **Descripción:** Epic que agrupa todas las tareas de diseño arquitectónico necesarias para establecer las bases del proyecto antes de comenzar la implementación.

#### Sub-Issues del Epic

**DNT-225: docs: Definir estructura completa del proyecto**
- **ID:** 49224d56-62ce-44b8-b1c0-e0198154dea6
- **URL:** https://linear.app/clasificadoria/issue/DNT-225/docs-definir-estructura-completa-del-proyecto
- **Branch:** `rafaceitunoalvarez/dnt-225-docs-definir-estructura-completa-del-proyecto`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** setup, docs
- **Parent:** DNT-224
- **Descripción:** Definir la estructura completa de carpetas, archivos y organización del proyecto antes de comenzar la implementación. Incluye definir estructura de carpetas para `src/`, `data/`, `tests/`, `scripts/`, `docs/` y archivos de configuración.

**DNT-226: docs: Crear diagramas UML del sistema**
- **ID:** 51b213d2-0065-4ee4-85bf-7d47407de67b
- **URL:** https://linear.app/clasificadoria/issue/DNT-226/docs-crear-diagramas-uml-del-sistema
- **Branch:** `rafaceitunoalvarez/dnt-226-docs-crear-diagramas-uml-del-sistema`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** research, docs
- **Parent:** DNT-224
- **Descripción:** Crear diagramas UML completos: Diagrama de Clases, Componentes, Secuencia, Estados (FSM), y Despliegue. Los diagramas deben representar la arquitectura, clases, componentes y flujos del sistema.

**DNT-227: docs: Definir diagramas de casos de uso**
- **ID:** 1c809f0d-2cb0-4f4b-a37d-36a3e55ae2da
- **URL:** https://linear.app/clasificadoria/issue/DNT-227/docs-definir-diagramas-de-casos-de-uso
- **Branch:** `rafaceitunoalvarez/dnt-227-docs-definir-diagramas-de-casos-de-uso`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** research, docs
- **Parent:** DNT-224
- **Descripción:** Crear diagramas de casos de uso que identifiquen los actores principales (Usuario Final, Sistemas internos) y los casos de uso del sistema. Documentar flujos con precondiciones y postcondiciones.

**DNT-228: docs: Identificar actores principales del sistema**
- **ID:** 8b6a40ca-da9d-4960-832d-54c7f2717e7c
- **URL:** https://linear.app/clasificadoria/issue/DNT-228/docs-identificar-actores-principales-del-sistema
- **Branch:** `rafaceitunoalvarez/dnt-228-docs-identificar-actores-principales-del-sistema`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** research, docs
- **Parent:** DNT-224
- **Descripción:** Identificar y documentar todos los actores principales: actores externos (Usuario Final), actores internos (Orchestrator, ValueEngine, DialecticalSystem, NihilismMonitor, RAG System), y agentes filosóficos (Zarathustra, Genealogist, Dionysus, Apollo, LastMan).

**DNT-229: docs: Documentar arquitectura en cursor rules**
- **ID:** 161b3a6b-e2a0-4749-84ea-3a1952bd5e8e
- **URL:** https://linear.app/clasificadoria/issue/DNT-229/docs-documentar-arquitectura-en-cursor-rules
- **Branch:** `rafaceitunoalvarez/dnt-229-docs-documentar-arquitectura-en-cursor-rules`
- **Prioridad:** High
- **Estado:** Backlog
- **Labels:** setup, cursor, docs
- **Parent:** DNT-224
- **Descripción:** Crear archivo `.cursorrules` completo que documente la arquitectura, contexto filosófico, stack tecnológico y reglas de desarrollo del proyecto. Debe incluir toda la información necesaria para que cualquier desarrollador (o IA) entienda el proyecto.

### Prioridades y Focos

**Prioridad Actual:**
- **Alta (High):** Todos los issues de diseño arquitectónico (DNT-224 a DNT-229)
- **Media (Medium):** Proyecto general

**Foco Actual:**
- Completar fase de diseño arquitectónico antes de comenzar implementación
- Definir estructura completa del proyecto
- Crear diagramas UML y casos de uso
- Documentar arquitectura en cursor rules

**Bloqueos:**
- La implementación está bloqueada hasta completar los issues de diseño
- La estructura del proyecto debe definirse antes de crear archivos

## Convenciones y Estándares

> **Estado:** A definir - Proyecto en fase inicial

Las convenciones y estándares del proyecto serán definidas durante la fase de diseño arquitectónico y documentadas en el archivo `.cursorrules` (issue DNT-229).

**Convenciones planificadas (según stack tecnológico):**
- TypeScript strict mode
- Estructura modular por funcionalidad
- Patrón Result<T, E> para manejo de errores
- Máquina de estados finitos (FSM) para ValueEngine
- Patrón Observer para NihilismMonitor
- Strategy pattern para prompts
- Decorators para LLM clients (cache, retry)

## Decisiones Arquitectónicas

> **Estado:** A documentar según issues de diseño

Las decisiones arquitectónicas principales serán documentadas durante la fase de diseño:

1. **Arquitectura de 4 fases:** Deconstrucción → Nihilismo → Creación → Evaluación
2. **Sistema multi-agente:** Agentes filosóficos con diferentes perspectivas nietzscheanas
3. **RAG System:** Retrieval-Augmented Generation con corpus de Nietzsche
4. **FSM para ValueEngine:** Máquina de estados finitos para gestionar el proceso
5. **Observer Pattern:** NihilismMonitor observa y clasifica fases nihilistas
6. **Background Processing:** BullMQ para procesar generación de valores en background

## Bloqueos y Dependencias

### Bloqueos Actuales

- **Implementación bloqueada:** Todos los issues de implementación están bloqueados hasta completar el epic de diseño arquitectónico (DNT-224)
- **Estructura del proyecto:** La estructura debe definirse (DNT-225) antes de crear archivos

### Dependencias entre Issues

- **DNT-225** (Definir estructura) → Bloquea todos los issues de implementación
- **DNT-226** (Diagramas UML) → Requiere DNT-225, bloquea implementación core
- **DNT-227** (Casos de uso) → Requiere DNT-225, bloquea implementación de API
- **DNT-228** (Actores) → Requiere DNT-225, bloquea implementación de agentes y core
- **DNT-229** (Cursor rules) → Requiere DNT-225, DNT-226, DNT-228, bloquea toda implementación

## Próximos Pasos

### Inmediatos (Fase de Diseño)

1. **Completar DNT-225:** Definir estructura completa del proyecto
   - Definir estructura de carpetas
   - Identificar archivos de configuración
   - Documentar en `docs/architecture.md`

2. **Completar DNT-226:** Crear diagramas UML del sistema
   - Diagrama de Clases
   - Diagrama de Componentes
   - Diagrama de Secuencia
   - Diagrama de Estados (FSM)
   - Diagrama de Despliegue

3. **Completar DNT-227:** Definir diagramas de casos de uso
   - Identificar actores
   - Definir casos de uso principales
   - Documentar flujos

4. **Completar DNT-228:** Identificar actores principales
   - Documentar actores externos e internos
   - Documentar agentes filosóficos
   - Definir roles y perspectivas

5. **Completar DNT-229:** Documentar arquitectura en cursor rules
   - Crear archivo `.cursorrules`
   - Incluir contexto filosófico
   - Documentar stack y arquitectura
   - Definir reglas de desarrollo

### Siguientes Fases

- **Fase 2:** Setup y configuración inicial del proyecto
- **Fase 3:** Implementación core (motor de generación, módulos, agentes)
- **Fase 4:** Integración y testing
- **Fase 5:** Documentación completa y deploy

## Cómo Usar Este Documento

### Para Desarrolladores

1. **Leer antes de comenzar:** Revisar este documento para entender el contexto completo del proyecto
2. **Consultar Linear:** Verificar issues activos y prioridades en Linear
3. **Actualizar cuando sea necesario:** Si hay cambios importantes, actualizar este documento

### Para Comandos Automatizados

Este documento debe ser referenciado por:
- Comandos de Linear que requieren contexto del proyecto
- Comandos de agentización que necesitan contexto
- Scripts de automatización que requieren información del proyecto

### Actualización del Documento

**Cuándo actualizar:**
- Cuando se completen issues importantes
- Cuando cambien las prioridades o focos
- Cuando se tomen decisiones arquitectónicas importantes
- Cuando cambie el estado del proyecto
- Al menos una vez por semana durante desarrollo activo

**Cómo actualizar:**
- Actualizar fecha de "Última actualización"
- Actualizar secciones relevantes con nueva información
- Mantener sincronizado con Linear
- Documentar cambios importantes en "Decisiones Arquitectónicas"

## Referencias

### Documentación del Proyecto

- **Proyecto en Linear:** https://linear.app/clasificadoria/project/sistema-de-generacion-de-valores-nietzscheano-bd208887ba46
- **Epic de Diseño:** https://linear.app/clasificadoria/issue/DNT-224/epic-diseno-arquitectonico-y-diagramas

### Issues de Linear

- [DNT-224: Epic: Diseño Arquitectónico y Diagramas](https://linear.app/clasificadoria/issue/DNT-224/epic-diseno-arquitectonico-y-diagramas)
- [DNT-225: Definir estructura completa del proyecto](https://linear.app/clasificadoria/issue/DNT-225/docs-definir-estructura-completa-del-proyecto)
- [DNT-226: Crear diagramas UML del sistema](https://linear.app/clasificadoria/issue/DNT-226/docs-crear-diagramas-uml-del-sistema)
- [DNT-227: Definir diagramas de casos de uso](https://linear.app/clasificadoria/issue/DNT-227/docs-definir-diagramas-de-casos-de-uso)
- [DNT-228: Identificar actores principales del sistema](https://linear.app/clasificadoria/issue/DNT-228/docs-identificar-actores-principales-del-sistema)
- [DNT-229: Documentar arquitectura en cursor rules](https://linear.app/clasificadoria/issue/DNT-229/docs-documentar-arquitectura-en-cursor-rules)

### Recursos Filosóficos

- Filosofía de Nietzsche (genealogía, nihilismo, creación de valores)
- Concepto del "eterno retorno"
- Personajes nietzscheanos: Zarathustra, Dionysus, Apollo, Last Man

---

**Nota:** Este documento debe mantenerse actualizado y sincronizado con Linear y el estado real del proyecto.
