# ATIVIDADE — PIPELINE DE DADOS (Orbital Insight)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados geográficos em informações úteis para análise de:
- risco de incêndio  
- desmatamento  
- produtividade agrícola  
- crescimento urbano  

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
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `orbital_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `orbital_monitoramento_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Coordenadas
- Converter para número
- Validar se está dentro do Brasil:
  - latitude: -34 a 6
  - longitude: -74 a -34

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null

#### Textos
- Corrigir erros (urbnao, procesado, etc.)
- Padronizar UF (mg → MG)

#### Duplicatas
- Remover por `registro_id`

#### Campos derivados
- Criar variacao_ndvi
- Criar classificações:
  - problema_desmatamento
  - problema_agricola
  - problema_urbano

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Risco de incêndio por cidade

Mostrar:

```cidade, UF, risco médio, quantidade de registros```


### Atividade 2 — Áreas críticas por região

Mostrar:

```região, quantidade de áreas críticas```


### Atividade 3 — Possível desmatamento

Mostrar:

```cidade, UF, latitude, longitude, NDVI, risco```


### Atividade 4 — Produtividade agrícola

Mostrar:

```cultura, produtividade média, NDVI médio, umidade```


### Atividade 5 — Clima x incêndio

Mostrar:

```classe de risco, temperatura, umidade, dias sem chuva```


### Atividade 6 — Crescimento urbano

Mostrar:

```cidade, UF, expansão urbana, densidade```
---

## INTERPRETAÇÃO

Responder:

### Incêndios
- Quais regiões têm maior risco?
- Existe relação com temperatura e seca?

### Desmatamento
- Onde estão os maiores indícios?
- NDVI confirma?

### Agricultura
- Quais culturas são mais produtivas?
- Relação com NDVI e umidade?

### Crescimento urbano
- Quais cidades crescem mais?
- Crescimento planejado ou não?

### Qualidade dos dados
- Problemas impactaram resultados?
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
