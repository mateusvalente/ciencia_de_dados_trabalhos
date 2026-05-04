# ATIVIDADE — PIPELINE DE DADOS (Farmarun)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de vendas, delivery e fidelização em informações úteis para análise de:
- queda nas vendas
- baixa utilização do delivery
- falta de fidelização de clientes

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
- Salvar o arquivo no HUE antes de iniciar a limpeza

---

### 3. Análise ANTES da limpeza Baixe o arquivo no HUE, e Abra no Excel

Abrir o arquivo e responder:

- Quantas linhas existem no dataset?
- Quantos valores nulos existem por coluna?
- Existem duplicatas? Como identificou?
- Existem valores inválidos? Quais?
- Existem inconsistências de formato?
- Existem outliers? Em quais colunas?
- Os outliers parecem erros de cadastro ou situações reais do negócio?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `farmarun_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

Campos esperados no CSV:

```text
pedido_id
cliente_id
data_pedido
cidade
uf
regiao
latitude
longitude
canal_venda
categoria_produto
produto
quantidade
preco_unitario
preco_concorrente
desconto_pct
valor_total
forma_pagamento
cupom_promocional
pedido_delivery
distancia_km
tempo_entrega_min
status_delivery
avaliacao_delivery
participa_fidelidade
compras_ultimos_90d
dias_desde_ultima_compra
nps_cliente
status_pedido
observacao
```

---

### 5. Limpeza via SQL

Criar tabela `farmarun_vendas_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover ou separar datas inválidas

#### Cidade, UF e região
- Padronizar nomes de cidades
- Padronizar UF em letras maiúsculas
- Validar se latitude e longitude pertencem ao território brasileiro:
  - latitude: -34 a 6
  - longitude: -74 a -34

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter para tipos numéricos:
  - quantidade
  - preco_unitario
  - preco_concorrente
  - desconto_pct
  - valor_total
  - distancia_km
  - tempo_entrega_min
  - avaliacao_delivery
  - compras_ultimos_90d
  - dias_desde_ultima_compra
  - nps_cliente

#### Textos
- Corrigir erros de digitação e padronizar categorias

Exemplos:

```text
medicamneto -> medicamento
remedio -> medicamento
loja fisica -> loja_fisica
loja -> loja_fisica
delivey -> delivery
entrega -> delivery
cartao credito -> cartao_credito
credito -> cartao_credito
cartao debito -> cartao_debito
entrgue -> entregue
atrazado -> atrasado
canceldo -> cancelado
pendete -> pendente
não -> nao
S -> sim
N -> nao
```

#### Valores inválidos
- Remover ou separar registros com:
  - desconto menor que 0 ou maior que 100
  - NPS menor que 0 ou maior que 10
  - tempo de entrega menor que 1
  - valor total negativo
  - latitude/longitude fora do Brasil

#### Outliers
- Identificar valores muito fora do padrão em:
  - quantidade
  - preco_unitario
  - valor_total
  - distancia_km
  - tempo_entrega_min
  - compras_ultimos_90d
- O grupo não deve apagar outliers automaticamente.
- Cada outlier deve ser analisado e classificado como:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa de validação
- Sugestões de métodos:
  - regra de negócio
  - análise por mínimo, máximo e média
  - comparação com mediana
  - método IQR, quando possível

#### Duplicatas
- Remover duplicatas por `pedido_id`
- Manter apenas um registro válido

#### Campos derivados
- Criar `diferenca_preco_concorrente`
- Criar `ticket_medio`
- Criar `pedido_delivery_bool`
- Criar `cliente_fidelizado_bool`
- Criar classificações:
  - problema_queda_vendas
  - problema_delivery
  - problema_fidelizacao

Regras sugeridas:

```text
problema_queda_vendas:
valor_total baixo, produto sem promoção ou preço acima do concorrente

problema_delivery:
pedido_delivery = sim e tempo_entrega_min alto ou avaliacao_delivery baixa

problema_fidelizacao:
participa_fidelidade = nao ou compras_ultimos_90d <= 1 ou dias_desde_ultima_compra alto
```

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

Sugestão de tabela final:

```text
farmarun_vendas_limpo
```

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Vendas por período e canal

Mostrar:

```text
mês, canal de venda, quantidade de pedidos, faturamento total, ticket médio
```

Objetivo: identificar em quais canais e períodos ocorre maior ou menor volume de vendas.

---

### Atividade 2 — Produtos e categorias com menor desempenho

Mostrar:

```text
categoria, produto, quantidade vendida, faturamento total, ticket médio
```

Objetivo: identificar produtos ou categorias que podem estar contribuindo para a queda nas vendas.

---

### Atividade 3 — Comparação com preço da concorrência

Mostrar:

```text
categoria, produto, preço médio Farmarun, preço médio concorrente, diferença média de preço
```

Objetivo: verificar se produtos com preço maior que o concorrente vendem menos.

---

### Atividade 4 — Desempenho do delivery por cidade

Mostrar:

```text
cidade, UF, quantidade de pedidos delivery, tempo médio de entrega, avaliação média do delivery
```

Objetivo: identificar cidades onde o delivery tem baixa qualidade ou baixa adesão.

---

### Atividade 5 — Relação entre tempo de entrega e avaliação

Mostrar:

```text
faixa de tempo de entrega, quantidade de pedidos, avaliação média, percentual de atrasos
```

Objetivo: analisar se atrasos prejudicam a avaliação do serviço de entrega.

Nesta atividade, o grupo também deve observar se existem outliers de tempo de entrega que distorcem a média.

---

### Atividade 6 — Fidelização de clientes

Mostrar:

```text
participa_fidelidade, quantidade de clientes, média de compras nos últimos 90 dias, ticket médio, NPS médio
```

Objetivo: comparar clientes fidelizados e não fidelizados.

O grupo deve verificar se clientes com número muito alto de compras nos últimos 90 dias são clientes reais de alta frequência ou possíveis erros de cadastro.

---

## INTERPRETAÇÃO

Responder:

### Queda nas vendas
- Quais canais apresentam menor faturamento?
- Quais categorias ou produtos vendem menos?
- O preço da Farmarun parece maior que o da concorrência em produtos importantes?
- Promoções parecem influenciar o volume de vendas?

### Delivery
- Em quais cidades o delivery apresenta pior desempenho?
- O tempo de entrega está relacionado com avaliações menores?
- A distância parece afetar o tempo de entrega?
- Que ações poderiam aumentar o uso do delivery?

### Fidelização
- Clientes fidelizados compram mais?
- Clientes não fidelizados ficam mais tempo sem comprar?
- O NPS dos clientes fidelizados é diferente dos não fidelizados?
- Que estratégias poderiam aumentar a recompra?

### Qualidade dos dados
- Os problemas encontrados no início impactaram os resultados?
- Alguma decisão poderia ser prejudicada por dados sujos?
- Os outliers encontrados mudaram a interpretação das médias?
- Algum outlier deveria ser mantido por representar uma situação real do negócio?
- Quais campos precisam de melhor padronização na coleta?
- Que melhorias você faria no processo de cadastro e registro de vendas?

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
- Explicação dos outliers encontrados e decisão tomada para cada tipo

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
