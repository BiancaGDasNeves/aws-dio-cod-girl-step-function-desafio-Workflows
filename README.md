# 🧠 aws-dio-cod-girl-step-function-desafio-Workflows  
### Repositório do Desafio: *"Explorando Workflows Automatizados com AWS Step Functions"*

---

## 🚀 Desafio DIO - AWS Step Functions: Automação de Workflows

Este repositório faz parte do desafio **"AWS Step Functions: Automação de Workflows"** da trilha **Code Girls | DIO**.  
O objetivo é aplicar, de forma prática, os conceitos de **automação, mensageria e orquestração de serviços AWS**, criando um workflow funcional e bem documentado.

---

## 🧠 Objetivos de Aprendizagem

- Aplicar os conceitos aprendidos nas aulas práticas.  
- Criar e executar workflows automatizados utilizando **AWS Step Functions**.  
- Integrar serviços AWS como **Lambda**, **S3**, **SNS**, **SQS** e **DynamoDB**.  
- Documentar os processos técnicos de forma clara, organizada e didática.  
- Utilizar o **GitHub** para versionamento e compartilhamento do projeto.

---

## ⚙️ Tecnologias e Serviços Utilizados

- 🧩 **AWS Step Functions** — orquestração de workflows  
- 🪄 **AWS Lambda** — execução de funções serverless  
- 🗂️ **Amazon S3** — armazenamento de arquivos  
- 📬 **Amazon SNS** — notificações automáticas  
- 🧾 **Amazon DynamoDB** — banco de dados NoSQL  
- 💻 **GitHub / Markdown** — documentação e versionamento  

---

## 🧩 Estrutura do Workflow

O fluxo criado realiza as seguintes etapas:

1. **Receber arquivo** — Upload no bucket S3.  
2. **Validar arquivo** — Função Lambda verifica se o arquivo está correto.  
3. **Decisão** — Caso o arquivo seja válido, o processo continua; caso contrário, uma notificação de erro é enviada.  
4. **Processamento** — Outra função Lambda processa os dados válidos.  
5. **Notificação final** — SNS informa o sucesso ou falha da execução.

---

## 📄 Definição do Workflow (Exemplo JSON)

```json
{
  "Comment": "Workflow para validar e processar arquivos S3 com Lambda e SNS",
  "StartAt": "ValidarArquivo",
  "States": {
    "ValidarArquivo": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:001758140394:function:ValidaArquivo",
      "Next": "DecisaoArquivo"
    },
    "DecisaoArquivo": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.valido",
          "BooleanEquals": true,
          "Next": "ProcessarArquivo"
        }
      ],
      "Default": "NotificarErro"
    },
    "ProcessarArquivo": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:001758140394:function:ProcessaArquivo",
      "Next": "NotificarSucesso"
    },
    "NotificarErro": {
      "Type": "Task",
      "Resource": "arn:aws:states:::sns:publish",
      "Parameters": {
        "Message": "Arquivo inválido detectado no bucket S3",
        "TopicArn": "arn:aws:sns:us-east-1:001758140394:NotificacoesErros"
      },
      "End": true
    },
    "NotificarSucesso": {
      "Type": "Task",
      "Resource": "arn:aws:states:::sns:publish",
      "Parameters": {
        "Message": "Arquivo processado com sucesso!",
        "TopicArn": "arn:aws:sns:us-east-1:001758140394:NotificacoesSucesso"
      },
      "End": true
    }
  }
}
```
---

## 💡 Insights e Aprendizados
Durante o desafio, pude compreender de forma prática:

A importância de orquestrar processos em aplicações distribuídas.

Como o Step Functions facilita o controle de fluxos complexos entre serviços AWS.

O uso de Choice States para lógica condicional e de SNS para mensageria.

A relevância de documentar e versionar projetos para aprendizado contínuo.

📘 Mais reflexões e anotações podem ser encontradas no arquivo insights.md.

---

## ✨ Autora
👩‍💻 Bianca Gonçalves das Neves
📧 biancagneves@gmail.com
💼 linkedin.com/in/biancagneves

---

## 🏁 Conclusão
Este desafio reforçou o poder da automação e orquestração na nuvem através do AWS Step Functions.
Com ele, é possível criar fluxos inteligentes, reduzir falhas e aumentar a eficiência operacional de forma serverless e escalável.
