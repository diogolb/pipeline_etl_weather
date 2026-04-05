<img width="572" height="332" alt="{F1688F3B-9334-454C-88BA-C385ADD19078}" src="https://github.com/user-attachments/assets/241b9d75-bcb6-4e9e-b4b1-6119cf6ee999" />

🚀 Pipeline ETL: Cotação do Dólar (BCB API)
Este projeto automatiza a extração, transformação e carga (ETL) da cotação do dólar comercial diretamente da API do Banco Central do Brasil (BCB) para um banco de dados PostgreSQL, utilizando Airflow como orquestrador e Docker para infraestrutura.

🛠️ Tecnologias e Ferramentas
Linguagem: Python 3.12 (com uv para gestão de pacotes)

Orquestração: Apache Airflow (TaskFlow API)

Containerização: Docker & Docker Compose

Banco de Dados: PostgreSQL

Ambiente de Desenvolvimento: WSL2 (Ubuntu)

Bibliotecas Principais: Pandas, SQLAlchemy, Holidays, Python-dotenv

🏗️ Arquitetura do Projeto
O pipeline foi desenhado seguindo as melhores práticas de modularização:

dags/: Definição do fluxo de trabalho e agendamento.

src/: Scripts core de Extração, Transformação e Carga (Separation of Concerns).

config/: Gestão de variáveis de ambiente e segurança.

data/: Armazenamento temporário de arquivos em formato Parquet.

🔄 O Pipeline (DAG)
O fluxo consiste em três etapas principais:

Extract: Consulta a API do BCB tratando feriados nacionais e finais de semana (através da lib holidays) para garantir que sempre buscaremos o último dia útil.

Transform: Limpeza dos dados, renomeação de colunas e tipagem, salvando o resultado em um arquivo .parquet para otimização de I/O.

Load: Ingestão dos dados no PostgreSQL via SQLAlchemy.

🧠 Desafios Técnicos & Aprendizados
Este projeto foi um divisor de águas no meu entendimento de infraestrutura:

Networking no Docker: Configurei a comunicação entre o container do Airflow e o PostgreSQL rodando no host (WSL2), utilizando IPs de rede virtual e ajustes no pg_hba.conf.

Resiliência: Implementei lógica de retentativas (retries) e tratamento de erros de conexão com o banco de dados.

Segurança: Toda a configuração sensível (senhas, hosts) é gerida via variáveis de ambiente (.env), nunca expostas no código.
