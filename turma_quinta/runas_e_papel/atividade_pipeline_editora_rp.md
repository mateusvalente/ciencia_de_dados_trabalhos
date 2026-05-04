# ATIVIDADE — PIPELINE DE DADOS (Runas & Papel)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de leitura em informações úteis para análise de:
- avaliação dos leitores
- segmentação de público
- seleção de escritores

---

## OBJETIVOS PEDAGÓGICOS

O grupo deve:

- entender a qualidade dos dados  
- justificar cada tratamento realizado  
- transformar dados brutos em informação útil  

---

## ETAPAS DA ATIVIDADE

### 1. Extrair CSV (NiFi)

- Utilizar o processador `GetHTTP`
- Buscar o arquivo CSV no link fornecido (GitHub)

---

### 2. Converter para XLSX e Salvar no HUE

- Utilizar `ConvertRecord` + `PutFile`
- Gerar arquivo Excel (.xlsx)

---

### 3. Análise ANTES da limpeza Baixe o arquivo no HUE, e Abra no Excel

Abrir o arquivo e responder:

- Quantas linhas existem no dataset?
- Quantos valores nulos existem por coluna?
- Existem duplicatas? Como identificou?
- Existem valores inválidos? Quais?
- Existem inconsistências de formato?
- Existem outliers? Em quais colunas?
- Os outliers parecem erros de cadastro ou situações reais de negócio?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `editora_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `editora_leitura_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null

#### Textos
- Corrigir erros
- Padronizar subgêneros

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores fora do padrão em:
  - avaliacao_capitulo
  - idade_usuario
  - tempo_leitura_min
  - qualidade_texto_score
  - aderencia_genero

#### Campos derivados
- criar flag_engajamento
- criar classificacao_publico
- criar classificacao_escritor

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Avaliação por livro

Mostrar:

```livro, média de avaliação, quantidade de leitores```


### Atividade 2 — Engajamento

Mostrar:

```capitulo, quantidade de avaliações, média de tempo de leitura```


### Atividade 3 — Público

Mostrar:

```subgenero, idade média, quantidade de leitores```


### Atividade 4 — Tags

Mostrar:

```tags, quantidade de uso, avaliação média```


### Atividade 5 — Escritores

Mostrar:

```escritor_id, qualidade média, aderência média```


### Atividade 6 — Interação

Mostrar:

```tipo de interação, quantidade, avaliação média```

---

## INTERPRETAÇÃO

Responder:

### Avaliação
- Leitores avaliam?
- Existe engajamento?

### Público
- Subgêneros estão corretos?
- Público está adequado?

### Escritores
- Qualidade está boa?
- IA ajudaria?

### Qualidade dos dados
- Outliers impactaram?
- Melhorias sugeridas?

---

## RELATÓRIO FINAL

O grupo deve entregar:

### Pipeline
- Print do NiFi
- Explicação das etapas

### Excel
- Respostas do diagnóstico

### Limpeza
- SQL utilizado
- Justificativas
- Análise dos outliers

### Banco
- Print tabela bruta
- Print tabela limpa

### SQL
- Queries
- Prints resultados

### Interpretação
- Respostas e conclusões

---

## CONCLUSÃO

O grupo deve demonstrar capacidade de:

- analisar qualidade dos dados  
- justificar transformações  
- gerar insights úteis
