# ATIVIDADE — PIPELINE DE DADOS (FastMarket)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de compras e entregas rápidas em informações úteis para análise de:
- demora na separação dos pedidos
- cancelamento de pedidos
- sugestão de produtos relevantes
- desempenho operacional das lojas parceiras

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

- Criar tabela `fastmarket_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `fastmarket_pedidos_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos numéricos:
  - quantidade_itens
  - produtos_indisponiveis
  - funcionarios_disponiveis
  - volume_pedidos_simultaneos
  - horario_pedido
  - tempo_separacao_min
  - tempo_entrega_estimado_min
  - tempo_entrega_real_min
  - valor_pedido
  - avaliacao_cliente
  - frequencia_compra_mes
  - dias_desde_ultima_compra

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar categoria principal:
  - horti fruti → hortifruti
  - conveniência → conveniencia
- Padronizar tipo de produto:
  - nao perecivel → nao_perecivel
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - tempo_separacao_min
  - tempo_entrega_real_min
  - quantidade_itens
  - funcionarios_disponiveis
  - avaliacao_cliente
  - valor_pedido
  - frequencia_compra_mes
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar atraso_entrega_min
- Criar flag_atraso_entrega
- Criar flag_cancelamento
- Criar flag_baixa_recorrencia
- Criar classificações:
  - risco_demora_separacao
  - risco_cancelamento
  - oportunidade_recomendacao_produto

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Tempo de separação por loja

Mostrar:

```loja, quantidade de pedidos, tempo médio de separação, média de itens por pedido```


### Atividade 2 — Impacto do horário de pico

Mostrar:

```período de pico, quantidade de pedidos, tempo médio de separação, tempo médio de entrega```


### Atividade 3 — Cancelamentos por motivo

Mostrar:

```motivo do cancelamento, quantidade de pedidos cancelados, avaliação média```


### Atividade 4 — Indisponibilidade de produtos

Mostrar:

```categoria principal, produtos indisponíveis médios, taxa de cancelamento```


### Atividade 5 — Recorrência dos clientes

Mostrar:

```cliente, frequência de compra no mês, dias desde última compra, valor médio do pedido```


### Atividade 6 — Sugestão de produtos por categoria

Mostrar:

```categoria principal, quantidade de pedidos, valor médio do pedido, frequência média de compra```

---

## INTERPRETAÇÃO

Responder:

### Separação de pedidos
- Quais lojas apresentam maior demora na separação?
- O número de itens e pedidos simultâneos influencia o tempo?
- A quantidade de funcionários parece suficiente?

### Cancelamentos
- Quais são os principais motivos de cancelamento?
- A indisponibilidade de produtos aumenta cancelamentos?
- A demora na entrega prejudica a avaliação?

### Recomendação de produtos
- Quais categorias são mais recorrentes?
- Os dados ajudam a sugerir produtos relevantes?
- Como cupons e histórico de compras poderiam ser usados?

### Qualidade dos dados
- Problemas impactaram resultados?
- Outliers alteraram médias ou conclusões?
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
- Explicação dos outliers encontrados e decisão tomada

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
