# ATIVIDADE — PIPELINE DE DADOS (Amazon E-commerce)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de pedidos, logística e comportamento de compra em informações úteis para análise de:
- atrasos nas entregas logísticas
- baixa satisfação dos clientes e devoluções
- recomendação de produtos para aumento de ticket médio
- desempenho de vendedores e categorias

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

- Criar tabela `amazon_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `amazon_pedidos_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos numéricos:
  - valor_produto
  - valor_frete
  - prazo_estimado_dias
  - tempo_processamento_h
  - tempo_transporte_h
  - distancia_cd_cliente_km
  - volume_pacotes_rota
  - avaliacao_cliente

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar categoria do produto:
  - eletronico → eletronicos
  - super mercado → supermercado
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - tempo_transporte_h
  - distancia_cd_cliente_km
  - valor_produto
  - valor_frete
  - volume_pacotes_rota
  - avaliacao_cliente
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar tempo_total_entrega_h
- Criar flag_atraso_entrega
- Criar flag_devolucao
- Criar classificações:
  - risco_atraso_logistico
  - baixa_satisfacao
  - potencial_cross_sell

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Atrasos por cidade

Mostrar:

```cidade, UF, quantidade de pedidos, quantidade de atrasos, taxa de atraso```


### Atividade 2 — Tempo médio de entrega por evento sazonal

Mostrar:

```evento sazonal, tempo médio de processamento, tempo médio de transporte, taxa de atraso```


### Atividade 3 — Devoluções por categoria

Mostrar:

```categoria do produto, quantidade de devoluções, taxa de devolução, avaliação média```


### Atividade 4 — Satisfação por tipo de vendedor

Mostrar:

```tipo de vendedor, avaliação média, taxa de devolução, quantidade de pedidos```


### Atividade 5 — Impacto do frete e Prime

Mostrar:

```prime, valor médio do frete, taxa de atraso, avaliação média```


### Atividade 6 — Recomendação e venda cruzada

Mostrar:

```categoria do produto, quantidade de itens comprados junto, quantidade em wishlist, valor médio do produto```

---

## INTERPRETAÇÃO

Responder:

### Logística
- Quais cidades ou períodos apresentam mais atrasos?
- Eventos sazonais aumentam o tempo de entrega?
- A distância ou volume de pacotes parece impactar a entrega?

### Satisfação e devolução
- Quais categorias geram mais devoluções?
- Marketplace e venda direta apresentam diferenças?
- Atrasos impactam a avaliação do cliente?

### Recomendação
- Quais categorias têm maior potencial de venda cruzada?
- Wishlist e comprado junto ajudam a recomendar produtos?
- Quais ações poderiam aumentar o ticket médio?

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
