# ATIVIDADE — PIPELINE DE DADOS (Delegacia Digital)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de segurança pública em informações úteis para análise de:
- demora no atendimento presencial e registro de B.O.
- lentidão na resolução de inquéritos e investigações
- subnotificação de crimes
- eficiência dos canais digitais de atendimento

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
- Os outliers parecem erros de cadastro ou situações reais de atendimento?
- Quais são os principais problemas de qualidade?

---

### 4. Carregar dados brutos no PostgreSQL

- Criar tabela `delegacia_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `delegacia_ocorrencias_limpo`

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
- Converter campos numéricos:
  - tempo_espera_min
  - tempo_preenchimento_bo_min
  - atendentes_disponiveis
  - tempo_resolucao_dias
  - avaliacao_atendimento
  - chamados_190
  - bo_registrados

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar tipo de ocorrência:
  - fraude on-line → fraude_online
  - perda_doc → perda_documento
  - roubo celular → roubo_celular
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - tempo_espera_min
  - tempo_preenchimento_bo_min
  - tempo_resolucao_dias
  - chamados_190
  - bo_registrados
  - avaliacao_atendimento
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar taxa_abandono_bo_online
- Criar diferenca_chamados_bo
- Criar classificações:
  - demora_atendimento
  - lentidao_inquerito
  - indicio_subnotificacao

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Tempo de espera por canal de atendimento

Mostrar:

```canal de registro, tempo médio de espera, quantidade de ocorrências```


### Atividade 2 — Horários e turnos com maior movimento

Mostrar:

```turno, quantidade de ocorrências, tempo médio de espera, atendentes médios disponíveis```


### Atividade 3 — Tipos de ocorrência mais registrados

Mostrar:

```tipo de ocorrência, quantidade de registros, tempo médio de preenchimento do B.O.```


### Atividade 4 — Lentidão na resolução de inquéritos

Mostrar:

```status do inquérito, tempo médio de resolução, quantidade de ocorrências```


### Atividade 5 — Subnotificação por cidade

Mostrar:

```cidade, UF, chamados 190, B.O. registrados, diferença entre chamados e registros```


### Atividade 6 — Avaliação do atendimento

Mostrar:

```canal de registro, avaliação média, tempo médio de espera, taxa de abandono```

---

## INTERPRETAÇÃO

Responder:

### Atendimento
- Quais canais apresentam maior tempo de espera?
- Existem turnos com sobrecarga de atendimento?
- A quantidade de atendentes parece suficiente?

### Inquéritos
- Quais tipos de ocorrência têm maior tempo de resolução?
- Existem muitos casos abertos ou em andamento?
- Que ações poderiam reduzir a lentidão dos processos?

### Subnotificação
- Quais cidades apresentam maior diferença entre chamados 190 e B.O. registrados?
- O abandono do formulário online pode indicar dificuldade de uso?
- Que medidas poderiam aumentar o registro digital de ocorrências?

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
