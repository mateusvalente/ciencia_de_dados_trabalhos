# ATIVIDADE — PIPELINE DE DADOS (E-commerce de Eletrônicos)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de navegação, carrinho e pagamento em informações úteis para análise de:
- abandono de carrinho
- falha no pagamento
- baixa conversão
- ações comerciais como cupom e frete grátis

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

- Criar tabela `ecommerce_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `ecommerce_eventos_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos numéricos:
  - preco_produto
  - valor_frete
  - desconto_pct
  - tempo_site_seg
  - quantidade_cliques
  - avaliacao_experiencia

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar categoria do produto:
  - smartfone → smartphone
  - notbook → notebook
- Padronizar etapa do funil:
  - pagto → pagamento
  - carrino → carrinho
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - preco_produto
  - valor_frete
  - desconto_pct
  - tempo_site_seg
  - quantidade_cliques
  - avaliacao_experiencia
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar taxa_conversao
- Criar flag_abandono_carrinho
- Criar flag_falha_pagamento
- Criar classificações:
  - abandono_carrinho
  - falha_pagamento
  - baixa_conversao

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Abandono de carrinho por categoria

Mostrar:

```categoria do produto, quantidade de carrinhos, quantidade de abandonos, taxa de abandono```


### Atividade 2 — Falhas de pagamento

Mostrar:

```motivo da falha, quantidade de ocorrências, valor médio do produto```


### Atividade 3 — Conversão por origem de tráfego

Mostrar:

```origem do tráfego, quantidade de acessos, quantidade de compras, taxa de conversão```


### Atividade 4 — Impacto do frete na conversão

Mostrar:

```faixa de frete, quantidade de pedidos, taxa de conversão, valor médio do produto```


### Atividade 5 — Uso de cupom e desconto

Mostrar:

```cupom utilizado, desconto médio, quantidade de compras, taxa de conversão```


### Atividade 6 — Experiência do usuário

Mostrar:

```dispositivo, avaliação média, tempo médio no site, quantidade média de cliques```

---

## INTERPRETAÇÃO

Responder:

### Abandono de carrinho
- Quais categorias apresentam maior abandono?
- O frete parece influenciar o abandono?
- Que ações poderiam reduzir o abandono?

### Falha no pagamento
- Quais são os principais motivos de falha?
- Existe relação entre valor do produto e falha no pagamento?
- Que melhorias poderiam ser feitas no checkout?

### Conversão
- Quais canais geram maior conversão?
- Cupom e desconto melhoram os resultados?
- O dispositivo utilizado influencia a compra?

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
