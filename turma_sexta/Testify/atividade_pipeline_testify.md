# ATIVIDADE — PIPELINE DE DADOS (Testify)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de conteúdo e reputação em informações úteis para análise de:
- avaliações falsas
- credenciais fraudulentas
- recomendação de conteúdo relevante

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

---

### 2. Converter para XLSX e Salvar no HUE

- Utilizar `ConvertRecord` + `PutFile`

---

### 3. Análise ANTES da limpeza

Responder:

- Existem avaliações suspeitas?
- Tempo leitura bate com avaliação?
- Existem padrões estranhos?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `testify_raw`

---

### 5. Limpeza via SQL

Criar tabela `testify_limpo`

Tratar:

- datas
- números
- textos
- duplicatas
- outliers

Criar campos:

- flag_avaliacao_falsa
- flag_credencial_falsa
- score_confiabilidade

---

### 6. Gravar dados limpos

---

### 7. Consultar no Postgress

---

## ATIVIDADES SQL

1 — Avaliações suspeitas  
2 — Credenciais inválidas  
3 — Engajamento por tema  
4 — Tempo leitura x avaliação  
5 — Cancelamentos  
6 — Recomendação conteúdo  

---

## INTERPRETAÇÃO

Responder:

- Existem fraudes?
- Como melhorar confiança?
- Como recomendar melhor conteúdo?

---

## RELATÓRIO FINAL

- pipeline
- excel
- limpeza
- banco
- sql
- interpretação

---

## CONCLUSÃO

Analisar dados e gerar insights
