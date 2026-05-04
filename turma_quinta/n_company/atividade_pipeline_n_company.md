# ATIVIDADE — PIPELINE DE DADOS (N Company)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados comerciais e de comportamento dos clientes em informações úteis para análise de:
- perda de clientes
- perfil dos clientes
- baixa conversão de propostas
- desempenho comercial e de UX/UI

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

- Criar tabela `ncompany_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `ncompany_leads_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos numéricos:
  - idade_cliente
  - renda_cliente
  - valor_proposta
  - taxa_abandono_formulario_pct
  - tempo_decisao_dias
  - score_ux
  - tempo_no_site_seg
  - cliques_formulario

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar status da proposta:
  - aceitaa → aceita
  - recuzada → recusada
  - em analise → em_analise
- Padronizar status do registro:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - valor_proposta
  - taxa_abandono_formulario_pct
  - tempo_decisao_dias
  - score_ux
  - tempo_no_site_seg
  - renda_cliente
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar taxa_conversao
- Criar flag_cliente_perdido
- Criar classificações:
  - perfil_cliente
  - baixa_conversao
  - proposta_abandonada

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Conversão por origem do lead

Mostrar:

```origem do lead, quantidade de propostas enviadas, quantidade de propostas aceitas, taxa de conversão```


### Atividade 2 — Perfil dos clientes

Mostrar:

```perfil do cliente, idade média, renda média, valor médio da proposta```


### Atividade 3 — Perda de clientes por motivo

Mostrar:

```motivo da perda, quantidade de clientes perdidos, valor médio da proposta```


### Atividade 4 — Abandono de proposta

Mostrar:

```status da proposta, taxa média de abandono do formulário, tempo médio no site```


### Atividade 5 — Relação UX x conversão

Mostrar:

```faixa de score UX, quantidade de leads, taxa de conversão```


### Atividade 6 — Tempo de decisão e fechamento

Mostrar:

```faixa de tempo de decisão, quantidade de propostas, taxa de aceitação```

---

## INTERPRETAÇÃO

Responder:

### Perda de clientes
- Quais são os principais motivos de perda?
- Existe relação entre valor da proposta e perda de clientes?
- Quais ações poderiam reduzir a perda?

### Perfil dos clientes
- Qual perfil parece ter maior potencial de fechamento?
- Idade, renda ou porte da empresa ajudam a entender o cliente?
- O grupo consegue identificar um público-alvo prioritário?

### Conversão
- Quais canais geram mais conversão?
- A experiência de UX/UI parece influenciar a aceitação da proposta?
- O tempo de decisão impacta a conversão?

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
