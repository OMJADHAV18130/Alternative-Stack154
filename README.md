┌─────────────────────────────────────────────────────────────────────────────┐
│                              OPERATOR / USER                                │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   │ HTTPS
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         REACT DASHBOARD                                     │
│                    Vite + Tailwind CSS                                      │
│                                                                             │
│  ┌──────────────┐ ┌──────────────┐ ┌────────────────┐ ┌──────────────────┐ │
│  │ File Upload  │ │ Prompt/Input │ │ Output Select  │ │ Generation Params│ │
│  │              │ │              │ │                │ │                  │ │
│  │ PDF DOCX     │ │ Instructions │ │ Summary        │ │ Language         │ │
│  │ PPTX XLSX    │ │ Context      │ │ Advisory       │ │ Tone             │ │
│  │ CSV TXT      │ │              │ │ Presentation    │ │ Audience         │ │
│  │ Images        │ │              │ │ Social Media   │ │ Detail Level     │ │
│  └──────────────┘ └──────────────┘ └────────────────┘ └──────────────────┘ │
│                                                                             │
│                  Job Progress / Output Preview / Downloads                  │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   │ REST API
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                    SPRING BOOT ENTERPRISE CORE                              │
│                         Java 17+ / Spring Boot 3                            │
│                                                                             │
│ ┌────────────────┐  ┌────────────────┐  ┌────────────────────────────────┐ │
│ │ Spring Security│  │ REST Controllers│ │ Transformation Job Service     │ │
│ │                │  │                │ │                                │ │
│ │ Authentication │  │ /jobs          │ │ Job creation                   │ │
│ │ Authorization  │  │ /files         │ │ Status tracking                │ │
│ │ JWT            │  │ /outputs       │ │ Request validation             │ │
│ └────────────────┘  └────────────────┘ │ AI-engine orchestration         │ │
│                                        └────────────────────────────────┘ │
│                                                                             │
│ ┌──────────────────────┐     ┌───────────────────────────────────────────┐ │
│ │ File / Job Metadata  │     │ FastAPI AI Engine Client                 │ │
│ │                      │     │                                           │ │
│ │ TransformationJob    │────►│ Submit transformation request            │ │
│ │ User                 │     │ Poll / receive status                    │ │
│ │ InputFile            │     │ Receive generated artifacts              │ │
│ │ OutputArtifact       │     └───────────────────────────────────────────┘ │
│ └───────────┬──────────┘                                                   │
└─────────────┼───────────────────────────────────────────────────────────────┘
              │
              │ JPA / JDBC
              ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                              POSTGRESQL                                     │
│                                                                             │
│ Users │ Jobs │ Input Metadata │ Output Metadata │ Job Status │ Audit Data  │
└─────────────────────────────────────────────────────────────────────────────┘


                              AI PROCESSING
                                    │
                                    │ HTTP / Internal Network
                                    ▼

┌─────────────────────────────────────────────────────────────────────────────┐
│                         FASTAPI AI ENGINE                                   │
│                       Python 3.11+ / LangChain                             │
│                                                                             │
│                         Transformation API                                 │
│                                │                                            │
│                                ▼                                            │
│                     ┌─────────────────────┐                                 │
│                     │ Request Orchestrator│                                 │
│                     └──────────┬──────────┘                                 │
│                                │                                            │
│             ┌──────────────────┼───────────────────┐                        │
│             │                  │                   │                        │
│             ▼                  ▼                   ▼                        │
│      Input Processor      Parameter        Output Manager                  │
│                          Processor                                          │
└─────────────┬───────────────────────────────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         INPUT INGESTION                                     │
│                                                                             │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌───────────────┐ │
│  │  PDF   │ │ DOCX   │ │  PPTX  │ │  XLSX  │ │  CSV   │ │ TXT / Prompt  │ │
│  └────┬───┘ └────┬───┘ └────┬───┘ └────┬───┘ └────┬───┘ └──────┬────────┘ │
│       │          │          │          │          │              │          │
│       └──────────┴──────────┴──────────┴──────────┴──────────────┘          │
│                                   │                                         │
│                                   ▼                                         │
│                        Document Extractors                                  │
│                                                                             │
│              Text │ Tables │ Metadata │ Images │ Structure                 │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                       CONTENT NORMALIZATION                                 │
│                                                                             │
│   Cleaning → Deduplication → Language Detection → Metadata → Chunking      │
│                                                                             │
│                    ↓                                                        │
│              Unified Document Model                                         │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           RAG PIPELINE                                      │
│                                                                             │
│                       Document Chunks                                       │
│                            │                                                │
│                            ▼                                                │
│                       Embedding Model                                       │
│                            │                                                │
│                            ▼                                                │
│                       Vector Store                                          │
│                            │                                                │
│                            │ Similarity Search                              │
│                            ▼                                                │
│                         Retriever                                           │
│                            │                                                │
│                            ▼                                                │
│                      Relevant Context                                       │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                       ANALYSIS AGENT                                        │
│                                                                             │
│  Understand source material                                                 │
│  Extract facts                                                              │
│  Identify entities                                                          │
│  Identify events                                                            │
│  Extract dates / locations / organizations                                   │
│  Identify risks / key findings                                              │
│  Resolve relevant retrieved context                                         │
│  Generate structured source understanding                                   │
│                                                                             │
│                              │                                              │
│                              ▼                                              │
│                    CANONICAL CONTEXT                                        │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                       AGENT ORCHESTRATOR                                    │
│                                                                             │
│             Reads selected output types from operator                      │
│                                                                             │
│                         ┌──────────────┐                                    │
│                         │ Task Planner │                                    │
│                         └──────┬───────┘                                    │
│                                │                                            │
│               Parallel execution where possible                             │
│                                │                                            │
│          ┌─────────────────────┼──────────────────────┐                     │
│          │                     │                      │                     │
│          ▼                     ▼                      ▼                     │
│ ┌─────────────────┐  ┌─────────────────┐  ┌────────────────────────┐       │
│ │ Executive       │  │ Advisory        │  │ Presentation           │       │
│ │ Summary Agent   │  │ Agent           │  │ Agent                  │       │
│ └────────┬────────┘  └────────┬────────┘  └───────────┬────────────┘       │
│          │                    │                       │                     │
│          ▼                    ▼                       ▼                     │
│ ┌─────────────────┐  ┌─────────────────┐  ┌────────────────────────┐       │
│ │ LinkedIn Agent  │  │ Twitter/X Agent │  │ Infographic Agent      │       │
│ └─────────────────┘  └─────────────────┘  └────────────────────────┘       │
│                                                                             │
│                         Optional                                           │
│                    ┌─────────────────┐                                      │
│                    │ Video Package   │                                      │
│                    │ Agent           │                                      │
│                    └─────────────────┘                                      │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                     OUTPUT VALIDATION LAYER                                 │
│                                                                             │
│  Pydantic Schemas                                                           │
│  Schema Validation                                                          │
│  Required Fields                                                            │
│  Content Consistency                                                        │
│  Source Grounding                                                           │
│  Length / Format Rules                                                      │
│  Safety / Policy Checks                                                     │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                       OUTPUT GENERATION                                     │
│                                                                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────────────────┐ │
│  │ PDF         │ │ DOCX        │ │ PPTX        │ │ TXT / JSON           │ │
│  │ Generator   │ │ Generator   │ │ Generator   │ │ Generator            │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────────────────┘ │
│                                                                             │
│              Structured AI Output → Final Artefact                         │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         OUTPUT STORAGE                                      │
│                                                                             │
│        Generated Files + Metadata + Job Status + Version                   │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   │
                                   ▼
                            Spring Boot API
                                   │
                                   ▼
                            React Dashboard
                                   │
                      ┌────────────┼─────────────┐
                      ▼            ▼             ▼
                   Preview      Download       History
