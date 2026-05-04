# ATIVIDADE — PIPELINE DE DADOS (Saber Forgers)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados comerciais em informações úteis para análise de:
- previsão de tendências de mercado
- custos de produção
- fidelização de clientes

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

- Criar tabela `saber_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `saber_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null

#### Textos
- Corrigir erros (procesado)
- Padronizar UF

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores fora do padrão em:
  - preco_venda
  - custo_producao
  - tempo_fabricacao_h
  - frequencia_compra
  - avaliacao_cliente

#### Campos derivados
- criar tendencia_modelo
- criar custo_eficiencia
- criar flag_fidelizacao

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Modelos mais vendidos

Mostrar:

```modelo, quantidade vendida, preco medio```


### Atividade 2 — Tendência por cor

Mostrar:

```cor, quantidade vendas, mes```


### Atividade 3 — Custos

Mostrar:

```modelo, custo medio, preco medio, margem```


### Atividade 4 — Produção vs venda

Mostrar:

```modelo, produzido, vendido, diferenca```


### Atividade 5 — Promoções

Mostrar:

```participou promocao, quantidade vendas, ticket medio```


### Atividade 6 — Fidelização

Mostrar:

```cliente, frequencia, dias ultima compra```

---

## INTERPRETAÇÃO

Responder:

### Tendência
- Quais modelos são populares?
- Cores influenciam?

### Custos
- Margem é adequada?
- Onde reduzir custo?

### Fidelização
- Clientes retornam?
- Estratégias possíveis?

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
