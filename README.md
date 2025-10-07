# 🧠 Sistema Multi-Agente – Esquema do Banco de Dados

Este projeto utiliza uma arquitetura baseada em múltiplos agentes de IA para auxiliar em tarefas de desenvolvimento, testes e depuração.

---

## 📘 Esquema do Banco (ER Diagram)

```mermaid
erDiagram
    USERS {
        UUID id PK "gen_random_uuid()"
        VARCHAR email "UNIQUE, NOT NULL"
        VARCHAR nome
        VARCHAR senha_hash
        TIMESTAMP created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    AGENTS {
        UUID id PK "gen_random_uuid()"
        VARCHAR name
        VARCHAR role
        VARCHAR ai_provider
        TEXT system_prompt
        TIMESTAMP created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    PROJECTS {
        UUID id PK "gen_random_uuid()"
        UUID user_id FK
        VARCHAR name
        TEXT description
        VARCHAR status "DEFAULT 'em_andamento'"
        TIMESTAMP created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    TASKS {
        UUID id PK "gen_random_uuid()"
        UUID project_id FK
        UUID agent_id FK
        VARCHAR titulo
        TEXT input_usuario
        TEXT output_gerado
        VARCHAR status "DEFAULT 'pendente'"
        TIMESTAMP created_at "DEFAULT CURRENT_TIMESTAMP"
        TIMESTAMP completed_at
    }

    IA_INTERACTIONS {
        UUID id PK "gen_random_uuid()"
        UUID task_id FK
        JSONB messages
        INTEGER tokens_usados
        DECIMAL custo_estimado
        TIMESTAMP created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    USERS ||--o{ PROJECTS : "possui"
    PROJECTS ||--o{ TASKS : "contém"
    AGENTS ||--o{ TASKS : "executa"
    TASKS ||--o{ IA_INTERACTIONS : "registra"
