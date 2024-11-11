# 05_Escalabilidade_EC2

## Escalabilidade

- Vertical → A escalabilidade vertical envolve **aumentar a capacidade de um único recurso**, como um servidor ou banco de dados, aumentando seu poder de processamento, memória, armazenamento, ou capacidade de rede.
- Horizontal → A escalabilidade horizontal envolve **adicionar mais recursos distribuídos** ao sistema, como adicionar mais servidores ou nós para lidar com a carga crescente. Em vez de aumentar a potência de um único servidor, você distribui a carga em vários servidores ou máquinas. O serviço dentro da AWS que faz essa escalabilidade horizontal é o AutoScaling + ELB

## Elasticidade

Capacidade do seu sistema se adaptar automaticamente às mudanças (load/carga).

Se os servidores estão com a carga muito alta de utilização, há a necessidade de criar um novo servidor ou então o contrário, um servidor não esta sendo utilizado, essa habilidade de expandir e reduzir é a ELASTICIDADE. Aumentar/reduzir a capacidade conforme necessário. Feito pelo AutoScaling + ELB.

## Disponibilidade

Estar disponível. Ter servidores em diferentes zonas de disponibilidades garante estar sempre disponível. Feito pelo AutoScaling.

## AutoScaling

O Amazon Auto Scaling é um serviço da AWS que permite o dimensionamento automático de recursos para manter a performance e a disponibilidade de suas aplicações. Ele funciona monitorando continuamente suas aplicações e ajustando a capacidade para manter a performance estável e previsível ao menor custo possível.

Aqui estão algumas características principais do Amazon Auto Scaling:

1. **Dimensionamento Automático**: O Auto Scaling permite que você defina políticas de dimensionamento que ajustam automaticamente a capacidade de recursos com base nas condições definidas. Por exemplo, você pode dimensionar automaticamente o número de instâncias do Amazon EC2 para atender à demanda de tráfego.
    
2. **Otimização de Custo e Performance**: Ao ajustar continuamente a capacidade, o Auto Scaling ajuda a melhorar a disponibilidade e minimizar os custos. Quando a demanda aumenta, o Auto Scaling adiciona automaticamente mais recursos. Quando a demanda diminui, ele remove os recursos desnecessários para economizar dinheiro.
    
3. **Balanceamento de Carga**: O Auto Scaling pode ser usado junto com o Elastic Load Balancing (ELB) para distribuir o tráfego de aplicações entre várias instâncias EC2 para melhorar a disponibilidade e a tolerância a falhas.
    
4. **Saúde da Aplicação**: O Auto Scaling realiza verificações de saúde em suas instâncias EC2 e substitui automaticamente as instâncias que não estão saudáveis.
    
5. **Integração AWS**: O Auto Scaling está integrado com uma série de serviços da AWS, incluindo Amazon CloudWatch, Amazon SNS, AWS CloudFormation, entre outros.
    
6. **Flexibilidade**: O Auto Scaling permite dimensionar vários recursos, não se limitando apenas às instâncias EC2. Você também pode dimensionar serviços como Amazon DynamoDB, Amazon Aurora, Amazon ECS, e Amazon RDS.

Em resumo, o Amazon Auto Scaling é um serviço eficaz e essencial para otimizar a performance e a disponibilidade de suas aplicações na AWS, garantindo que você tenha o número certo de recursos da AWS quando precisar.

## ELB (Elastic Load Balance)

O Elastic Load Balancing (ELB) é um serviço da Amazon Web Services (AWS) que distribui automaticamente o tráfego de entrada de aplicações em várias instâncias EC2, contêineres, endereços IP e funções Lambda para garantir que as aplicações tenham alta disponibilidade e desempenho.

Aqui estão algumas características principais do ELB:

1. **Tipos de Balanceador de Carga**: O ELB oferece três tipos de balanceadores de carga que se adequam a diferentes necessidades de aplicação - o Balanceador de Carga de Aplicação (ALB) para tráfego HTTP e HTTPS, o Balanceador de Carga de Rede (NLB) para tráfego TCP, UDP e TLS, e o Classic Load Balancer para tráfego HTTP, HTTPS, TCP e SSL.
    
2. **Alta disponibilidade**: O ELB distribui automaticamente o tráfego em várias instâncias em várias zonas de disponibilidade para garantir a continuidade do serviço, mesmo se uma ou mais instâncias falharem.
    
3. **Escalabilidade**: O ELB escala automaticamente a sua capacidade de balanceamento de carga em resposta ao tráfego de entrada.
    
4. **Integração com o Auto Scaling**: O ELB trabalha em conjunto com o Auto Scaling da AWS para garantir que há capacidade suficiente para atender ao tráfego de entrada e para substituir as instâncias que falham.
    
5. **Segurança**: O ELB oferece recursos de segurança como a integração com o AWS Certificate Manager para SSL/TLS, e a integração com o AWS Identity Access Management (IAM) para controle de acesso.
    
6. **Monitoramento e Auditoria**: O ELB integra-se com o Amazon CloudWatch e o AWS CloudTrail para monitorar o desempenho de suas aplicações e registrar as ações realizadas no seu balanceador de carga.
    
Resumindo, o Elastic Load Balancing é uma ferramenta essencial para a distribuição eficiente de tráfego, melhorando a disponibilidade e a tolerância a falhas das suas aplicações na AWS.