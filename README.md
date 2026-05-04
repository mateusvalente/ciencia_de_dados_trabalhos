
---

## DESCRIÇÃO DOS ARQUIVOS

### 1. dataset_sujo.csv

Arquivo contendo os dados brutos que serão utilizados no pipeline.

Características:

- Possui dados **intencionalmente sujos**
- Contém:
  - valores nulos
  - formatos inconsistentes
  - erros de digitação
  - duplicatas
  - outliers
- Representa a **origem do ETL (extração)**

Este arquivo deve ser utilizado no:

- Apache NiFi (GetHTTP / ingestão)
- Análise inicial no Excel (antes da limpeza)
- Carga na tabela bruta no PostgreSQL

---

### 2. atividade_pipeline.md

Arquivo com todas as instruções da atividade.

Contém:

- Objetivo da atividade
- Problemas de negócio
- Etapas do pipeline (ETL)
- Orientações de limpeza de dados via SQL
- Atividades em SQL para geração de insights
- Perguntas de interpretação
- Estrutura do relatório final

---

## ORGANIZAÇÃO POR TURMA

Os arquivos estão separados por turma para facilitar o gerenciamento:

Exemplo:
/turma_A/
/orbital_insight/
/ecommerce_eletronicos/

turma_B/
/fixit/
/fastmarket/



---

## ORGANIZAÇÃO POR TRABALHO

Dentro de cada turma, cada grupo possui sua própria pasta com:

- 1 arquivo CSV (dados)
- 1 arquivo MD (instruções)

Exemplo:

/turma_A/orbital_insight/
orbital_dataset_sujo.csv
atividade_pipeline.md


---

## OBJETIVO DA ORGANIZAÇÃO

Essa estrutura foi criada para:

- Separar claramente cada grupo
- Facilitar correção e acompanhamento
- Evitar mistura de datasets
- Garantir reprodutibilidade dos pipelines

---

## OBSERVAÇÃO IMPORTANTE

Cada grupo deve trabalhar **apenas com os arquivos da sua pasta**.

Não é permitido:

- reutilizar datasets de outros grupos
- modificar o CSV original
- ignorar as instruções do `.md`

---

## RESUMO

Cada grupo recebe:

- um dataset sujo (`.csv`)
- um roteiro completo da atividade (`.md`)

E deve:

- construir o pipeline ETL
- limpar os dados
- armazenar no banco
- gerar insights

---