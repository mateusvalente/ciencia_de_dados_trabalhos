
# ATIVIDADE — PIPELINE DE DADOS (Bella Massa Pizzaria)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados operacionais em informações úteis para análise de:
- desperdício de ingredientes
- queda no movimento em dias específicos
- cancelamento de pedidos

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

- Criar tabela `bella_massa_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `bella_massa_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null

#### Textos
- Corrigir erros (procesado, calabreza, mussarelaa, quejio)
- Padronizar UF

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores fora do padrão em:
  - desperdicio_g
  - tempo_entrega_min
  - avaliacao_cliente
  - valor_pedido
  - quantidade_ingrediente_g

#### Campos derivados
- criar flag_desperdicio
- criar flag_cancelamento
- criar flag_baixo_movimento
- criar classificacao_sabor

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Desperdício por ingrediente

Mostrar:

ingrediente, desperdicio medio, quantidade utilizada

### Atividade 2 — Vendas por dia

Mostrar:

dia_semana, quantidade pedidos, faturamento medio

### Atividade 3 — Cancelamentos

Mostrar:

motivo_cancelamento, quantidade cancelamentos, tempo medio cancelamento

### Atividade 4 — Promoções

Mostrar:

promocao, quantidade pedidos, ticket medio

### Atividade 5 — Sabores mais vendidos

Mostrar:

sabor_pizza, quantidade vendas, avaliacao media

### Atividade 6 — Tempo de entrega

Mostrar:

cidade, tempo medio entrega, quantidade pedidos

---

## INTERPRETAÇÃO

Responder:

### Desperdício
- Quais ingredientes geram mais perdas?
- Existe relação com validade?

### Movimento
- Quais dias têm menor venda?
- Promoções ajudam?

### Cancelamentos
- Principais motivos?
- A demora impacta?

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
