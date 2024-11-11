# 11_Integrações_Cloud

### AWS Kinesis

Real-Time Data Streaming

Ele é frequentemente usado para transmitir dados como logs de aplicações, cliques em sites, dados de sensores IoT, entre outros, permitindo que as empresas obtenham insights em tempo real

- **Kinesis Data Streams**: Captura e armazena dados em tempo real para processá-los com aplicações de consumidores.
- **Kinesis Data Firehose**: Envia dados em tempo real para destinos como S3, Redshift ou Elasticsearch.
- **Kinesis Data Analytics**: Permite análises de fluxo de dados em tempo real usando SQL.
- **Kinesis Video Streams**: Transmite e processa fluxos de vídeo.

### AWS SQS

Simple Queue Service

É um serviço de mensageria totalmente gerenciado que permite o envio, recebimento e armazenamento de mensagens entre componentes de sistemas distribuídos, garantindo que as mensagens sejam processadas de forma assíncrona.

- **Garante Desacoplamento**: Facilita a comunicação entre diferentes partes de uma aplicação, permitindo que elas funcionem de forma independente.
- **Tipos de Fila**:
    - **Fila Padrão**: Oferece alta taxa de transferência e garante que as mensagens sejam entregues ao menos uma vez, mas a ordem das mensagens não é garantida.
    - **Fila FIFO (First-In-First-Out)**: Garante que as mensagens sejam processadas exatamente uma vez e na ordem correta.
- **Escalabilidade e Confiabilidade**: SQS é altamente escalável e pode lidar com milhões de mensagens por segundo, sendo utilizado em arquiteturas sem servidor ou microsserviços.

O SQS é ideal para aplicações que precisam gerenciar filas de trabalho ou comunicação entre serviços sem se preocupar com a perda de mensagens.

### AWS SNS

Simple Notification Service

É um serviço de mensageria da AWS que facilita a publicação de mensagens de forma assíncrona e o envio dessas mensagens para múltiplos assinantes simultaneamente.

1. **Modelo de Publicação/Assinatura (Pub/Sub)**: Os produtores (publicadores) enviam mensagens para um tópico SNS, e os consumidores (assinantes) recebem essas mensagens. Os assinantes podem ser serviços como Amazon SQS, funções Lambda, HTTP endpoints ou até notificações por SMS e e-mail.
2. **Entrega em Massa**: SNS permite a entrega em massa de mensagens a diferentes sistemas ou usuários finais de maneira eficiente.
3. **Alta Escalabilidade e Confiabilidade**: O SNS é escalável e gerenciado, garantindo que mensagens sejam entregues a todos os assinantes.

O SNS é ideal para arquiteturas onde múltiplos serviços precisam ser notificados de eventos em tempo real, como em sistemas distribuídos e aplicações que requerem notificações instantâneas.

Diferença SNS para SQS, o SQS armazena as mensagens por 4 dias e no máximo 14 dias, o SNS recebe o evento e envia direto, ele não armazena informação, ele apenas envia para quem está inscrito.