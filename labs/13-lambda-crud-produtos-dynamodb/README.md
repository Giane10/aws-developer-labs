# Laboratório 13 - Aplicação Web Serverless CRUD com DynamoDB e Python

## 📋 Descrição do Projeto
Este repositório contém os artefatos e a documentação do **Laboratório 13** da trilha AWS Developer na Escola da Nuvem. O objetivo prático foi construir uma aplicação web full-stack **100% Serverless** para gerenciamento e cadastro de produtos.

A solução utiliza uma interface estática (Frontend) hospedada de forma segura e econômica no **Amazon S3**, que realiza chamadas HTTP assíncronas para um endpoint do **Amazon API Gateway**. A API encaminha as requisições para uma função **AWS Lambda** desenvolvida em **Python 3.12**, responsável por executar as operações de **CRUD** (Create, Read, Update, Delete) diretamente em uma tabela NoSQL do **Amazon DynamoDB**. Toda a camada de monitoramento e auditoria de acessos foi centralizada no **Amazon CloudWatch Logs**.

---


## 🏗️ Arquitetura da Solução

![Arquitetura do Sistema CRUD Serverless](arqui13.png)

* **Camada de Apresentação (Frontend):** Interface web (HTML5, CSS3, JavaScript) hospedada em um Bucket do Amazon S3 configurado para Static Website Hosting.

* **Camada de Apresentação (Frontend):** Interface web (HTML5, CSS3, JavaScript) hospedada em um Bucket do Amazon S3 configurado para Static Website Hosting.
* **Camada de Roteamento (API Management):** Amazon API Gateway (HTTP API) configurado com regras de CORS e integração direta com a Lambda.
* **Camada de Processamento (Backend):** AWS Lambda executando Python 3.12 com o SDK `boto3` para orquestração da lógica de negócio.
* **Camada de Persistência (Banco de Dados):** Amazon DynamoDB atuando como banco NoSQL chave-valor de alta performance.
* **Camada de Observabilidade:** Grupos de Logs customizados no Amazon CloudWatch para rastreamento de acessos da API e execuções da Lambda.

---

## 🛠️ Rotas da API e Operações CRUD

A API foi estruturada utilizando rotas HTTP específicas integradas à mesma função Lambda controladora:

| Método HTTP | Caminho do Recurso | Operação CRUD | Descrição |
| :--- | :--- | :--- | :--- |
| **POST** | `/produtos` | **Create** | Cadastra um novo produto no DynamoDB |
| **GET** | `/produtos` | **Read (List)** | Lista todos os produtos armazenados |
| **GET** | `/produtos/{id}` | **Read (Detail)**| Obtém detalhes de um produto específico |
| **PUT** | `/produtos/{id}` | **Update** | Atualiza os dados de um produto existente |
| **DELETE**| `/produtos/{id}` | **Delete** | Remove um produto do banco de dados |

---

## 📜 Código do Backend (AWS Lambda - Python 3.12)

A função Lambda foi configurada com o manipulador ajustado para `CRUD.lambda_handler`, contando com **256 MB de memória** e **10 segundos de Timeout** para garantir resiliência.

<details>
<summary><b>💻 Ver código-fonte do Backend (CRUD.py)</b></summary>

```python
import json
import boto3
from boto3.dynamodb.conditions import Key

# Inicializa o recurso do DynamoDB
dynamodb = boto3.resource('dynamodb')
# MUDAR: Insira o nome exato da sua tabela abaixo
table = dynamodb.Table('Produtos-gianecosta')

def lambda_handler(event, context):
    print("Evento recebido: ", json.dumps(event))
    
    # Identifica a rota e o método HTTP
    route_key = event.get('routeKey', '')
    http_method = event.get('requestContext', {}).get('http', {}).get('method', '')
    path_parameters = event.get('pathParameters', {}) or {}
    
    headers = {
        "Content-Type": "application/json",
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "GET,POST,PUT,DELETE,OPTIONS",
        "Access-Control-Allow-Headers": "Content-Type"
    }
    
    try:
        # 1. CREATE: Cadastrar Produto
        if http_method == 'POST' and '/produtos' in route_key:
            body = json.loads(event.get('body', '{}'))
            table.put_item(Item={
                'id': body['id'],
                'nome': body['nome'],
                'preco': str(body['preco']),
                'quantidade': int(body['quantidade'])
            })
            return {"statusCode": 201, "headers": headers, "body": json.dumps("Produto cadastrado com sucesso!")}
            
        # 2. READ: Listar Todos os Produtos
        elif http_method == 'GET' and route_key == 'GET /produtos':
            response = table.scan()
            return {"statusCode": 200, "headers": headers, "body": json.dumps(response.get('Items', []))}
            
        # 3. READ: Obter Produto por ID
        elif http_method == 'GET' and '/produtos/{id}' in route_key:
            prod_id = path_parameters.get('id')
            response = table.get_item(Key={'id': prod_id})
            if 'Item' in response:
                return {"statusCode": 200, "headers": headers, "body": json.dumps(response['Item'])}
            return {"statusCode": 404, "headers": headers, "body": json.dumps("Produto não encontrado.")}
            
        # 4. UPDATE: Atualizar Produto
        elif http_method == 'PUT' and '/produtos/{id}' in route_key:
            prod_id = path_parameters.get('id')
            body = json.loads(event.get('body', '{}'))
            table.update_item(
                Key={'id': prod_id},
                UpdateExpression="set nome = :n, preco = :p, quantidade = :q",
                ExpressionAttributeValues={
                    ':n': body['nome'],
                    ':p': str(body['preco']),
                    ':q': int(body['quantidade'])
                }
            )
            return {"statusCode": 200, "headers": headers, "body": json.dumps("Produto atualizado com sucesso!")}
            
        # 5. DELETE: Remover Produto
        elif http_method == 'DELETE' and '/produtos/{id}' in route_key:
            prod_id = path_parameters.get('id')
            table.delete_item(Key={'id': prod_id})
            return {"statusCode": 200, "headers": headers, "body": json.dumps("Produto removido com sucesso!")}
            
        else:
            return {"statusCode": 400, "headers": headers, "body": json.dumps("Rota não suportada.")}
            
    except Exception as e:
        print("Erro: ", str(e))
        return {"statusCode": 500, "headers": headers, "body": json.dumps(f"Erro interno: {str(e)}")}
```
</details>

## 🧪 Dados para Teste de Carga Inicial

Utilize os dados abaixo na interface web para validar o comportamento do CRUD e popular a tabela do DynamoDB:

| ID do Produto | Nome do Produto | Preço (Number/Float) | Quantidade (Int) |
| :---: | :--- | :---: | :---: |
| **1** | Bolsa | `12.50` | 100 |
| **2** | Camiseta | `29.90` | 50 |
| **3** | Tênis | `189.90` | 20 |
| **4** | Relógio | `350.00` | 10 |

---

## 📸 Evidências de Implantação e Testes

Abaixo estão listadas as validações visuais de cada camada da infraestrutura serverless implantada:

### 0. Arquitetura do Projeto
Diagrama estrutural do fluxo de dados da aplicação.
![Arquitetura](img/00-arquitetura.png)

### 1. Frontend em Execução (Amazon S3)
Interface web hospedada estaticamente, realizando operações de listagem e cadastro de produtos com sucesso.
![Site Funcionando](img/01-site-funcionando.png)

### 2. Configurações de Segurança (CORS)
Restrições de compartilhamento de recursos configuradas no API Gateway para permitir requisições seguras vindas do S3.
![Configuração de CORS](img/02-api-gateway-cors.png)

### 3. Logs de Acesso da API (Amazon CloudWatch)
Inspeção de requisições web em tempo real através do CloudWatch Logs, evidenciando chamadas bem-sucedidas (HTTP 200).
![Logs do API Gateway](img/03-cloudwatch-api-logs.png)

### 4. Ciclo de Vida da Função Serverless (AWS Lambda)
Métricas de execução interna da função Lambda, detalhando tempo de computação e bilhetagem por invocação.
![Logs da Lambda](img/04-cloudwatch-lambda-logs.png)

---