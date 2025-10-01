# Arquitetura do Banco de Dados do Projeto

Abaixo está o Diagrama de Entidade-Relacionamento (ER) que descreve a estrutura dos nossos bancos de dados (Relacional e NoSQL).

```mermaid
erDiagram
    usuarios {
        UUID id PK
        VARCHAR nome
        VARCHAR email
        TIMESTAMP criado_em
    }

    agentes {
        UUID id PK
        VARCHAR nome
        VARCHAR tipo
        TIMESTAMP criado_em
    }

    relacoes_agentes {
        UUID id PK
        UUID agente_origem_id FK
        UUID agente_destino_id FK
        VARCHAR tipo_comunicacao
        TIMESTAMP criado_em
    }

    interacoes {
        UUID id PK
        UUID usuario_id FK
        UUID agente_id FK
        TEXT prompt
        STRING resposta_id "FK para NoSQL"
        TIMESTAMP criado_em
    }

    "respostas (NoSQL)" {
        STRING _id PK
        STRING interacaoId
        TEXT codigoGerado
        JSON arquivosGerados
        JSON logsAgentes
        STRING feedbackUsuario
        TIMESTAMP criadoEm
    }

    usuarios ||--o{ interacoes : "inicia"
    agentes  ||--o{ interacoes : "participa"
    agentes  ||--o{ relacoes_agentes
    agentes  ||--o{ relacoes_agentes
    interacoes ||--|| "respostas (NoSQL)" : "gera"
```

## Próximos Passos
- Implementar as migrations do banco de dados.
- Definir os modelos de dados na aplicação.
