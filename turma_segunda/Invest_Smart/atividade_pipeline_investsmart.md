# ATIVIDADE — PIPELINE DE DADOS (InvestSmart)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados financeiros e de comportamento dos investidores em informações úteis para análise de:
- tomada de decisão de compra e venda
- rentabilidade dos investidores
- recomendação de investimentos
- comparação com benchmark de mercado

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
- Os outliers parecem erros de cadastro ou casos reais do mercado financeiro?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `investsmart_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `investsmart_operacoes_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Ativos e setores
- Padronizar códigos de ativos
- Padronizar nomes de setores
- Remover ou separar ativos vazios ou inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos financeiros para formato numérico:
  - preco
  - volume
  - pl
  - roe
  - dy
  - volatilidade
  - rentabilidade_usuario
  - benchmark_ibov
  - taxa_operacao

#### Textos
- Corrigir erros de digitação
- Padronizar valores de recomendação:
  - comprar → compra
  - vend → venda
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - preco
  - volume
  - rentabilidade_usuario
  - taxa_operacao
  - volatilidade
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - valor extremo possível no mercado
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar lucro_vs_ibov
- Criar flag_prejuizo
- Criar classificações:
  - decisao_compra
  - baixa_rentabilidade
  - recomendacao_investimento

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Rentabilidade por ativo

Mostrar:

```ativo, setor, rentabilidade média, quantidade de operações```


### Atividade 2 — Comparação com o Ibovespa

Mostrar:

```ativo, rentabilidade média, benchmark médio, diferença em relação ao Ibovespa```


### Atividade 3 — Perfil de risco dos usuários

Mostrar:

```perfil do usuário, rentabilidade média, volatilidade média, quantidade de operações```


### Atividade 4 — Recomendações da IA

Mostrar:

```recomendação da IA, quantidade de ativos, rentabilidade média, volatilidade média```


### Atividade 5 — Impacto das taxas na rentabilidade

Mostrar:

```faixa de taxa, rentabilidade média, quantidade de operações```


### Atividade 6 — Ativos com maior risco

Mostrar:

```ativo, setor, volatilidade média, rentabilidade média, quantidade de operações```

---

## INTERPRETAÇÃO

Responder:

### Tomada de decisão
- Quais ativos parecem apresentar melhores oportunidades?
- Os dados ajudam o investidor a decidir entre compra, venda ou manter?
- Quais indicadores parecem mais úteis para apoiar a decisão?

### Rentabilidade
- Os investidores estão performando melhor ou pior que o Ibovespa?
- Quais perfis de risco apresentam melhor resultado?
- A baixa rentabilidade parece estar associada a algum padrão?

### Recomendação de investimentos
- As recomendações da IA parecem coerentes com os indicadores?
- Existem ativos recomendados com alta volatilidade?
- Que cuidados deveriam ser tomados antes de recomendar um investimento?

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
