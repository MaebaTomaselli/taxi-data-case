# ifood-data-case
Desafio técnico de análise e engenharia de dados - iFood (NYC Taxi)
</br>
## 📌 Visão Geral
Este projeto processa dados de táxis & Limusine de Nova York, transformando dados brutos em insights através de um pipeline com três camadas: Bronze (raw), Silver (processada) e Gold (refinada). A parte final é a análise dos dados refinados.</br>
Utilização de Databricks e Delta Lake.</br>
</br>
## 🎯 Objetivo
Transformar dados brutos em informações analíticas prontas para consumo, seguindo o padrão Medallion Architecture (Bronze → Silver → Gold).
</br>
## 📂 Estrutura do Projeto

Databricks Runtime: 10.4 LTS ou superior

1. Notebooks Principais

![image](https://github.com/user-attachments/assets/d4211bee-973d-4840-9589-c7a6396d640f)

2. Estrutura de Pastas no DBFS
Estrutura do Projeto
<img width="426" alt="image" src="https://github.com/user-attachments/assets/ac10b6f7-0f48-4766-99cf-393bc9f0ef16" />
</br>

## 🧱 Arquitetura de Dados (Medallion Architecture)</br>
A solução foi estruturada seguindo a arquitetura em camadas com o objetivo de garantir escalabilidade, governança e qualidade dos dados ao longo do pipeline.</br>

🥉 Bronze</br>
Representa a ingestão inicial dos dados do site para o Databricks, preservando todas as colunas originais.
Os dados são armazenados em formato Delta Lake, particionados por ano e mês.
Serve como base bruta confiável para processamento posterior, sem alterações de schema ou filtros.

🥈 Silver</br>
Realiza o tratamento e limpeza dos dados, mantendo todas as colunas relevantes e adicionando colunas que identificam o arquivo, veículo e ano/mês.
Os dados continuam em Delta Lake, com estrutura e qualidade aptas para análise e uso corporativo.

🥇 Gold</br>
Dados prontos para consumo analítico, com foco nas necessidades de negócio.
Filtra e mantém apenas as colunas necessárias para as análises solicitadas (ex: VendorID, passenger_count, total_amount, tpep_pickup_datetime, tpep_dropoff_datetime).
Padronização e união das bases de dados.
Ideal para visualizações, dashboards e consultas otimizadas via SQL.


</br>

##  Instruções de Execução

### Opção 1: Execução Manual (Notebook por Notebook)
##### 1. Configure os widgets em cada notebook:
Exemplo (em 01_bronze_dataExtract) </br>
dbutils.widgets.text("start_date", "2023-01", "Data de início (YYYY-MM)") </br>
dbutils.widgets.text("end_date", "2023-01", "Data final (YYYY-MM)") </br>

##### 2. Execute em ordem:
01_bronze_dataExtract → 02_silver_dataProcessing → 03_gold_dataAnalysis. </br>
Observação: O notebook Silver deve ser executado duas vezes (uma para yellow e outra para green). </br>

### Opção 2: Databricks Workflows (Recomendado)
</br>

## 📊 Saída Esperada
Bronze: Dados brutos em dbfs:/case_ifood_nyc/bronze. </br>
Silver: Dados limpos em dbfs:/case_ifood_nyc/silver. </br>
Gold: Tabelas analíticas em dbfs:/case_ifood_nyc/gold. </br>
</br>

## 📈 Análises
### Análise 1: Média do Valor Total (Yellow Taxis)
<img width="286" alt="image" src="https://github.com/user-attachments/assets/c4f2f2f5-6e5e-46f0-98f6-4e4107d98ae0" />

### Análise 2: Média de Passageiros por Hora (Todos os Táxis - Maio)
![image](https://github.com/user-attachments/assets/8ee52ef5-cb33-4bb1-96f0-403c6ebbfc41)

#### Exra 1 - Gráfico de passageiro por hora
![image](https://github.com/user-attachments/assets/0883c86b-56a1-4fa0-b721-805a18109088)

#### Exra 2 - Cálculo do Tempo Médio de Duração da Corrida
![image](https://github.com/user-attachments/assets/4bb5c181-2453-4a51-91d3-d636d11f6818)

</br>

## 📌 Próximos Passos
- Criar dashboard no Power BI com os dados da camada Analysis
- Montar um histórico completo dos dados;
- Montar um script que baixe somente os arquivos novos/alterados e adicione aos dados consolidados.
- Ambiente produtivo: tirar os prints
