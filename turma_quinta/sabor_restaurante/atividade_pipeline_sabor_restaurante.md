# ATIVIDADE — PIPELINE DE DADOS (SABOR Restaurante)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados operacionais em informações úteis para análise de:
- queda nas vendas do delivery
- desperdício de alimentos
- churn de clientes

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
- Os outliers parecem erros ou situações reais?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `sabor_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `sabor_limpo`

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
  - tempo_entrega_min
  - quantidade_produzida
  - ticket_medio
  - avaliacao
  - frequencia_cliente_mes

#### Campos derivados
- criar flag_queda_delivery
- criar flag_desperdicio
- criar flag_churn
- criar classificacao_cliente

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Vendas por dia

Mostrar:

```dia_semana, quantidade pedidos, ticket medio```


### Atividade 2 — Delivery vs local

Mostrar:

```tipo_pedido, quantidade, ticket medio, tempo entrega```


### Atividade 3 — Desperdício

Mostrar:

```prato, produzido, vendido, desperdicio```


### Atividade 4 — Avaliação

Mostrar:

```prato, avaliacao media, quantidade pedidos```


### Atividade 5 — Promoções

Mostrar:

```promocao, quantidade pedidos, ticket medio```


### Atividade 6 — Churn

Mostrar:

```cliente, frequencia, dias ultimo pedido``` 

---

## INTERPRETAÇÃO

Responder:

### Delivery
- Há queda nos fins de semana?
- Motivos?

### Desperdício
- Quais pratos sobram?
- Ajustes possíveis?

### Churn
- Clientes estão saindo?
- Como evitar?

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
