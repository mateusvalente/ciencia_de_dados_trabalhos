# ATIVIDADE — PIPELINE DE DADOS (Flash Pet Care)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de atendimento veterinário em informações úteis para análise de:
- eficiência de triagem (IA)
- tempo de espera e atendimento
- qualidade do serviço (avaliação do tutor)
- retorno do paciente (fidelização)

---

## OBJETIVOS PEDAGÓGICOS

O grupo deve:
- entender a qualidade dos dados
- justificar cada tratamento realizado
- transformar dados brutos em informação útil

---

## ETAPAS DA ATIVIDADE

### 1. Extrair CSV (NiFi)
- Utilizar `GetHTTP`
- Buscar o CSV no GitHub

---

### 2. Converter para XLSX e Salvar no HUE
- Utilizar `ConvertRecord` + `PutFile`
- Gerar Excel (.xlsx)

---

### 3. Análise ANTES da limpeza (HUE → Excel)
Abrir o arquivo e responder:
- Quantas linhas existem?
- Quantos nulos por coluna?
- Existem duplicatas?
- Existem valores inválidos?
- Existem inconsistências de formato?
- Existem outliers? Em quais colunas?
- Os outliers parecem erros ou casos reais?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL
- Criar `flash_raw`
- Inserir sem tratamento

---

### 5. Limpeza via SQL
Criar `flash_atendimentos_limpo`

Tratar:

#### Datas
- Padronizar formatos e converter para DATE
- Remover inválidos

#### Números
- Corrigir vírgula decimal
- Tratar NA, vazio, null

#### Textos
- Padronizar status e UF
- Corrigir erros (procesado → processado)

#### Duplicatas
- Remover por `registro_id`

#### Valores inválidos
- tempo_espera_min < 0
- temperatura fora de faixa plausível
- frequência cardíaca incoerente

#### Outliers
- Identificar outliers em:
  - tempo_espera_min
  - tempo_atendimento_min
  - temperatura_corporal_c
  - frequencia_cardiaca
  - avaliacao_tutor
- Classificar como:
  - erro de cadastro
  - caso real extremo
  - dado suspeito

#### Campos derivados
- criar tempo_total = espera + atendimento
- criar flag_critico (prioridade_ia = 'critico')
- criar flag_retorno (retorno_7d = 'sim')

---

### 6. Gravar dados limpos no Postgres
- Criar tabelas finais
- Inserir dados tratados

---

### 7. Consultar no Postgres
Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Tempo médio por prioridade
Mostrar: prioridade_ia, tempo médio de espera e atendimento

### Atividade 2 — Gargalos de triagem
Mostrar: cidade, média de espera, % de casos críticos

### Atividade 3 — Qualidade do atendimento
Mostrar: média de avaliação por cidade e prioridade

### Atividade 4 — Retorno de pacientes
Mostrar: % de retorno em 7 dias por cidade e prioridade

### Atividade 5 — Relação espera x avaliação
Mostrar: faixas de espera, avaliação média
Observar impacto de outliers

### Atividade 6 — Casos críticos
Mostrar: quantidade de casos críticos por cidade
Identificar possíveis sobrecargas

---

## INTERPRETAÇÃO

### Triagem
- A IA está priorizando corretamente os casos críticos?

### Atendimento
- Onde há maior tempo de espera?
- Isso impacta a avaliação?

### Fidelização
- Pacientes retornam?
- O retorno está ligado à qualidade?

### Qualidade dos dados
- Outliers mudaram as conclusões?
- Quais devem ser mantidos?

---

## RELATÓRIO FINAL

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
