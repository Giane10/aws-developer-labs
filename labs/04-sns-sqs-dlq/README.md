# ☁️ Lab 04: Mensageria Assíncrona e Desacoplamento com Amazon SNS, SQS e DLQ

## 🎯 Objetivo do Projeto
Este laboratório documenta a implementação de uma arquitetura de mensageria altamente disponível e tolerante a falhas na AWS. O foco principal foi simular o padrão de integração de microsserviços onde eventos são publicados e processados de forma assíncrona, garantindo que falhas de processamento não causem perda de dados ou bloqueios no sistema.

---

## 🏗️ Arquitetura e Fluxo de Mensagens
O cenário simula um sistema de e-commerce ou aplicação distribuída onde um microsserviço (Publicador) precisa notificar outros serviços (Assinantes) sobre um evento importante, como a criação de um novo pedido.

1. **Publicação (Amazon SNS):** O evento é enviado para um Tópico SNS (barramento central).
2. **Distribuição (Fanout):** O SNS distribui a mensagem automaticamente para a Fila SQS assinante.
3. **Buffer e Consumo (Amazon SQS Padrão):** A fila atua como um buffer durável, retendo a mensagem até que o serviço consumidor a processe.
4. **Tolerância a Falhas (Amazon SQS DLQ):** Caso o consumidor falhe repetidamente em processar a mensagem (esgotando o limite de tentativas configurado), a mensagem é movida automaticamente para uma Dead-Letter Queue para análise isolada.

---

## 🛠️ Tecnologias e Recursos Explorados
* **Amazon SNS (Simple Notification Service):** Criação de Tópicos Padrão e configuração de assinaturas.
* **Amazon SQS (Simple Queue Service):** Filas Padrão, integração com SNS e recebimento de payloads JSON.
* **Dead-Letter Queues (DLQ):** Isolamento de mensagens problemáticas (*poison pills*).
* **Políticas de Acesso (IAM/Resource-based Policies):** Configuração de políticas baseadas em recursos no SQS permitindo a gravação de mensagens vindas do SNS (`sqs:SendMessage`).

---

## ⚙️ Passo a Passo da Implementação

* **Passo 1:** Criação da Dead-Letter Queue (DLQ) no Amazon SQS.
* **Passo 2:** Criação da Fila SQS Principal.
* **Passo 3:** Configuração da *Redrive Policy* na Fila Principal, vinculando-a à DLQ com um `maxReceiveCount` (Número máximo de recebimentos) definido como 3.
* **Passo 4:** Criação do Tópico Padrão no Amazon SNS.
* **Passo 5:** Inscrição (Subscription) da Fila SQS Principal no Tópico SNS.
* **Passo 6:** Edição da política de acesso da Fila SQS (JSON) para conceder permissão ao SNS.

---

## 🧪 Validação e Testes Práticos
Para comprovar a resiliência da arquitetura, o seguinte teste de falha foi executado com sucesso:
* Uma mensagem de teste (payload JSON simulando um pedido) foi publicada diretamente no Tópico SNS.
* A mensagem foi roteada com sucesso para a Fila SQS Principal.
* Simulou-se uma falha de processamento através de sondagens sucessivas sem a exclusão da mensagem.
* Após esgotar o *Visibility Timeout* e atingir o limite de 3 recebimentos configurados (`maxReceiveCount`), a mensagem foi automaticamente roteada para a DLQ.

---

## 🎓 Foco na Certificação AWS Developer (DVA-C02)
Este laboratório fixou conceitos cobrados com alta frequência no exame DVA-C02:
* **Visibility Timeout:** A importância de dimensionar o tempo de visibilidade para ser maior que o tempo de processamento do consumidor.
* **Padrão Fanout:** Utilização do SNS para notificar múltiplos SQS simultaneamente.
* **Redrive Policy:** Mecânica exata de transição de mensagens para a DLQ baseada no limite de falhas.
* **Raw Message Delivery:** A opção de remover metadados estruturais do SNS, entregando apenas o payload original para a fila.

---

## 👩‍💻 Autor
Laboratório executado por [Giane Costa](https://www.linkedin.com/in/giane-costa/).