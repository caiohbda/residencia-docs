# Diagrama ER do Sistema

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
        VARCHAR papel
    }

    interacoes {
        UUID id PK
        UUID usuario_id FK
        UUID conexao_id FK
        TEXT prompt
        STRING resposta_id
        TIMESTAMP criado_em
    }

    respostas {
        STRING _id PK
        STRING interacaoId
        JSON codigoGerado
        JSON arquivosGerados
        JSON logsAgentes
        STRING feedbackUsuario
        TIMESTAMP criadoEm
    }

    usuarios ||--o{ interacoes : "inicia"
    conexoes ||--o{ interacoes : "gera"
    conexoes ||--o{ conexao_agentes : "tem"
    agentes  ||--o{ conexao_agentes : "participa"
    interacoes ||--|| respostas : "produz"
