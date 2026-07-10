# 🕵️‍♂️ Datacrypt

> Plataforma de Inteligência Investigativa, Due Diligence e Auditoria de Dados Públicos.

O **Datacrypt** é um motor de inteligência investigativa desenvolvido para ir além de um simples painel de monitoramento. A plataforma automatiza processos de auditoria de contratos públicos, cruza beneficiários de programas governamentais e identifica padrões, inconsistências e anomalias financeiras por meio de pipelines de dados de alta performance.

---

# 🏗️ Arquitetura

O projeto adota uma arquitetura **Lakehouse**, combinando a flexibilidade de um Data Lake com a performance analítica de um Data Warehouse.

A plataforma segue rigorosamente o princípio de **Separation of Concerns (SoC)**, separando responsabilidades entre:

- **Produtores de dados** (extração e ingestão)
- **Camada de armazenamento** (Data Lake e Data Warehouse)
- **Aplicações consumidoras** (Dashboards e análises)

Essa arquitetura permite escalabilidade, resiliência e facilidade de manutenção.

---

# 🚀 Stack Tecnológica

| Camada | Tecnologia | Finalidade |
|---------|------------|------------|
| Extração e Processamento | **Python + Polars** | Processamento em lote e micro-batching com alta performance utilizando o motor em Rust. |
| Armazenamento Frio | **Apache Parquet + ZSTD** | Data Lake colunar particionado com compressão de alta eficiência. |
| Armazenamento Quente | **PostgreSQL** | Data Warehouse relacional para consultas rápidas e integrações. |
| Visualização | **Streamlit** | Interface web para dashboards de auditoria e inteligência de mercado. |

---

# 🔍 Fontes de Dados

## Portal da Transparência

Coleta contínua de dados transacionais, incluindo programas como o **Novo Bolsa Família**.

A ingestão é realizada através de **micro-batching**, utilizando aproximadamente **10 requisições a cada 1,5 minuto**, reduzindo o risco de bloqueios nas APIs governamentais e garantindo estabilidade operacional.

## IBGE — API SIDRA

Integração com a **Tabela 9514 (Censo Demográfico 2022)** para obtenção de indicadores populacionais utilizados em cruzamentos estatísticos.

Esses dados permitem identificar métricas como:

- Taxa de Penetração Improvável
- Indicadores demográficos municipais
- Relações entre população e benefícios públicos

---

# ⚙️ Diferenciais de Engenharia

## 🗂️ Arquitetura ELT

O pipeline mantém separadas as diferentes etapas do ciclo de vida dos dados:

- Dados brutos (Raw/Bronze)
- Dados processados (Silver)
- Dados prontos para consumo (Gold)

Essa separação simplifica reprocessamentos, auditorias e recuperação de falhas.

---

## ⚡ Processamento de Alta Performance

O projeto utiliza **Polars** para processamento de grandes volumes de dados, explorando recursos como:

- Execução baseada em Rust
- Baixo consumo de memória
- Processamento vetorizado
- Conversão direta para tuplas utilizando `.rows()`, reduzindo overhead de serialização.

---

## 💾 Data Lake Otimizado

Os dados são armazenados em arquivos **Apache Parquet**, utilizando compressão **ZSTD**, proporcionando:

- Alto desempenho de leitura
- Redução significativa de espaço em disco
- Particionamento nativo
- Compatibilidade com ferramentas analíticas modernas

---

## 🚀 Bulk Loading para PostgreSQL

Após o processamento, os dados são convertidos para Parquet e carregados no Data Warehouse utilizando **bulk inserts** com `execute_values`.

Essa abordagem elimina gargalos causados por inserções linha a linha e acelera significativamente o processo de carga.

---

# 🎯 Objetivos

O Datacrypt foi projetado para fornecer uma base sólida para:

- Auditoria de gastos públicos
- Due Diligence corporativa
- Inteligência investigativa
- Detecção de inconsistências financeiras
- Cruzamento de grandes bases de dados governamentais
- Geração de indicadores analíticos para tomada de decisão
