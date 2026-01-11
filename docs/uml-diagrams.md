# Diagramas UML del Sistema

**Última actualización:** 2026-01-11  
**Versión:** 1.0

> **Nota:** Este documento contiene los diagramas UML completos del Sistema de Generación de Valores Nietzscheano, incluyendo diagramas de clases, componentes, secuencia, estados y despliegue.

## Introducción

Los diagramas UML son esenciales para visualizar y comunicar la arquitectura del sistema antes de la implementación. Este documento incluye todos los diagramas UML necesarios para entender la estructura, relaciones, flujos y despliegue del sistema.

**Diagramas incluidos:**
1. Diagrama de Clases - Estructura de clases y relaciones
2. Diagrama de Componentes - Componentes principales e interfaces
3. Diagrama de Secuencia - Flujos de interacción
4. Diagrama de Estados - Máquina de estados finitos (FSM)
5. Diagrama de Despliegue - Arquitectura de despliegue

## 1. Diagrama de Clases

El diagrama de clases muestra la estructura estática del sistema, incluyendo clases principales, módulos, agentes, interfaces y sus relaciones.

```mermaid
classDiagram
    %% Core Classes
    class Orchestrator {
        -valueEngine: ValueEngine
        -dialecticalSystem: DialecticalSystem
        -ragSystem: RAGSystem
        -nihilismMonitor: NihilismMonitor
        +generateValue(concept: string): Promise~Result~Value, Error~~
        +coordinatePhase(phase: Phase): Promise~void~
        +handleError(error: Error): void
    }
    
    class ValueEngine {
        -currentState: ValueState
        -stateHistory: ValueState[]
        +transitionTo(state: ValueState): Result~void, Error~
        +validateTransition(from: ValueState, to: ValueState): boolean
        +getCurrentState(): ValueState
        +reset(): void
    }
    
    class DialecticalSystem {
        -agents: Map~AgentType, Agent~
        -debateHistory: Debate[]
        +initiateDebate(participants: AgentType[], topic: string): Promise~DebateResult~
        +synthesizePerspectives(perspectives: Perspective[]): Synthesis
        +addAgent(agent: Agent): void
    }
    
    class NihilismMonitor {
        -metrics: NihilismMetrics
        -observers: Observer[]
        +observePhase(phase: Phase): void
        +classifyNihilism(state: NihilisticState): NihilismType
        +generateAlert(alert: Alert): void
        +getMetrics(): NihilismMetrics
    }
    
    %% Phase Modules
    class DeconstructionModule {
        -genealogist: Genealogist
        -ragSystem: RAGSystem
        +deconstruct(concept: MoralConcept): Promise~DeconstructionResult~
        +analyzeGenealogy(concept: MoralConcept): Genealogy
    }
    
    class NihilisticModule {
        -dionysus: Dionysus
        -lastMan: LastMan
        +createVoid(concept: MoralConcept): Promise~NihilisticState~
        +destroyValues(values: Value[]): void
    }
    
    class CreativeModule {
        -zarathustra: Zarathustra
        -dionysus: Dionysus
        -apollo: Apollo
        +createValue(concept: MoralConcept, void: NihilisticState): Promise~Value~
        +synthesizePerspectives(perspectives: Perspective[]): Value
    }
    
    class EvaluationModule {
        -zarathustra: Zarathustra
        -apollo: Apollo
        -lastMan: LastMan
        +evaluateValue(value: Value): Promise~EvaluationResult~
        +applyEternalReturn(value: Value): boolean
        +checkStructure(value: Value): StructureCheck
    }
    
    %% Agents
    class Agent {
        <<interface>>
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +getName(): string
        +getPersonality(): Personality
    }
    
    class Zarathustra {
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +affirmLife(value: Value): boolean
        +applyEternalReturn(value: Value): boolean
    }
    
    class Genealogist {
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +deconstructGenealogy(concept: MoralConcept): Genealogy
        +revealOrigins(value: Value): Origin[]
    }
    
    class Dionysus {
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +createFromVoid(void: NihilisticState): Value
        +destroyValues(values: Value[]): void
    }
    
    class Apollo {
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +giveForm(value: Value): StructuredValue
        +evaluateStructure(value: Value): StructureCheck
    }
    
    class LastMan {
        +generatePerspective(topic: string, context: Context): Promise~Perspective~
        +detectWeakness(value: Value): boolean
        +warnPassiveNihilism(state: NihilisticState): Alert
    }
    
    %% RAG System
    class RAGSystem {
        -vectorStore: VectorStore
        -embedder: Embedder
        -documentProcessor: DocumentProcessor
        +retrieveContext(query: string, limit: number): Promise~Context[]
        +processCorpus(corpus: Document[]): Promise~void~
        +searchSemantic(query: string): Promise~Document[]
    }
    
    class DocumentProcessor {
        +chunkDocuments(documents: Document[]): Chunk[]
        +extractMetadata(document: Document): Metadata
    }
    
    class Embedder {
        +generateEmbedding(text: string): Promise~Vector~
        +generateBatchEmbeddings(texts: string[]): Promise~Vector[]~
    }
    
    class VectorStore {
        +storeEmbedding(embedding: Embedding): Promise~void~
        +searchSimilar(query: Vector, limit: number): Promise~Embedding[]
    }
    
    %% LLM Integration
    class LLMClient {
        <<interface>>
        +generate(prompt: Prompt): Promise~Response~
        +stream(prompt: Prompt): AsyncGenerator~Response~
    }
    
    class LMStudioClient {
        +generate(prompt: Prompt): Promise~Response~
        +stream(prompt: Prompt): AsyncGenerator~Response~
        -baseUrl: string
        -apiKey: string
    }
    
    %% Repositories
    class ValueRepository {
        +save(value: Value): Promise~void~
        +findById(id: string): Promise~Value | null~
        +findByCriteria(criteria: Criteria): Promise~Value[]~
    }
    
    class GenealogyRepository {
        +save(genealogy: Genealogy): Promise~void~
        +findByValueId(valueId: string): Promise~Genealogy | null~
    }
    
    %% Types
    class Value {
        +id: string
        +content: string
        +phase: Phase
        +createdAt: Date
        +genealogy: Genealogy
    }
    
    class MoralConcept {
        +name: string
        +description: string
        +origin: string
    }
    
    class Perspective {
        +agent: AgentType
        +content: string
        +tone: Tone
    }
    
    class DebateResult {
        +perspectives: Perspective[]
        +synthesis: Synthesis
        +conflicts: Conflict[]
    }
    
    %% Relationships
    Orchestrator --> ValueEngine : uses
    Orchestrator --> DialecticalSystem : coordinates
    Orchestrator --> RAGSystem : requests context
    Orchestrator --> NihilismMonitor : receives alerts
    Orchestrator --> DeconstructionModule : orchestrates
    Orchestrator --> NihilisticModule : orchestrates
    Orchestrator --> CreativeModule : orchestrates
    Orchestrator --> EvaluationModule : orchestrates
    
    ValueEngine --> ValueState : manages
    ValueEngine --> Phase : transitions
    
    DialecticalSystem --> Agent : coordinates
    DialecticalSystem --> Zarathustra : uses
    DialecticalSystem --> Genealogist : uses
    DialecticalSystem --> Dionysus : uses
    DialecticalSystem --> Apollo : uses
    DialecticalSystem --> LastMan : uses
    
    Agent <|.. Zarathustra : implements
    Agent <|.. Genealogist : implements
    Agent <|.. Dionysus : implements
    Agent <|.. Apollo : implements
    Agent <|.. LastMan : implements
    
    DeconstructionModule --> Genealogist : uses
    NihilisticModule --> Dionysus : uses
    NihilisticModule --> LastMan : uses
    CreativeModule --> Zarathustra : uses
    CreativeModule --> Dionysus : uses
    CreativeModule --> Apollo : uses
    EvaluationModule --> Zarathustra : uses
    EvaluationModule --> Apollo : uses
    EvaluationModule --> LastMan : uses
    
    RAGSystem --> VectorStore : uses
    RAGSystem --> Embedder : uses
    RAGSystem --> DocumentProcessor : uses
    RAGSystem --> LLMClient : uses
    
    LLMClient <|.. LMStudioClient : implements
    
    ValueRepository --> Value : manages
    GenealogyRepository --> Genealogy : manages
    
    NihilismMonitor --> ValueEngine : observes
    NihilismMonitor --> Phase : monitors
```

## 2. Diagrama de Componentes

El diagrama de componentes muestra los componentes principales del sistema, sus interfaces y dependencias externas.

```mermaid
graph TB
    subgraph "API Layer"
        APIREST[API REST<br/>Fastify]
    end
    
    subgraph "Application Layer"
        Orchestrator[Orchestrator]
        ValueEngine[ValueEngine<br/>FSM]
        DialecticalSystem[DialecticalSystem]
    end
    
    subgraph "Domain Modules"
        DeconstructionModule[DeconstructionModule]
        NihilisticModule[NihilisticModule]
        CreativeModule[CreativeModule]
        EvaluationModule[EvaluationModule]
    end
    
    subgraph "Agents Layer"
        Zarathustra[Zarathustra]
        Genealogist[Genealogist]
        Dionysus[Dionysus]
        Apollo[Apollo]
        LastMan[LastMan]
    end
    
    subgraph "RAG System"
        RAGSystem[RAGSystem]
        DocumentProcessor[DocumentProcessor]
        Embedder[Embedder<br/>Transformers.js]
        VectorStore[VectorStore<br/>pgvector]
    end
    
    subgraph "Monitoring"
        NihilismMonitor[NihilismMonitor]
        MetricsExporter[Metrics Exporter<br/>Prometheus]
    end
    
    subgraph "Queue System"
        QueueManager[Queue Manager<br/>BullMQ]
        ValueWorker[Value Generation Worker]
    end
    
    subgraph "LLM Integration"
        LLMClient[LLM Client<br/>OpenAI SDK]
        LMStudio[LM Studio<br/>Local]
    end
    
    subgraph "Data Layer"
        PostgreSQL[(PostgreSQL<br/>+ pgvector)]
        Neo4j[(Neo4j<br/>Graph DB)]
        Redis[(Redis<br/>Cache + Queues)]
    end
    
    subgraph "External Services"
        Prometheus[Prometheus<br/>Metrics]
        Grafana[Grafana<br/>Visualization]
    end
    
    %% API to Application
    APIREST -->|HTTP Requests| Orchestrator
    APIREST -->|Queue Jobs| QueueManager
    
    %% Application Layer
    Orchestrator --> ValueEngine
    Orchestrator --> DialecticalSystem
    Orchestrator --> DeconstructionModule
    Orchestrator --> NihilisticModule
    Orchestrator --> CreativeModule
    Orchestrator --> EvaluationModule
    Orchestrator --> RAGSystem
    Orchestrator --> NihilismMonitor
    
    ValueEngine -->|State Transitions| Orchestrator
    
    %% Modules to Agents
    DeconstructionModule --> Genealogist
    NihilisticModule --> Dionysus
    NihilisticModule --> LastMan
    CreativeModule --> Zarathustra
    CreativeModule --> Dionysus
    CreativeModule --> Apollo
    EvaluationModule --> Zarathustra
    EvaluationModule --> Apollo
    EvaluationModule --> LastMan
    
    DialecticalSystem --> Zarathustra
    DialecticalSystem --> Genealogist
    DialecticalSystem --> Dionysus
    DialecticalSystem --> Apollo
    DialecticalSystem --> LastMan
    
    %% RAG System
    RAGSystem --> DocumentProcessor
    RAGSystem --> Embedder
    RAGSystem --> VectorStore
    RAGSystem --> LLMClient
    
    %% LLM Integration
    LLMClient --> LMStudio
    Agents -->|Use| LLMClient
    
    %% Data Layer
    VectorStore --> PostgreSQL
    Orchestrator --> PostgreSQL
    Orchestrator --> Neo4j
    QueueManager --> Redis
    Orchestrator --> Redis
    
    %% Monitoring
    NihilismMonitor --> MetricsExporter
    MetricsExporter --> Prometheus
    Prometheus --> Grafana
    
    %% Queue System
    QueueManager --> ValueWorker
    ValueWorker --> Orchestrator
    
    %% Agents (simplified)
    Agents[Agents] -.->|Use| LLMClient
```

## 3. Diagrama de Secuencia

El diagrama de secuencia muestra el flujo completo de generación de valores a través de las 4 fases, incluyendo interacciones entre componentes.

```mermaid
sequenceDiagram
    participant User as Usuario Final
    participant API as API REST
    participant Queue as Queue Manager
    participant Worker as Value Worker
    participant Orch as Orchestrator
    participant VE as ValueEngine
    participant DS as DialecticalSystem
    participant RAG as RAG System
    participant NM as NihilismMonitor
    participant Gen as Genealogist
    participant Dion as Dionysus
    participant Zar as Zarathustra
    participant Apo as Apollo
    participant Last as LastMan
    
    User->>API: POST /api/values/generate
    API->>Queue: Enqueue generation job
    API-->>User: 202 Accepted (jobId)
    
    Queue->>Worker: Process job
    Worker->>Orch: generateValue(concept)
    
    %% Phase 1: Deconstruction
    Orch->>VE: transitionTo(DECONSTRUCTION)
    VE-->>Orch: State updated
    
    Orch->>RAG: retrieveContext(concept)
    RAG-->>Orch: Context from Nietzsche
    
    Orch->>DS: initiateDebate([Genealogist], topic)
    DS->>Gen: generatePerspective(topic, context)
    Gen->>RAG: retrieveContext(genealogy)
    RAG-->>Gen: Genealogical context
    Gen-->>DS: Perspective (deconstruction)
    DS-->>Orch: DebateResult (deconstructed)
    
    Orch->>NM: observePhase(DECONSTRUCTION)
    NM-->>Orch: Metrics recorded
    
    %% Phase 2: Nihilistic
    Orch->>VE: transitionTo(NIHILISTIC)
    VE-->>Orch: State updated
    
    Orch->>DS: initiateDebate([Dionysus, LastMan], void)
    DS->>Dion: generatePerspective(void, context)
    Dion-->>DS: Perspective (creative destruction)
    DS->>Last: generatePerspective(void, context)
    Last-->>DS: Perspective (warning passive)
    DS-->>Orch: DebateResult (nihilistic state)
    
    Orch->>NM: observePhase(NIHILISTIC)
    NM->>NM: classifyNihilism(state)
    NM->>NM: generateAlert(if needed)
    NM-->>Orch: Metrics + Alerts
    
    %% Phase 3: Creative
    Orch->>VE: transitionTo(CREATIVE)
    VE-->>Orch: State updated
    
    Orch->>RAG: retrieveContext(creation)
    RAG-->>Orch: Creative context
    
    Orch->>DS: initiateDebate([Zarathustra, Dionysus, Apollo], creation)
    DS->>Zar: generatePerspective(creation, context)
    Zar-->>DS: Perspective (affirmation)
    DS->>Dion: generatePerspective(creation, context)
    Dion-->>DS: Perspective (chaos)
    DS->>Apo: generatePerspective(creation, context)
    Apo-->>DS: Perspective (form)
    DS->>DS: synthesizePerspectives()
    DS-->>Orch: DebateResult (new value)
    
    %% Phase 4: Evaluation
    Orch->>VE: transitionTo(EVALUATION)
    VE-->>Orch: State updated
    
    Orch->>DS: initiateDebate([Zarathustra, Apollo, LastMan], evaluation)
    DS->>Zar: generatePerspective(evaluation, context)
    Zar->>Zar: applyEternalReturn(value)
    Zar-->>DS: Perspective (affirmed)
    DS->>Apo: generatePerspective(evaluation, context)
    Apo->>Apo: evaluateStructure(value)
    Apo-->>DS: Perspective (structured)
    DS->>Last: generatePerspective(evaluation, context)
    Last->>Last: detectWeakness(value)
    Last-->>DS: Perspective (warning if weak)
    DS->>DS: synthesizePerspectives()
    DS-->>Orch: DebateResult (evaluated)
    
    Orch->>Orch: Finalize value
    Orch->>PostgreSQL: Save value
    Orch->>NM: observePhase(COMPLETED)
    NM-->>Orch: Final metrics
    
    Orch-->>Worker: Value generated
    Worker-->>Queue: Job completed
    Queue->>API: Notify completion
    API-->>User: GET /api/values/{id}
```

## 4. Diagrama de Estados (FSM)

El diagrama de estados muestra la máquina de estados finitos del ValueEngine, con todas las transiciones entre fases.

```mermaid
stateDiagram-v2
    [*] --> IDLE: System initialized
    
    IDLE --> DECONSTRUCTION: generateValue(concept)
    
    DECONSTRUCTION --> NIHILISTIC: deconstructionComplete()
    DECONSTRUCTION --> ERROR: deconstructionFailed()
    
    NIHILISTIC --> CREATIVE: voidCreated()
    NIHILISTIC --> ERROR: voidCreationFailed()
    NIHILISTIC --> DECONSTRUCTION: retryDeconstruction()
    
    CREATIVE --> EVALUATION: valueCreated()
    CREATIVE --> ERROR: valueCreationFailed()
    CREATIVE --> NIHILISTIC: retryVoid()
    
    EVALUATION --> COMPLETED: evaluationPassed()
    EVALUATION --> ERROR: evaluationFailed()
    EVALUATION --> CREATIVE: retryCreation()
    
    COMPLETED --> IDLE: reset()
    COMPLETED --> [*]: System shutdown
    
    ERROR --> IDLE: reset()
    ERROR --> DECONSTRUCTION: retryFromStart()
    ERROR --> [*]: System shutdown
    
    note right of DECONSTRUCTION
        Genealogist analyzes
        and deconstructs
        existing values
    end note
    
    note right of NIHILISTIC
        Dionysus creates void,
        LastMan warns of passivity
    end note
    
    note right of CREATIVE
        Zarathustra, Dionysus,
        Apollo create new value
    end note
    
    note right of EVALUATION
        Zarathustra applies
        eternal return,
        Apollo evaluates structure
    end note
```

## 5. Diagrama de Despliegue

El diagrama de despliegue muestra la arquitectura de despliegue del sistema, incluyendo servicios Docker, contenedores y redes.

```mermaid
graph TB
    subgraph "Client Layer"
        Browser[Web Browser<br/>Future Frontend]
        API_Client[API Clients]
    end
    
    subgraph "Application Server"
        API_Container[Fastify API<br/>Container]
        Worker_Container[BullMQ Workers<br/>Container]
    end
    
    subgraph "Docker Network: nietzsche-network"
        subgraph "Database Services"
            PostgreSQL_Container[(PostgreSQL 15<br/>+ pgvector<br/>Container)]
            Neo4j_Container[(Neo4j 5.x<br/>Container)]
            Redis_Container[(Redis 7.x<br/>Container)]
        end
        
        subgraph "LLM Service"
            LMStudio_Container[LM Studio<br/>Local LLM<br/>Container]
        end
        
        subgraph "Monitoring Stack"
            Prometheus_Container[Prometheus<br/>Container]
            Grafana_Container[Grafana<br/>Container]
        end
    end
    
    subgraph "External Storage"
        Corpus_Volume[Corpus Volume<br/>Nietzsche Texts]
        Data_Volume[Data Volume<br/>Exports]
    end
    
    subgraph "Configuration"
        Env_File[.env<br/>Configuration]
        Docker_Compose[docker-compose.yml]
    end
    
    %% Client to API
    Browser -->|HTTPS| API_Container
    API_Client -->|HTTPS| API_Container
    
    %% API to Services
    API_Container -->|SQL| PostgreSQL_Container
    API_Container -->|Cypher| Neo4j_Container
    API_Container -->|Redis Protocol| Redis_Container
    API_Container -->|HTTP| LMStudio_Container
    API_Container -->|HTTP| Prometheus_Container
    
    %% Workers to Services
    Worker_Container -->|SQL| PostgreSQL_Container
    Worker_Container -->|Cypher| Neo4j_Container
    Worker_Container -->|Redis Protocol| Redis_Container
    Worker_Container -->|HTTP| LMStudio_Container
    
    %% Monitoring
    Prometheus_Container -->|Scrape| API_Container
    Prometheus_Container -->|Scrape| Worker_Container
    Grafana_Container -->|Query| Prometheus_Container
    
    %% Storage
    LMStudio_Container -.->|Read| Corpus_Volume
    API_Container -.->|Read/Write| Data_Volume
    Worker_Container -.->|Read/Write| Data_Volume
    
    %% Configuration
    Docker_Compose -.->|Orchestrates| API_Container
    Docker_Compose -.->|Orchestrates| Worker_Container
    Docker_Compose -.->|Orchestrates| PostgreSQL_Container
    Docker_Compose -.->|Orchestrates| Neo4j_Container
    Docker_Compose -.->|Orchestrates| Redis_Container
    Docker_Compose -.->|Orchestrates| LMStudio_Container
    Docker_Compose -.->|Orchestrates| Prometheus_Container
    Docker_Compose -.->|Orchestrates| Grafana_Container
    
    Env_File -.->|Config| API_Container
    Env_File -.->|Config| Worker_Container
    
    style API_Container fill:#e1f5ff
    style Worker_Container fill:#e1f5ff
    style PostgreSQL_Container fill:#fff4e1
    style Neo4j_Container fill:#fff4e1
    style Redis_Container fill:#fff4e1
    style LMStudio_Container fill:#e8f5e9
    style Prometheus_Container fill:#f3e5f5
    style Grafana_Container fill:#f3e5f5
```

## Leyenda y Notas Explicativas

### Convenciones de Diagramas

**Diagrama de Clases:**
- `+` = Método público
- `-` = Atributo privado
- `<<interface>>` = Interfaz
- `-->` = Asociación/uso
- `<|..` = Implementación de interfaz
- `-->` con etiqueta = Relación específica

**Diagrama de Componentes:**
- Rectángulos = Componentes
- Líneas sólidas = Dependencias directas
- Líneas punteadas = Dependencias opcionales
- Subgrafos = Agrupaciones lógicas

**Diagrama de Secuencia:**
- Participantes verticales = Actores/Componentes
- Líneas horizontales = Mensajes/Interacciones
- Flechas sólidas = Llamadas síncronas
- Flechas punteadas = Respuestas
- Rectángulos = Activación

**Diagrama de Estados:**
- Estados = Fases del proceso
- Transiciones = Cambios de estado
- `[*]` = Estado inicial/final
- Notas = Descripciones de estados

**Diagrama de Despliegue:**
- Contenedores = Servicios Docker
- Volúmenes = Almacenamiento persistente
- Redes = Comunicación entre servicios
- Configuración = Archivos de configuración

### Notas Arquitectónicas

1. **Separación de Responsabilidades:**
   - Orchestrator coordina pero no contiene lógica de negocio
   - ValueEngine gestiona solo estados, no lógica de fases
   - Módulos encapsulan lógica específica de cada fase
   - Agentes son independientes y reutilizables

2. **Patrones de Diseño:**
   - **FSM (Finite State Machine):** ValueEngine
   - **Observer:** NihilismMonitor observa ValueEngine
   - **Strategy:** Diferentes agentes para diferentes perspectivas
   - **Repository:** Acceso a datos abstraído
   - **Factory:** Creación de agentes y módulos

3. **Dependencias Externas:**
   - PostgreSQL con pgvector para embeddings
   - Neo4j para relaciones genealógicas
   - Redis para cache y colas
   - LM Studio para LLM local
   - Prometheus/Grafana para monitoreo

4. **Escalabilidad:**
   - Workers pueden escalarse horizontalmente
   - Base de datos puede replicarse
   - Colas distribuyen carga
   - API stateless permite load balancing

## Referencias

- **Issue Linear:** [DNT-226: Crear diagramas UML del sistema](https://linear.app/clasificadoria/issue/DNT-226/docs-crear-diagramas-uml-del-sistema)
- **Epic Padre:** [DNT-224: Epic de Diseño Arquitectónico](https://linear.app/clasificadoria/issue/DNT-224/epic-diseno-arquitectonico-y-diagramas)
- **Casos de Uso:** [docs/use-cases.md](./use-cases.md)
- **Actores:** [docs/actors.md](./actors.md) (si existe)
- **Contexto del Proyecto:** [docs/project-context.md](./project-context.md)

## Notas de Mantenimiento

- Los diagramas deben actualizarse cuando cambie la arquitectura
- Los diagramas están en formato Mermaid para fácil versionado en Git
- Se pueden exportar a imágenes usando herramientas como Mermaid CLI
- Los diagramas reflejan el diseño actual y deben mantenerse sincronizados con la implementación

---

**Última actualización:** 2026-01-11  
**Mantenido por:** Equipo de desarrollo  
**Versión del documento:** 1.0
