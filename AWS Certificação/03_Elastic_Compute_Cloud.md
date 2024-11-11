# 03_Elastic_Compute_Cloud

Infraestrutura como serviço (IaaS) para máquinas virtuais

### Como Era Antes da Virtualização:

1. **Servidores Físicos**:
    - Antes, para rodar uma aplicação ou um site, você precisava de um **servidor físico** dedicado, ou seja, uma máquina (hardware) que ficasse em um data center.
    - O servidor físico rodava um sistema operacional (Windows, Linux, etc.) e era configurado para executar suas aplicações.

2. **Alto Custo e Manutenção**:
    - Você precisava comprar e manter um servidor, o que era caro. Além do custo inicial, havia despesas com energia elétrica, refrigeração, espaço físico e manutenção de hardware.
    - Se você quisesse mais capacidade (mais CPU, memória ou armazenamento), precisava **comprar novos servidores**, o que levava tempo e aumentava os custos.

3. **Subutilização dos Recursos**:
    - Um problema comum era que muitos servidores não utilizavam todo o seu potencial. Por exemplo, um servidor dedicado a uma aplicação poderia usar apenas 20% da capacidade de processamento, deixando os outros 80% ociosos, sem uso eficiente.

4. **Escalabilidade Limitada**:
    - Se você tivesse um pico de usuários ou demanda de processamento, era difícil aumentar rapidamente a capacidade do servidor. Muitas vezes, as empresas compravam mais servidores do que precisavam, apenas para garantir que não teriam problemas no futuro.

### Como Funciona Hoje com a Virtualização e Hypervisor:

1. **Virtualização e Hypervisor**:
    - A virtualização permite que um **único servidor físico** seja dividido em várias **máquinas virtuais (VMs)**.
        
    - O **hypervisor** é o software que permite essa divisão. Ele cria várias máquinas virtuais (cada uma rodando seu próprio sistema operacional) em cima do servidor físico. Isso é ilustrado na imagem com várias "OS" (sistemas operacionais) rodando em um único hardware.
        
    - Cada máquina virtual tem seus próprios recursos dedicados (CPU, memória, disco), mas na verdade elas estão compartilhando os recursos de um único servidor físico.
        
2. **Eficiência e Flexibilidade**:
    - Com a virtualização, o uso do hardware é muito mais eficiente. Se uma VM usa 30% da CPU, outra VM pode usar o restante, aproveitando ao máximo a capacidade do servidor.
    - Isso também permite que diferentes aplicações rodem no mesmo hardware, sem interferir umas nas outras, já que cada VM tem seu próprio sistema operacional e ambiente isolado.
    
3. **Escalabilidade Rápida**:
    - Agora, se você precisa de mais capacidade, pode criar **novas máquinas virtuais** em minutos, sem precisar comprar mais hardware. Por exemplo, no **Amazon EC2**, você pode iniciar ou parar instâncias (servidores virtuais) conforme necessário.
    - Se uma aplicação precisa de mais capacidade apenas durante alguns dias ou horas, você pode aumentar temporariamente o número de instâncias (escalabilidade), sem gastar dinheiro com hardware adicional.
    
4. **Redução de Custos**:
    - A virtualização e o uso de hypervisors permitem que as empresas aluguem recursos de computação apenas pelo tempo e pela capacidade que realmente usam, em vez de comprar e manter seus próprios servidores.
    - Serviços como o EC2 cobram por hora de uso, o que reduz bastante os custos.

### Comparação Simples:

- **Antes da Virtualização**: Para cada servidor físico, você rodava apenas uma aplicação, e o servidor físico ficava frequentemente subutilizado. Havia custos altos para adquirir e manter hardware, e era difícil aumentar ou reduzir a capacidade.
    
- **Depois da Virtualização (com Hypervisor)**: Agora, você pode rodar várias máquinas virtuais em um único servidor físico, otimizando o uso dos recursos. Isso permite que você crie e escale servidores virtuais rapidamente, com custos muito menores e sem a necessidade de comprar hardware adicional.
    

O **Amazon EC2** se baseia nessa tecnologia de virtualização, permitindo que você crie, gerencie e escale seus servidores virtuais na nuvem de maneira flexível e com baixo custo, usando a infraestrutura da AWS.

1. **Máquinas Virtuais**: EC2 fornece instâncias, que são máquinas virtuais executando os sistemas operacionais que você escolher.
    
2. **Escalabilidade**: Você pode dimensionar a capacidade de computação facilmente, criando e lançando novas instâncias conforme necessário, o que é útil para lidar com picos de demanda e escala.
    
3. **Controle Completo**: Os usuários têm controle total sobre as instâncias do EC2. Eles têm acesso de root, e podem interagir com elas como fariam com qualquer máquina.
    
4. **Várias Regiões e Zonas de Disponibilidade**: As instâncias do EC2 podem ser implantadas em várias regiões geográficas e zonas de disponibilidade. Isso ajuda a reduzir latência, aumentar a tolerância a falhas e cumprir os requisitos de residência de dados.
    
5. **Modelos de Instância**: O EC2 fornece uma variedade de tipos de instâncias otimizadas para diferentes casos de uso, garantindo que você tenha os recursos de que precisa para o aplicativo que está executando.
    
6. **Preços Flexíveis**: O EC2 oferece várias opções de preços, incluindo On-Demand (pague pelo que usar), Reservado (reserve uma instância por um período e obtenha um desconto) e Spot (licitação por capacidade não utilizada a preços mais baixos).
    
7. **Armazenamento Integrado**: As instâncias do EC2 podem ser integradas com outros serviços da AWS para fornecer armazenamento (por exemplo, Amazon EBS), bancos de dados (por exemplo, Amazon RDS), e redes (por exemplo, Amazon VPC).
    
8. **Segurança**: O EC2 trabalha com o Amazon VPC para fornecer segurança e robustez por meio de grupos de segurança e redes isoladas.

## Tipos de Instâncias

[Tipos de instâncias do Amazon EC2](https://aws.amazon.com/pt/ec2/instance-types/)

Os tipos de instâncias compreendem combinações variadas de capacidade de CPU, memória, armazenamento e rede e proporcionam a flexibilidade para escolher a combinação apropriada de recursos para seus aplicativos. Os principais tipos de instâncias do Amazon EC2 incluem:

1. **Instâncias de Uso Geral (A, T, M)**: Essas instâncias proporcionam um bom equilíbrio de computação, memória e rede e são uma boa escolha para muitas cargas de trabalho que não requerem especificações de hardware específicas.
    
2. **Instâncias Otimizadas para Computação (C)**: Essas instâncias são otimizadas para cargas de trabalho que exigem alta performance de CPU, como computação científica, modelagem e análise financeira, e renderização de mídia.
    
3. **Instâncias Otimizadas para Memória (R, X, Z)**: Essas instâncias são projetadas para cargas de trabalho que processam grandes conjuntos de dados na memória, como bancos de dados em memória, caches distribuídos, análise em memória e aplicações de big data.
    
4. **Instâncias Otimizadas para Armazenamento (D, I, H)**: Essas instâncias são projetadas para cargas de trabalho que requerem alto desempenho de armazenamento local, como bancos de dados escalonáveis, processamento de dados em escala de petabytes e aplicações de data warehousing.
    
5. **Instâncias Otimizadas para GPU (P, G, F, Inf)**: Essas instâncias são projetadas para cargas de trabalho de computação gráfica, como aprendizado de máquina, mineração de criptomoedas, renderização 3D, e aplicações de streaming de jogos.
    
6. **Instâncias Arm (A1, M6g, C6g, R6g)**: Essas instâncias são baseadas na arquitetura Arm e são uma opção de baixo custo para cargas de trabalho que requerem um bom desempenho de CPU e suportam a arquitetura Arm.
## Modelos de Aquisição

- **Sob Demanda**: Permite que você crie e utilize instâncias de EC2 sempre que necessário, pagando apenas pelo tempo em que a instância está ativa (por hora ou segundo). Não há compromisso a longo prazo, sendo ideal para cargas de trabalho temporárias ou variáveis. No entanto, esse modelo tende a ser o mais caro em termos de custo por hora.

- **Saving Plans**: Esse modelo oferece um desconto em troca de um compromisso de uso de 1 a 3 anos. Ou seja, você se compromete a pagar por uma determinada quantidade de capacidade de computação por um período, garantindo um preço mais baixo em relação às instâncias sob demanda. Isso é vantajoso para empresas que têm cargas de trabalho previsíveis e que podem se comprometer com o uso por um período longo.

- **Spot Instances**: Oferecem as instâncias EC2 a um preço significativamente mais baixo (até 90% de desconto), usando capacidade de computação ociosa. No entanto, essas instâncias podem ser interrompidas pela AWS quando a capacidade é necessária para outros usos. Isso as torna ideais para cargas de trabalho que podem tolerar interrupções, como processamento em lote, simulações ou outras tarefas de computação intensiva que não exigem tempo de execução contínuo.

- **Host Dedicados**: São servidores físicos inteiramente dedicados a um único cliente, garantindo isolamento completo do hardware. São mais caros e utilizados principalmente por instituições financeiras, governos ou organizações que precisam de maior controle e conformidade com regulamentações, como licenciamento de software ou requisitos de auditoria

- **Capacidade por Demanda**: Permite que você utilize instâncias conforme necessário, pagando apenas pelo que usar, ideal para cenários com demanda variável ou imprevisível. Esse modelo oferece flexibilidade e escalabilidade, mas pode ser mais caro para uso contínuo em comparação com outros modelos como Savings Plans ou Spot Instances.

## Security Group

Os Security Groups atuam como um firewall virtual para as suas instâncias Amazon EC2 para controlar o tráfego de entrada e saída. Eles operam ao nível da instância, o que significa que você pode associar diferentes security groups a diferentes instâncias, o que é útil para configurar a segurança a um nível granular.

Características principais dos Security Groups na AWS:

1. **Regras de entrada e saída**: Cada security group consiste em um conjunto de regras de entrada e saída. As regras de entrada controlam o tráfego que é permitido chegar à instância associada ao security group, enquanto as regras de saída controlam o tráfego permitido para sair da instância.
    
2. **Estado de conexão**: Os security groups são "stateful", o que significa que se você enviar uma solicitação de uma instância, a resposta é permitida automaticamente, independentemente das regras de saída.
    
3. **Permissões por protocolo**: As regras em um security group permitem especificar protocolos permitidos, portas e origem (para tráfego de entrada) ou destino (para tráfego de saída). Isso permite que você restrinja o tráfego para um protocolo ou porta específicos e controle de onde o tráfego é originado ou para onde ele é direcionado.
    
4. **Flexibilidade e controle**: Você pode associar diferentes security groups a diferentes instâncias e também pode modificar as regras de um security group a qualquer momento. As novas regras são aplicadas automaticamente a todas as instâncias associadas ao security group.
    
5. **Isolamento de instâncias**: Os security groups ajudam a isolar suas instâncias de outras instâncias na mesma rede, uma vez que as regras são aplicadas por instância e não por sub-rede.