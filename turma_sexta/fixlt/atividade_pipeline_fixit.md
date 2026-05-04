# ATIVIDADE — PIPELINE DE DADOS (FixIt)

## OBJETIVO

O grupo deve desenvolver um pipeline de dados (ETL) completo utilizando Apache NiFi, PostgreSQL e Hue.

O objetivo é transformar dados de chamados e serviços residenciais em informações úteis para análise de:
- ineficiência no deslocamento dos profissionais
- incompatibilidade entre profissional e tarefa
- baixa recorrência de uso
- satisfação e retrabalho nos serviços

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

- Criar tabela `fixit_raw`
- Todos os campos devem ser TEXT
- Inserir dados sem tratamento

---

### 5. Limpeza via SQL

Criar tabela `fixit_chamados_limpo`

Tratar:

#### Datas
- Padronizar formatos
- Converter para DATE
- Remover inválidos

#### Números
- Converter vírgula para ponto
- Tratar NA, vazio e null
- Converter campos numéricos:
  - distancia_km
  - tempo_deslocamento_min
  - tempo_execucao_min
  - tempo_total_min
  - valor_orcamento
  - valor_pago
  - avaliacao_cliente
  - dias_desde_ultimo_uso
  - idade_imovel_anos

#### Textos
- Corrigir erros de digitação
- Padronizar UF (mg → MG, sp → SP)
- Padronizar tipo de serviço:
  - eletric. → eletrica
  - hidraulicaa → hidraulica
  - montagem_moveis → montagem
- Padronizar especialidade:
  - eletrica_geral → eletricista
  - encanador geral → encanador
- Padronizar status:
  - procesado → processado

#### Duplicatas
- Remover por `registro_id`

#### Outliers
- Identificar valores muito fora do padrão em:
  - tempo_deslocamento_min
  - distancia_km
  - tempo_execucao_min
  - valor_orcamento
  - valor_pago
  - avaliacao_cliente
  - idade_imovel_anos
- O grupo deve analisar se o outlier é:
  - erro de cadastro
  - caso real extremo
  - dado suspeito que precisa ser separado

#### Campos derivados
- Criar tempo_total_calculado
- Criar flag_atraso_deslocamento
- Criar flag_retrabalho
- Criar flag_baixa_recorrencia
- Criar classificações:
  - compatibilidade_profissional
  - risco_insatisfacao
  - oportunidade_servico_preventivo

---

### 6. Gravar dados limpos no postgress

- Criar a(s) tabela(s)
- Inserir dados tratados na(s) tabela(s) final

---

### 7. Consultar no Postgress

Executar consultas SQL para gerar insights.

---

## ATIVIDADES SQL

### Atividade 1 — Tempo de deslocamento por bairro

Mostrar:

```bairro, quantidade de chamados, distância média, tempo médio de deslocamento```


### Atividade 2 — Eficiência por tipo de serviço

Mostrar:

```tipo de serviço, tempo médio de execução, valor médio pago, avaliação média```


### Atividade 3 — Compatibilidade profissional x tarefa

Mostrar:

```tipo de serviço, especialidade profissional, quantidade de chamados, taxa de retrabalho```


### Atividade 4 — Reclamações e retorno para correção

Mostrar:

```tipo de serviço, quantidade de reclamações, quantidade de retornos, avaliação média```


### Atividade 5 — Baixa recorrência de uso

Mostrar:

```cliente, dias desde último uso, quantidade de chamados, uso de cupom```


### Atividade 6 — Oportunidades de serviços preventivos

Mostrar:

```idade do imóvel, tipo de serviço, quantidade de chamados, valor médio pago```

---

## INTERPRETAÇÃO

Responder:

### Deslocamento
- Quais bairros apresentam maior tempo de deslocamento?
- A distância explica os atrasos?
- Que ações poderiam reduzir o tempo entre chamados?

### Compatibilidade
- Existem profissionais atendendo serviços fora da especialidade?
- Isso aumenta reclamações ou retrabalho?
- Como a plataforma poderia melhorar o direcionamento dos chamados?

### Recorrência
- Os clientes usam o app apenas em emergências?
- Quais sinais indicam baixa recorrência?
- Que serviços preventivos poderiam ser recomendados?

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
