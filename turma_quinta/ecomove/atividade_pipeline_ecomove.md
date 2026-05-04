# ATIVIDADE — PIPELINE DE DADOS (EcoMove)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de mobilidade urbana em informações úteis para análise de:
- disponibilidade de veículos
- retenção de usuários
- recomendação de transporte
- uso de modais sustentáveis

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
- Os outliers parecem erros ou comportamento real?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `ecomove_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `ecomove_viagens_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Coordenadas
- Converter para número
- Validar se está dentro do Brasil:
  - latitude: -34 a 6
  - longitude: -74 a -34

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null

#### Textos
- Padronizar UF
- Corrigir valores inconsistentes

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores fora do padrão em:
  - tempo_viagem_min
  - distancia_km
  - custo
  - frequencia_uso_mes
  - avaliacao_usuario

#### Campos derivados
- criar flag_pico
- criar flag_baixa_retenção
- criar recomendacao_modal

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Uso por modal

Mostrar:

```modal, quantidade de viagens, custo médio, tempo médio```


### Atividade 2 — Horários de pico

Mostrar:

```hora, quantidade de viagens, tempo médio```


### Atividade 3 — Retenção de usuários

Mostrar:

```usuario, frequência média, tempo desde última viagem```


### Atividade 4 — Influência do clima

Mostrar:

```clima, quantidade de viagens, tempo médio```


### Atividade 5 — Cancelamentos

Mostrar:

```modal, quantidade de cancelamentos, taxa de cancelamento```


### Atividade 6 — Avaliação do serviço

Mostrar:

```modal, avaliação média, custo médio```

---

## INTERPRETAÇÃO

Responder:

### Disponibilidade
- Há falta de veículos?
- Existem horários críticos?

### Retenção
- Usuários voltam a usar?
- Frequência é suficiente?

### Recomendação
- Qual modal é mais eficiente?
- O clima influencia?

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
