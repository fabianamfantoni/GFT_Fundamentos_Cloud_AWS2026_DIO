# Executando Tarefas Automatizadas com Lambda Function e S3

*Este projeto demonstra como automatizar tarefas utilizando AWS Lambda em conjunto com Amazon S3 e DynamoDB, simulando um ambiente de nuvem local com Docker e LocalStack.*

## Objetivo

- Inserir registros em uma tabela DynamoDB.

- Consultar registros via API Gateway.

- Processar arquivos enviados para um bucket S3.

- Testar e validar toda a solução em ambiente local, sem custos de AWS reais.

---

## Ferramentas Utilizadas
---
- Docker

    - Responsável por criar containers isolados para execução dos serviços.

    - Função principal: fornecer o ambiente necessário para rodar o LocalStack e simular os serviços da AWS.
---
- LocalStack

    - Usado para simular serviços da AWS localmente.

    - Permite testar Lambda Functions, DynamoDB, S3 e API Gateway sem precisar acessar a nuvem real.
---
**Comando básicos de inicialização:**

```
docker run -p 4566:4566 -p 4571:4571 localstack/localstack

```
---

- Postman: 

    - Ferramenta utilizada para testar as requisições HTTP (GET/POST) contra o API Gateway.
---

- Python (Boto3)

    -SDK para interagir com os serviços simulados da AWS.

    -Usado dentro da Lambda Function para manipular DynamoDB e S3.

**Esse projeto mostrou como funciona uma arquitetura serverless, auxiliou a aprimorar o uso de ferramentas do dia a dia de um desenvolvedor. Também evidenciou a importância de ter cuidado com as informações e de manter o fluxo correto de execução. Destacou como as permissões adequadas podem, ao mesmo tempo, dificultar a implementação, mas também proteger o trabalho e garantir a segurança da aplicação.**

## outras informações: 

- Como funciona:
    Upload de Arquivo no S3 - Um arquivo é enviado para o bucket configurado, o que dispara a execução da Lambda Function.

    Lambda Function - Valida o conteúdo do arquivo e insere os registros na tabela DynamoDB.

    API Gateway + Lambda Function - Usuários podem consultar registros via endpoint REST. A Lambda consulta o DynamoDB e retorna os dados.
    
---

- Fluxo:
    Iniciar o LocalStack - Simula os serviços da AWS em ambiente local.

    Criar recursos AWS simulados - Configurar bucket S3 e tabela DynamoDB no LocalStack.

    Não esqueça de configurar as permissões básicas.

    Deploy da Lambda Function - Enviar o código Python para execução no LocalStack.
        > Empacote o código em um arquivo ZIP -> Faça upload para o LocalStack -> Configure o handler como "grava_db.lambda_handler".
    
    Testar com Postman -> Validar as requisições GET e POST via API Gateway.

---
 
 ***O uso de Docker e LocalStack garante que o desenvolvimento seja rápido, seguro e sem custos de infraestrutura real.***