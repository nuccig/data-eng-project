# 🏗️ Data Engineering Project

## 📋 Descrição
Pipeline completo de engenharia de dados com ETL automatizado usando Apache Airflow, transformações dbt e modelagem dimensional para análise de vendas de concessionárias.

## 🚀 Tecnologias Utilizadas
- **Apache Airflow** - Orquestração de pipelines
- **dbt (Data Build Tool)** - Transformações de dados
- **PostgreSQL** - Banco de dados origem
- **Snowflake** - Data warehouse destino
- **SQL** - Modelagem e transformações

## 📁 Estrutura do Projeto
```
├── dags/
│   └── dag.py                    # DAG do Airflow para ETL
├── dbt/
│   ├── models/
│   │   ├── source.yml           # Definição das fontes
│   │   ├── stage/               # Camada de staging
│   │   ├── dim/                 # Tabelas dimensão
│   │   ├── fact/                # Tabelas fato
│   │   └── analytics/           # Análises de negócio
│   ├── analyses/                # Análises ad-hoc
│   ├── macros/                  # Macros reutilizáveis
│   ├── seeds/                   # Dados estáticos
│   ├── snapshots/               # Snapshots SCD
│   └── tests/                   # Testes de qualidade
├── aws/                         # Configurações AWS
├── dbt_project.yml             # Configuração do dbt
├── LICENSE
└── README.md
```

## ⚡ Funcionalidades
### Pipeline ETL (Airflow)
- **Extração incremental** do PostgreSQL
- **Carregamento automatizado** no Snowflake
- **Orquestração de tarefas** com dependências
- **Monitoramento e alertas**

### Modelagem de Dados (dbt)
#### Camada Staging
- `stg_vendas`, `stg_clientes`, `stg_veiculos`
- `stg_vendedores`, `stg_concessionarias`
- `stg_cidades`, `stg_estados`

#### Camada Dimensional
- **Dimensões**: `dim_clientes`, `dim_veiculos`, `dim_vendedores`, `dim_concessionarias`, `dim_cidades`, `dim_estados`
- **Fato**: `fct_vendas`

#### Camada Analytics
- `analise_vendas_concessionaria` - Performance por concessionária
- `analise_vendas_temporal` - Tendências temporais
- `analise_vendas_veiculo` - Análise por modelo/marca
- `analise_vendas_vendedor` - Performance de vendedores

## 🔧 Instalação e Execução
### Pré-requisitos
```bash
# Instalar Airflow
pip install apache-airflow

# Instalar dbt
pip install dbt-core dbt-snowflake dbt-postgres
```

### Configuração
```bash
# Configurar conexões do Airflow
airflow connections add postgres_conn --conn-type postgres --conn-host localhost

# Configurar perfis do dbt
dbt init data_eng_project

# Executar transformações
dbt run
dbt test
```

### Execução do Pipeline
```bash
# Iniciar Airflow
airflow standalone

# Executar DAG
airflow dags trigger postgres_to_snowflake
```

## 🛠️ Configuração do Ambiente
### Airflow DAG
- **Schedule**: Diário
- **Retry**: Sem retry
- **Tabelas processadas**: veiculos, estados, cidades, clientes, vendedores, concessionarias, vendas

### dbt Profiles
Configuração para múltiplos ambientes (dev, staging, prod) com Snowflake como target principal.

## 📊 Modelo de Dados
### Arquitetura Medallion
1. **Bronze** (Staging) - Dados brutos limpos
2. **Silver** (Dimensional) - Modelagem star schema
3. **Gold** (Analytics) - Análises agregadas

### Métricas Principais
- Volume de vendas por período
- Performance de vendedores
- Análise geográfica de vendas
- Tendências por tipo de veículo

## 📦 Dependências Principais
- apache-airflow[postgres,snowflake]
- dbt-core
- dbt-snowflake
- dbt-postgres

## 🎯 Casos de Uso
- **Dashboards executivos** com KPIs de vendas
- **Análise de performance** de vendedores e concessionárias
- **Planejamento estratégico** baseado em tendências
- **Otimização de estoque** por região