# ATIVIDADE — PIPELINE DE DADOS (Distribuidora de Autopeças)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados operacionais em informações úteis para análise de:
- ruptura e excesso de estoque
- inconsistência na precificação e margem
- gargalos logísticos e atrasos

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

- Criar tabela `autopecas_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `autopecas_limpo`

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
  - estoque_atual
  - demanda_mensal
  - custo_aquisicao
  - tempo_entrega_dias
  - margem_lucro

#### Campos derivados
- criar flag_ruptura
- criar flag_excesso_estoque
- criar flag_atraso_logistico
- criar classificacao_margem

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Ruptura de estoque

Mostrar:

```sku, categoria, estoque atual, demanda mensal```


### Atividade 2 — Excesso de estoque

Mostrar:

```sku, estoque atual, demanda, curva abc```


### Atividade 3 — Margem por produto

Mostrar:

```sku, custo, preco, margem```


### Atividade 4 — Impacto dos impostos

Mostrar:

```categoria, imposto medio, margem media```


### Atividade 5 — Atrasos logísticos

Mostrar:

```cidade, tempo medio entrega, quantidade atrasos```


### Atividade 6 — Qualidade logística

Mostrar:

```cidade, devoluções, avarias, entregas```

---

## INTERPRETAÇÃO

Responder:

### Estoque
- Existem rupturas?
- Existe excesso?

### Margem
- Preços estão corretos?
- Impostos impactam?

### Logística
- Onde há atraso?
- O frete impacta?

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
