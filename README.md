Esse projeto foi feito com base no curso da udemy https://www.udemy.com/course/arquitetura-de-microsservicos-padrao-saga-orquestrado/learn/lecture/37378720#content

Arquitetura

Sumário:
Tecnologias
Ferramentas utilizadas
Arquitetura Proposta
Execução do projeto
01 - Execução geral via docker-compose
02 - Execução geral via automação com script em Python
03 - Executando os serviços de bancos de dados e Message Broker
04 - Executando manualmente via CLI
Acessando a aplicação
Acessando tópicos com Redpanda Console
Dados da API
Produtos registrados e seu estoque
Endpoint para iniciar a saga
Endpoint para visualizar a saga
Acesso ao MongoDB
Tecnologias
Voltar ao início

Java 17
Spring Boot 3
Apache Kafka
API REST
PostgreSQL
MongoDB
Docker
docker-compose
Redpanda Console
Ferramentas utilizadas
Voltar ao início

IntelliJ IDEA Community Edition
Docker
Gradle
Arquitetura Proposta
Voltar ao início

No curso, desenvolveremos a seguinte aquitetura:

Arquitetura

Em nossa arquitetura, teremos 5 serviços:

Order-Service: microsserviço responsável apenas por gerar um pedido inicial, e receber uma notificação. Aqui que teremos endpoints REST para inciar o processo e recuperar os dados dos eventos. O banco de dados utilizado será o MongoDB.
Orchestrator-Service: microsserviço responsável por orquestrar todo o fluxo de execução da Saga, ele que saberá qual microsserviço foi executado e em qual estado, e para qual será o próximo microsserviço a ser enviado, este microsserviço também irá salvar o processo dos eventos. Este serviço não possui banco de dados.
Product-Validation-Service: microsserviço responsável por validar se o produto informado no pedido existe e está válido. Este microsserviço guardará a validação de um produto para o ID de um pedido. O banco de dados utilizado será o PostgreSQL.
Payment-Service: microsserviço responsável por realizar um pagamento com base nos valores unitários e quantidades informadas no pedido. Este microsserviço guardará a informação de pagamento de um pedido. O banco de dados utilizado será o PostgreSQL.
Inventory-Service: microsserviço responsável por realizar a baixa do estoque dos produtos de um pedido. Este microsserviço guardará a informação da baixa de um produto para o ID de um pedido. O banco de dados utilizado será o PostgreSQL.
Todos os serviços da arquitetura irão subir através do arquivo docker-compose.yml.

Execução do projeto
Voltar ao início

Há várias maneiras de executar os projetos:

Executando tudo via docker-compose
Executando tudo via script de automação que eu disponibilizei (build.py)
Executando apenas os serviços de bancos de dados e message broker (Kafka) separadamente
Executando as aplicações manualmente via CLI (java -jar ou gradle bootRun ou via IntelliJ)
Para rodar as aplicações, será necessário ter instalado:

Docker
Java 17
Gradle 7.6 ou superior
