# ifood-data-case
Desafio técnico de análise e engenharia de dados - iFood (NYC Taxi)

Este projeto processa dados de táxis & Limusine de Nova York, transformando dados brutos em insights através de um pipeline com três camadas: Bronze (raw), Silver (processada) e Gold (refinada). A parte final é a análise dos dados refinados.

Pré-requisitos
Databricks Runtime: 10.4 LTS ou superior

Bibliotecas:

PySpark 3.2.1

Delta Lake 1.1.0

Estrutura do Projeto
/case_ifood_nyc/
├── bronze/          # Dados brutos
├── silver/          # Dados processados
├── gold/            # Dados analíticos
/notebooks/
├── 1_Bronze_Ingest  # Notebook de ingestão
├── 2_Silver_Process # Notebook de processamento
├── 3_Gold_Refined  # Notebook refinado

Instruções de Execução
1. Configuração Inicial
# Configurar widgets para todos os notebooks
dbutils.widgets.dropdown("vehicle_type", "yellow", ["yellow", "green"])
dbutils.widgets.text("start_date", "2023-01", "Data Início (YYYY-MM)")
dbutils.widgets.text("end_date", "2023-01", "Data Fim (YYYY-MM)")

2. Execução do Pipeline
Notebook 1: Bronze (Ingestão)
# Executar célula de configuração
# Definir caminho de entrada/saída
input_path = "/mnt/raw_data/nyc_taxi/"
bronze_path = "/case_ifood_nyc/bronze/nyc_taxi"

# Executar ingestão para cada tipo de veículo
for vehicle in ["yellow", "green"]:
    process_vehicle(vehicle, start_date, end_date)

Notebook 2: Silver (Processamento)
