# AWS Developer - Laboratórios Práticos ☁️🚀

Bem-vindo(a) ao meu repositório de laboratórios práticos da trilha AWS Developer, realizados em parceria com a Escola da Nuvem sob a orientação do professor Rafael Silva Willians.

O objetivo deste repositório é consolidar o meu aprendizado em computação em nuvem, documentando a implementação de arquiteturas, automação de infraestrutura, práticas de DevOps, modelagem de dados e governança financeira (FinOps) no ambiente Amazon Web Services.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

| Categoria | Ferramentas |
| :--- | :--- |
| **☁️ Cloud & Serverless** | AWS, AWS Lambda (Python), AWS Elastic Beanstalk |
| **🗄️ Dados & Armazenamento** | Amazon DynamoDB (NoSQL), Amazon S3 |
| **🌐 Redes & Integração** | Amazon API Gateway, Amazon SNS, Amazon SQS |
| **🛡️ Segurança, Auditoria & FinOps** | AWS CloudTrail, AWS STS, IAM (Roles/Policies), Security Groups, Políticas de S3, AWS Budgets |
| **📊 Observabilidade & Alertas** | Amazon CloudWatch (Alarms, Metrics, Health Checks, Logs) |
| **⚙️ Infraestrutura & Testes** | AWS CLI, CloudShell, User Data Scripts, `stress-ng`, Boto3 SDK, AWS CloudFormation |
| **💻 Versionamento** | Git, GitHub, Markdown |

---

## 📂 Índice de Laboratórios
Abaixo está a lista dos projetos e laboratórios desenvolvidos ao longo do programa. Cada link leva diretamente para a pasta contendo a documentação detalhada:

🔹 **[Lab 01: Amazon EC2](./labs/01-amazon-ec2)** — Automação de instâncias e servidores web Apache.

🔹 **[Lab 02: AWS Budgets](./labs/02-aws-budgets)** — Governança financeira e alertas proativos com SNS.

🔹 **[Lab 03: Automação Serverless](./labs/03-automated-ec2-cleanup)** — Automatizando o fim de instâncias EC2 com Lambda em Python e EventBridge.

🔹 **[Lab 04: Amazon SNS e SQS](./labs/04-sns-sqs-dlq)** — Arquitetura desacoplada e mensageria assíncrona utilizando o padrão Fanout e Dead-Letter Queues (DLQ) para tratamento de falhas em filas de mensagens secundárias.

🔹 **[Lab 05: AWS Lambda (Aliases) e API Gateway (Stages)](./labs/05-lambda-api-gateway)** — Gerenciamento de múltiplos ambientes (Desenvolvimento e Produção) com roteamento inteligente de tráfego e controle de versão em arquiteturas serverless.

🔹 **[Lab 06: Aplicação Web Serverless](./labs/06-jogo-adivinhacao-aws-serverless)** — Integration ponta a ponta de um jogo de adivinhação web utilizando frontend estático no Amazon S3 acoplado a um backend dinâmico com API Gateway e AWS Lambda.

🔹 **[Lab 07: Amazon DynamoDB](./labs/07-amazon-dynamodb)** — Modelagem NoSQL com Índices Secundários Locais (LSI) e Globais (GSI), manipulação de arquivos JSON e carga em lote.

🔹 **[Lab 08: AWS SSM Parameter Store e KMS](./labs/08-ssm-parameter-store-kms)** — Gerenciamento centralizado de variáveis de ambiente e segredos, utilizando chaves customizadas para criptografia em repouso e consumo via CLI.

🔹 **[Lab 09: Monitoramento, Alertas e Auditoria](./labs/09-cloudwatch-cloudtrail-monitoring)** — Implementação de observabilidade com alarmes estáticos no Amazon CloudWatch e notificações via Amazon SNS integrados a uma trilha de auditoria contínua via AWS CloudTrail armazenada no Amazon S3.

🔹 **[Lab 10: AWS Security Token Service (STS)](./labs/10-aws-sts-temporary-credentials)** — Provisionamento e gerenciamento de credenciais temporárias efêmeras com Python/Boto3, assunção de papéis (Roles) e validação de políticas de confiança (Trust Relationships) sob o princípio do privilégio mínimo.

🔹 **[Lab 11: AWS Elastic Beanstalk](./labs/11-aws-elastic-beanstalk-deployment)** — Provisionamento, gerenciamento e orquestração automatizada de aplicações web em modelo PaaS, controlando perfis de instância IAM e ciclo de vida de recursos.

🔹 **[Lab 12: Arquitetura Fan-Out com SNS, SQS e Lambda](./labs/12-arquitetura-fanout-sns-sqs-lambda)** — Implementação de um ecossistema orientado a eventos (*Event-Driven*) para processamento de e-commerce, aplicando políticas avançadas de filtragem de assinatura no SNS, buffers de isolamento assíncronos em filas SQS e contenção de falhas com Dead-Letter Queues (DLQ).

🔹 **[Lab 13: Operação CRUD Serverless com DynamoDB e Python](./labs/13-lambda-crud-produtos-dynamodb)** — Construção de uma aplicação web full-stack serverless com frontend estático no Amazon S3 integrado via rotas HTTP estruturadas no Amazon API Gateway a um backend controlador em AWS Lambda (Python), realizando persistência dinâmica em tabelas NoSQL do Amazon DynamoDB.

---

## 🧠 Aprendizados Consolidados
Competências aprimoradas para atuação na Engenharia de Nuvem, organizadas nos seguintes pilares:

⚙️ **Arquitetura & Computação**
* **Ciclo de Vida Serverless:** Isolamento lógico de ambientes (Dev/Prod) utilizando *Stages* e *Aliases*, sem duplicar recursos físicos.
* **Sistemas Orientados a Eventos & Desacoplados:** Aplicação avançada do padrão *Fan-Out* com Amazon SNS e SQS para roteamento de payloads complexos em microsserviços paralelos, minimizando o acoplamento sistêmico e garantindo tolerância a falhas.
* **Resiliência e Contenção:** Configuração de Dead-Letter Queues (DLQ) no SQS para tratamento, isolamento e auditoria de mensagens com falhas consecutivas de processamento.
* **Aplicações Full-Stack Serverless:** Acoplamento completo de arquiteturas desacopladas de microsserviços, distribuindo regras de negócio lógicas e fluxos de dados ponta a ponta sem necessidade de gerenciar servidores subjacentes.
* **Abstração de Infraestrutura (PaaS):** Compreensão de como o AWS Elastic Beanstalk otimiza o tempo de deploy de aplicações (como Node.js), isolando servidores web em ambientes single instance com foco em eficiência operacional.

🌐 **Integração Web & Dados**
* **Aplicações Modernas & Hosting Estático:** Hospedagem estática altamente disponível e de baixo custo no S3 através do *Static Website Hosting*, roteamento assíncrono cliente-servidor e configuração granular de controle de acesso a recursos compartilhados (**CORS**).
* **Modelagem e Persistência NoSQL:** Criação de tabelas com LSI e GSI no DynamoDB para otimizar desempenho e reduzir custos (RCUs), e manipulação programática de operações transacionais complexas de escrita, leitura, atualização e deleção (**CRUD**) via SDK `boto3`.
* **Filtros Cirúrgicos de Mensageria:** Escrita de políticas de filtragem de assinatura (*Subscription Filter Policies*) em JSON para otimização de processamento computacional no SNS, garantindo o direcionamento seletivo de mensagens e gerando economia de custos de invocação da Lambda.

📊 **Observabilidade, Segurança & Auditoria (DevSecOps)**
* **Gerenciamento de Identidades Dinâmico:** Utilização do AWS STS para reduzir superfícies de ataque através do uso de tokens e chaves temporárias programáticas em substituição a credenciais de longo prazo estáticas.
* **Mecanismos de Confiança IAM:** Estruturação e edição de políticas de confiança (*Trust Policies*), perfis de execução específicos para serviços e políticas de privilégio mínimo em formato JSON, garantindo que a Lambda acesse estritamente escopos delimitados no DynamoDB e CloudWatch.
* **Orquestração Subjacente:** Rastreabilidade e análise dos bastidores de provisionamento automatizado de recursos (Security Groups, EC2 e Elastic IPs) através do AWS CloudFormation.
* **Monitoramento Proativo & Rastreamento:** Configuração de alarmes baseados em limites de métricas críticas (como `CPUUtilization`), auditoria de requisições HTTP em API Gateway e consolidação estruturada de grupos de logs no **Amazon CloudWatch Logs** para inspeção em tempo real e depuração de fluxos lógicos e códigos Python.
* **Rastreabilidade e Governança:** Provisionamento de trilhas de auditoria globais com CloudTrail para registro imutável de chamadas de API de segurança no S3.
* **Políticas de Acesso Públicas e Seguras:** Engenharia de segurança e liberação controlada de recursos usando S3 Bucket Policies estruturadas via JSON com controle estrito de `Principal` e ações direcionadas (`GetObject`).
* **Higienização de Dados:** Aplicação de boas práticas de segurança na publicação de evidências de infraestrutura, com o correto mascaramento de Account IDs, e-mails e escopos de IPs públicos e privados.
* **Gerenciamento de Segredos:** Centralização de credenciais sensíveis via SSM Parameter Store e criptografia em repouso controlada por chaves do AWS KMS sob o princípio do privilégio mínimo.
* **Governança de Custos (FinOps):** Monitoramento financeiro proativo para manutenção de uma nuvem sustentável e eficiente.

---

## 👩‍💻 Conecte-se Comigo
Se você quiser acompanhar a minha transição de carreira para o setor de tecnologia ou trocar ideias sobre o ecossistema AWS:
* **LinkedIn:** [giane-costa](https://www.linkedin.com/in/giane-costa/)
* **GitHub:** [Giane10](https://github.com/Giane10)