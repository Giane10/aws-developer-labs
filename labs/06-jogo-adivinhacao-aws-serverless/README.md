# ☁️ Lab 06: Jogo de Adivinhação Serverless com Amazon S3, API Gateway e AWS Lambda

## 🎯 Objetivo do Projeto
Este laboratório documenta a implementação de uma aplicação web interativa e 100% serverless na AWS. O foco principal foi construir um jogo de adivinhação integrando um frontend estático hospedado em nuvem com um backend dinâmico, demonstrando como diferentes serviços da AWS se comunicam de forma segura sem a necessidade de provisionar ou gerenciar servidores tradicionais.

---

## 🗺️ Arquitetura do Sistema

![Arquitetura do Sistema](arquitetura.png)

O fluxo de execução segue o modelo clássico de arquitetura serverless orientada a eventos:

`Cliente (Navegador)` ➔ `Amazon S3 (Website Estático)` ➔ `Amazon API Gateway (HTTP API)` ➔ `AWS Lambda (Python 3.13)` ➔ `Retorno JSON (Resultado)`

### 🔄 Detalhes do Fluxo de Requisições:
1. **Frontend (Amazon S3):** O usuário acessa a interface do jogo através do Endpoint público gerado pelo S3 e insere um número de 1 a 10.
2. **Comunicação (CORS e API Gateway):** O script da página realiza uma requisição HTTP GET para a rota `/jogo` do API Gateway. O CORS garante que a origem (o site no S3) tem permissão para acessar a API.
3. **Processamento (AWS Lambda):** O API Gateway aciona a função Lambda, passando o número escolhido pelo usuário. A Lambda processa a lógica em Python e verifica se o usuário acertou o número secreto.
4. **Resposta ao Cliente:** A Lambda devolve o resultado para o API Gateway, que o repassa ao site no S3, exibindo a mensagem final na tela do usuário.

---

## 🛠️ Tecnologias e Recursos Explorados
* **Amazon S3:** Hospedagem de site estático (Static Website Hosting), configuração de acesso público e criação de Políticas de Bucket (Bucket Policies) baseadas em JSON.
* **Amazon API Gateway (HTTP API):** Criação de rotas, configuração de métodos (`GET`) e configuração essencial de segurança CORS (Cross-Origin Resource Sharing).
* **AWS Lambda:** Criação do backend utilizando o runtime **Python 3.13**, recebendo eventos do API Gateway e retornando respostas estruturadas.

---

## ⚙️ Passo a Passo da Implementação

* **Passo 1:** Criação da função Lambda `LambdaGame` utilizando Python 3.13 e upload do pacote de código (arquivo `.zip`).
* **Passo 2:** Criação de uma HTTP API no Amazon API Gateway com integração direta à função Lambda recém-criada, utilizando o caminho de recurso `/jogo`.
* **Passo 3:** Configuração rigorosa do CORS no API Gateway, permitindo todas as origens (`*`), cabeçalhos `content-type` e o método `GET`.
* **Passo 4:** Customização do arquivo `index.html` inserindo a URL de Invocação da API (Invoke URL) e personalização da interface gráfica.
* **Passo 5:** Criação de um bucket S3 globalmente exclusivo, upload do arquivo HTML e ativação da funcionalidade de "Hospedagem de site estático".
* **Passo 6:** Edição das configurações de segurança do bucket S3, desmarcando o bloqueio de acesso público e gerando/aplicando uma `Bucket Policy` com a permissão `s3:GetObject` para habilitar o acesso via navegador.

---

## 🧪 Validação e Testes Práticos
Para comprovar a comunicação ponta a ponta da arquitetura, a aplicação foi testada diretamente através do navegador:
* Acesso ao link do **Endpoint de site de bucket** gerado pelo S3.
* A interface web foi carregada com sucesso, exibindo o nome customizado no frontend.
* Inserção de valores no formulário de adivinhação.
* Validação do retorno assíncrono na tela (mensagens de acerto ou erro), comprovando o acionamento do gatilho entre o frontend (S3), a camada de roteamento (API Gateway) e a computação (Lambda).

---

## 🎓 Foco na Certificação AWS Developer (DVA-C02)
Este projeto consolida conhecimentos adquiridos na certificação Cloud Practitioner e avança em tópicos cobrados no exame DVA-C02:
* **Políticas IAM baseadas em Recursos:** Escrita e compreensão da estrutura JSON de uma *Bucket Policy* para expor objetos estáticos de forma segura.
* **Troubleshooting de CORS:** Entendimento prático de um dos erros mais comuns em integrações web serverless e como resolvê-lo configurando os cabeçalhos corretos no API Gateway.
* **Integração S3 e API Gateway:** Padrão arquitetural amplamente utilizado para aplicações modernas de página única (SPAs).

---

## 📄 Documentação Acadêmica
Se você deseja visualizar o relatório detalhado com os prints do console da AWS e as validações de cada etapa, acesse:
📎 [Clique aqui para visualizar o PDF do Entregável Completo](./Lab6_Jogo_de_Adivinhacao_GianeCosta.pdf)

---

## 👩‍💻 Autor
Laboratório executado por [Giane Costa](https://www.linkedin.com/in/giane-costa/).