# ATIVIDADE — PIPELINE DE DADOS (LiftOn Gym)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de academia em informações úteis para análise de:
- evasão de alunos
- horários de pico
- uso de equipamentos

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

- Criar tabela `lifton_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `lifton_alunos_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter para número
- Tratar NA, vazio e null

#### Textos
- Corrigir erros (procesado)
- Padronizar valores

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores fora do padrão em:
  - frequencia_semanal
  - tempo_treino_min
  - uso_equipamento_min
  - idade
  - tempo_permanencia_meses

#### Campos derivados
- criar flag_evasao
- criar flag_pico
- criar classificacao_uso_equipamento

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Evasão de alunos

Mostrar:

```plano, quantidade de alunos, taxa de cancelamento```


### Atividade 2 — Tempo médio de permanência

Mostrar:

```plano, tempo médio de permanência, frequência média```


### Atividade 3 — Horários de pico

Mostrar:

```horario_entrada, quantidade de alunos, média de tempo de treino```


### Atividade 4 — Uso de equipamentos

Mostrar:

```equipamento, frequência de uso, tempo médio de uso```


### Atividade 5 — Relação frequência x evasão

Mostrar:

```frequencia_semanal, quantidade de alunos, taxa de evasão```


### Atividade 6 — Perfil dos alunos

Mostrar:

```idade, plano, frequência média, tempo médio de permanência```

---

## INTERPRETAÇÃO

Responder:

### Evasão
- Quais alunos cancelam mais?
- Existe relação com frequência?

### Horários
- Quais são os horários de pico?
- Há ociosidade?

### Equipamentos
- Quais são mais usados?
- Existe desbalanceamento?

### Qualidade dos dados
- Outliers impactaram?
- Problemas prejudicam análise?

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
