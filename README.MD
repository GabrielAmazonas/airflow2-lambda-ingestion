Running Airflow in Docker
This quick-start guide will allow you to quickly start Airflow with CeleryExecutor in Docker. This is the fastest way to start Airflow.

## Executando Airflow no Docker
##### https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html

Este guia rápido permite qeu você inicie rapidamente a utilizar o Airflow com o CeleryExecutor no Docker. Esta é a maneira mais rápida de começar a explorar o Airflow e suas funcionalidades.

### Antes de iniciar:
Follow these steps to install the necessary tools.
Siga estes passos e instale as ferarmentas necessárias:

- Instale o Docker Community Edition (CE) na sua máquina.
- Instale o Docker Compose v1.27.0 ou superior em sua máquina.

Obs.: As versões mais recentes do Docker CE já acompanham a instalação do Docker Compose.


docker-compose.yaml
Utilize o docker-compose.yaml deste repositório. 

Referência original da documentação do airflow: https://airflow.apache.org/docs/apache-airflow/stable/docker-compose.yaml


airflow-scheduler - Este componente monitora todas as tasks e Dags, e dispara a execução das instâncias de tarefas assim que suas tarefas dependentes forem concluídas.

airflow-webserver - O serviço web localizado em http://localhost:8080.

airflow-worker - O worker que executa o trabalho agendado pelo scheduler

airflow-init - Serviço de inicialização

flower - Aplicação flower que monitora o ambiente. Disponível em http://localhost:8080.

postgres - O banco de dados.

redis - Utilizado como broker para as mensagems encaminhadas do scheduler para o worker.

Todos estes serviços te permitem executar o Airflow com o CeleryExecutor. Para mais informações, consulte: https://airflow.apache.org/docs/apache-airflow/stable/concepts.html#architecture


Alguns diretórios dos containers são mounted (montados), o que significa que o conteúdo deles é sincronizado entre seu computador e os containeres.

./dags - Coloque seus arquivos de Dags aqui.

./logs - Contém logs das execuções de tarefas e do scheduler. contains logs from task execution and scheduler.

./plugins - Coloque aqui seus plugins customizados.

Inicializando o Ambiente
Antes de iniciar o Airflow pela primeira vez, você precisa preparar seu ambiente. Criar os arquivos necessáriso e inicializar o banco de dados.

Estes arquivos já foram criados para você neste repositório.

Em todos os sistemas operacionais, você precisa executar as database migrations e criar a primeira conta de usuário.
Para isso, utilize o comando

docker-compose up airflow-init

Após a conclusão da inicialização, você deverá visualizar uma mensagem similar a mensagem abaixo:

airflow-init_1       | Upgrades done
airflow-init_1       | Admin user airflow created
airflow-init_1       | 2.0.1
start_airflow-init_1 exited with code 0
The account created has the login airflow and the password airflow.

Executando o Airflow
Agora você pode iniciar todos os serviços com o comando:

docker-compose up

Em outro terminal, você pode checar o estado dos contâneires e certificar de que eles estão rodando sem problemas

docker ps