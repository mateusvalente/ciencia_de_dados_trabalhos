# ATIVIDADE — PIPELINE DE DADOS (VitrineOn)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de e-commerce em informações úteis para análise de:
- abandono de carrinho
- devoluções
- baixa recorrência de clientes

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

- Quantas linhas existem?
- Existem nulos?
- Existem duplicatas?
- Existem inconsistências?
- Existem outliers?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `vitrine_raw`

---

### 5. Limpeza via SQL

Criar tabela `vitrine_limpo`

Tratar:

- datas
- números
- textos
- duplicatas
- outliers

Criar:

- flag_abandono
- flag_devolucao
- flag_recorrencia

---

### 6. Gravar dados limpos

---

### 7. Consultar no Postgress

---

## ATIVIDADES SQL

1 — Abandono carrinho  
2 — Devoluções  
3 — Conversão  
4 — Origem vendas  
5 — Recorrência  
6 — Ticket médio  

---

## INTERPRETAÇÃO

Responder:

- Onde perde venda?
- Por que devolvem?
- Como aumentar recorrência?

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
