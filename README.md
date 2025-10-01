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
        VARCHAR tipo "backend, frontend, QA, etc."
        TIMESTAMP criado_em
    }

    conexoes {
        UUID id PK
        VARCHAR descricao
        VARCHAR tipo_comunicacao
        TIMESTAMP criado_em
    }

    conexao_agentes {
        UUID id PK
        UUID conexao_id FK
        UUID agente_id FK
        VARCHAR papel "gerador, validador, etc."
    }

    interacoes {
        UUID id PK
        UUID usuario_id FK
        UUID conexao_id FK
        TEXT prompt
        STRING resposta_id "FK para NoSQL"
        TIMESTAMP criado_em
    }

    "respostas (NoSQL)" {
        STRING _id PK
        STRING interacaoId
        JSON codigoGerado
        JSON arquivosGerados
        JSON logsAgentes
        STRING feedbackUsuario
        TIMESTAMP criadoEm
    }

    usuarios ||--o{ interacoes : inicia
    conexoes ||--o{ conexao_agentes : envolve
    agentes  ||--o{ conexao_agentes : participa
    conexoes ||--o{ interacoes : gera
    interacoes ||--|| "respostas (NoSQL)" : produz
