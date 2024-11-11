# 10_Containers

### Docker

O Docker é uma plataforma que permite criar, implantar e gerenciar aplicativos em contêineres. Contêineres são unidades leves e portáteis que encapsulam um aplicativo e todas as suas dependências, permitindo que ele seja executado de forma consistente em diferentes ambientes.

### Amazon ECS 

O Amazon Elastic Container Service (ECS) é um serviço gerenciado de orquestração de contêineres que facilita a execução, gerenciamento e escalabilidade de aplicativos em contêineres na AWS.

O ECS permite que você execute contêineres Docker em um cluster de instâncias do Amazon EC2 ou em um modo sem servidor usando AWS Fargate. Aqui estão os principais componentes do Amazon ECS:

1. **Cluster**:
    
    - Um cluster é um agrupamento lógico de instâncias do Amazon EC2 ou de recursos gerenciados pelo Fargate, onde os contêineres são executados. Um cluster pode incluir várias instâncias EC2 ou pode ser gerenciado inteiramente pelo Fargate.
2. **Tarefa (Task)**:
    
    - Uma tarefa representa a execução de um ou mais contêineres em um cluster. As tarefas são definidas em um modelo de definição de tarefa (Task Definition) que descreve como os contêineres devem ser configurados, incluindo a imagem do contêiner, recursos necessários (CPU, memória), variáveis de ambiente e outras configurações.
3. **Definição de Tarefa (Task Definition)**:
    
    - A definição de tarefa é um arquivo JSON que especifica todos os parâmetros necessários para executar um contêiner. Isso inclui a configuração do contêiner, os volumes, as redes e as permissões necessárias.
4. **Serviço (Service)**:
    
    - Um serviço no ECS é usado para manter um número desejado de instâncias de tarefa em execução. Ele garante que as tarefas sejam iniciadas e mantidas em execução, mesmo que uma instância falhe. Os serviços podem ser configurados para usar balanceadores de carga, como o Elastic Load Balancer (ELB), para distribuir o tráfego entre as instâncias de tarefa.
5. **Scheduler**:
    
    - O scheduler do ECS é responsável por decidir onde e quando as tarefas devem ser executadas no cluster. Ele considera a capacidade disponível, os requisitos de recursos e as políticas de escalonamento.
6. **Registro de Contêiner (Container Registry)**:
    
    - O Amazon Elastic Container Registry (ECR) é um serviço de registro de contêineres que facilita o armazenamento, a distribuição e a implantação de imagens de contêineres. O ECS pode se integrar diretamente ao ECR para acessar imagens.
7. **Integrations com Outros Serviços AWS**:
    
    - O ECS se integra com outros serviços da AWS, como CloudWatch (para monitoramento e logs), IAM (para controle de acesso e permissões), e VPC (para configuração de rede).

### Amazon EKS

O Amazon Elastic Kubernetes Service (EKS) é um serviço de gerenciamento de contêineres que facilita a execução, escalabilidade e monitoramento de aplicações baseadas em contêineres usando o Kubernetes, um sistema de orquestração de contêineres de código aberto, na plataforma AWS.