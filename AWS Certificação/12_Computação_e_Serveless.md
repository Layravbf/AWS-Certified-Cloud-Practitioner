# 12_Computação_e_Serveless

### AWS Batch

Batch → grupo de tarefas que devem ser executadas ao mesmo tempo ou em uma sequência pré-definida

É um serviço que permite a execução de trabalhos em lote em qualquer escala, de forma totalmente gerenciada, sem a necessidade de gerenciar infraestrutura de servidores.

- **Escalonamento Automático**: Dimensiona automaticamente a quantidade de recursos computacionais com base no volume e nas necessidades dos trabalhos, otimizando custos e desempenho.
- **Trabalhos em Lote Diversos**: Suporta a execução de trabalhos em lote para uma ampla variedade de casos, como processamento de dados, análise de grandes volumes de informações e simulações.
- **Integração com Outros Serviços AWS**: Funciona em conjunto com serviços como Amazon EC2 e EC2 Spot Instances para executar tarefas com eficiência de custo.

O AWS Batch é ideal para executar grandes volumes de tarefas computacionais de forma escalável e sem precisar configurar manualmente clusters ou gerenciar servidores.

### AWS LightSail

O Amazon Lightsail é um serviço que oferece servidores virtuais privados (VPS), armazenamento, bancos de dados e redes balanceamento de carga a um custo acessível. É projetado para simplificar o lançamento e gerenciamento de aplicações na AWS, especialmente para pequenas empresas, desenvolvedores e estudantes que estão começando a usar a nuvem.

É um serviço ideal para quem está começando com a computação em nuvem, oferecendo um ponto de partida simples e de baixo custo para hospedar aplicações, sites, blogs, e outros projetos na AWS.

### AWS Lambda

É um serviço de computação que executa seu código em resposta a eventos e gerencia automaticamente os recursos computacionais para você, tornando mais fácil a implantação de aplicações que escalam individualmente em resposta a novas informações.

1. **Execução de Código sem Servidor**: O AWS Lambda executa o código em um ambiente computacional de alta disponibilidade, o que significa que você não precisa se preocupar em provisionar, escalar, ou gerenciar quaisquer servidores.
    
2. **Resposta a Eventos em Tempo Real**: Você pode executar seu código em resposta a desencadeadores (triggers), como alterações em um bucket do Amazon S3, atualizações em uma tabela do DynamoDB, solicitações HTTP personalizadas ou até mesmo em novos fluxos de dados no Kinesis.
    
3. **Escalabilidade Automática**: Sua aplicação escala automaticamente com o AWS Lambda. Quando seu código não está sendo executado, você não paga nada. O serviço gerencia toda a capacidade, patching de segurança, monitoramento e registro de logs.
    
4. **Personalização de Recursos Computacionais**: Você pode ajustar a quantidade de memória alocada para sua função e o AWS Lambda alocará proporcionalmente a CPU, o disco de E/S e a largura de banda da rede.
    
5. **Programação em Múltiplas Linguagens**: O AWS Lambda suporta código escrito em JavaScript (Node.js), Python, Java (Java 8 & 11), .NET (C#), Go, Ruby e PowerShell. Também oferece um Runtime API que permite o uso de qualquer linguagem de programação adicional para a criação de funções.
    
6. **Integração Profunda com a AWS**: O AWS Lambda está integrado ao ecossistema da AWS, o que significa que ele pode ser acionado diretamente por outros serviços da AWS.
    
7. **Modelo de Preço Baseado em Uso**: Você paga apenas pelo tempo de computação que consome - não há cobrança quando seu código não está sendo executado.

Resumindo, o AWS Lambda é uma ferramenta de computação eficiente e flexível que permite a execução de código sem a necessidade de gerenciar servidores, proporcionando um modelo de desenvolvimento focado em responder a eventos e construir aplicações orientadas a microserviços.

### AWS Fargate

É um serviço de computação sem servidor para contêineres que permite executar aplicações sem ter que gerenciar a infraestrutura subjacente. Ele funciona com o Amazon Elastic Container Service (ECS) e o Amazon Elastic Kubernetes Service (EKS), simplificando a tarefa de executar contêineres em escala.

Resumindo, o AWS Fargate é uma opção poderosa e flexível para a execução de aplicações baseadas em contêineres na AWS, eliminando a necessidade de gerenciar a infraestrutura subjacente e permitindo que os desenvolvedores se concentrem em construir aplicações eficazes e eficientes.