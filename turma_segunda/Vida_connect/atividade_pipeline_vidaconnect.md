# ATIVIDADE — PIPELINE DE DADOS (VidaConnect)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de saúde digital em informações úteis para análise de:
- abandono de consultas
- monitoramento de pacientes crônicos
- recomendação de médicos e especialidades

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
- Os outliers parecem erros ou casos reais?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `vidaconnect_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `vidaconnect_consultas_limpo`

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
  - tempo_espera_min
  - glicemia
  - idade
  - checkins_mes
  - avaliacao_medico

#### Campos derivados
- criar flag_falta
- criar flag_risco_cronico
- criar recomendacao_especialidade

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Taxa de comparecimento

Mostrar:

```tipo de consulta, quantidade, taxa de comparecimento```


### Atividade 2 — Abandono de consultas

Mostrar:

```dia da semana, horário, quantidade de faltas```


### Atividade 3 — Monitoramento de pacientes

Mostrar:

```checkins, glicemia média, pressão média, quantidade de pacientes```


### Atividade 4 — Especialidades mais procuradas

Mostrar:

```especialidade, quantidade de consultas, avaliação média```


### Atividade 5 — Relação espera x avaliação

Mostrar:

```tempo de espera, avaliação média, quantidade```


### Atividade 6 — Perfil dos pacientes

Mostrar:

```idade, tipo de consulta, frequência de checkins, quantidade```

---

## INTERPRETAÇÃO

Responder:

### Consultas
- Existe alta taxa de abandono?
- O tipo de consulta influencia?

### Pacientes crônicos
- Há pacientes em risco?
- Monitoramento é eficiente?

### Recomendação
- Especialidades fazem sentido?
- Dados ajudam decisão?

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
