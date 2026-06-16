
# AWS Developer - Laboratórios Práticos ☁️🚀

Bem-vindo(a) ao meu repositório de laboratórios práticos da trilha AWS Developer, realizados em parceria com a Escola da Nuvem sob a orientação do professor Rafael Silva Willians.

O objetivo deste repositório é consolidar o meu aprendizado em computação em nuvem, documentando a implementação de arquiteturas, automação de infraestrutura, práticas de DevOps, modelagem de dados e governança financeira (FinOps) no ambiente Amazon Web Services.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

| Categoria | Ferramentas |
| :--- | :--- |
| **☁️ Cloud & Serverless** | AWS, AWS Lambda (Python) |
| **🗄️ Dados & Armazenamento** | Amazon DynamoDB (NoSQL), Amazon S3 |
| **🌐 Redes & Integração** | Amazon API Gateway, Amazon SNS, Amazon SQS |
| **🛡️ Segurança & FinOps** | IAM, Security Groups, Políticas de S3, AWS Budgets |
| **⚙️ Infraestrutura** | AWS CLI, CloudShell, User Data Scripts |
| **💻 Versionamento** | Git, GitHub, Markdown |

---

## 📂 Índice de Laboratórios
Abaixo está a lista dos projetos e laboratórios desenvolvidos ao longo do programa. Cada link leva diretamente para a pasta contendo a documentação detalhada:

🔹 **[Lab 01: Amazon EC2](./labs/01-amazon-ec2)** — Automação de instâncias e servidores web Apache.

🔹 **[Lab 02: AWS Budgets](./labs/02-aws-budgets)** — Governança financeira e alertas proativos com SNS.

🔹 **[Lab 03: Automação Serverless](./labs/03-automated-ec2-cleanup)** — Automatizando o fim de instâncias EC2 com Lambda em Python e EventBridge.

🔹 **[Lab 04: Amazon SNS e SQS](./labs/04-sns-sqs-dlq)** — Arquitetura desacoplada e mensageria assíncrona utilizando o padrão Fanout e Dead-Letter Queues (DLQ) para tolerância a falhas.

🔹 **[Lab 05: AWS Lambda (Aliases) e API Gateway (Stages)](./labs/05-lambda-api-gateway)** — Gerenciamento de múltiplos ambientes (Desenvolvimento e Produção) com roteamento inteligente de tráfego e controle de versão em arquiteturas serverless.

🔹 **[Lab 06: Aplicação Web Serverless](./labs/06-jogo-adivinhacao-aws-serverless)** — Integração ponta a ponta de um jogo de adivinhação web utilizando frontend estático no Amazon S3 acoplado a um backend dinâmico com API Gateway e AWS Lambda.

🔹 **[Lab 07: Amazon DynamoDB](./labs/07-amazon-dynamodb)** — Modelagem NoSQL com Índices Secundários Locais (LSI) e Globais (GSI), manipulação de arquivos JSON e carga em lote.

🔹 **[Lab 08: AWS SSM Parameter Store e KMS](./labs/08-ssm-parameter-store-kms)** — Gerenciamento centralizado de variáveis de ambiente e segredos, utilizando chaves customizadas para criptografia em repouso e consumo via CLI.

---

## 🧠 Aprendizados Consolidados
Competências aprimoradas para atuação na Engenharia de Nuvem, organizadas nos seguintes pilares:

⚙️ **Arquitetura & Computação**
* **Ciclo de Vida Serverless:** Isolamento lógico de ambientes (Dev/Prod) utilizando *Stages* e *Aliases*, sem duplicar recursos físicos.
* **Sistemas Desacoplados:** Aplicação de padrões de integração assíncrona (como *Fanout*) para alta resiliência.

🌐 **Integração Web & Dados**
* **Aplicações Modernas:** Hospedagem estática no S3 e configuração de políticas de CORS no API Gateway.
* **Modelagem NoSQL:** Criação de tabelas com LSI e GSI no DynamoDB para otimizar desempenho e reduzir custos (RCUs).

🛡️ **Segurança, Automação & FinOps**
* **Infraestrutura Automatizada:** Uso de comandos replicáveis via AWS CLI em substituição a processos manuais.
* **Segurança em Camadas:** Restrição estrita de acessos através de *Bucket Policies* e *Security Groups*.
* **Gerenciamento de Segredos (DevSecOps):** Centralização de credenciais sensíveis via SSM Parameter Store e criptografia em repouso controlada por chaves do AWS KMS sob o princípio do privilégio mínimo.
* **Governança de Custos:** Monitoramento proativo para uma nuvem financeiramente sustentável e eficiente.

---

## 👩‍💻 Conecte-se Comigo
Se você quiser acompanhar a minha transição de carreira para o setor de tecnologia ou trocar ideias sobre o ecossistema AWS:
* **LinkedIn:** [giane-costa](https://www.linkedin.com/in/giane-costa/)
* **GitHub:** [Giane10](https://github.com/Giane10)

