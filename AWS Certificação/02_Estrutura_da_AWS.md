# 02_Estrutura_da_AWS

A AWS organiza sua infraestrutura em regiões e zonas de disponibilidade para garantir alta disponibilidade e resiliência. Cada **região** é um local geográfico distinto no mundo, como `us-east-1` (Norte da Virgínia) ou `sa-east-1` (São Paulo). Dentro de cada região, a AWS possui múltiplas zonas de disponibilidade.

### Regiões

Uma região da AWS é uma área geográfica que contém pelo menos duas Zonas de Disponibilidade. Cada região é completamente independente das outras regiões, o que ajuda a isolar falhas e evitar a propagação de problemas de uma região para outra. Em setembro de 2024, a AWS tinha 34 regiões geográficas ao redor do mundo.

### Availability Zones (AZs)

As **Availability Zones** (Zonas de Disponibilidade) são data centers isolados fisicamente e independentes dentro de uma mesma região, mas interconectados com baixa latência. Cada zona de disponibilidade é alimentada e resfriada de forma independente e tem uma rede e conectividade redundante, garantindo alta disponibilidade e tolerância a falhas. Isso significa que, mesmo que uma AZ tenha um problema, as outras continuarão funcionando normalmente.

Ao implementar aplicações na AWS, é recomendado distribuir recursos através de múltiplas AZs para aumentar a resiliência e reduzir o risco de downtime (tempo de inatividade).

### Local Zones

As **Local Zones** (Zonas Locais) são uma extensão da infraestrutura da AWS, trazendo certos serviços da AWS, como computação, armazenamento, banco de dados e outros, para mais perto dos usuários finais. Elas são projetadas para aplicações que precisam de latência muito baixa e maior proximidade com usuários finais em áreas geográficas específicas que estão longe das regiões principais da AWS.

Por exemplo, se você tiver uma aplicação que deve ser extremamente responsiva para usuários em uma cidade específica, como Los Angeles, mas a região da AWS mais próxima está em Oregon, você pode usar uma Local Zone em Los Angeles para reduzir a latência e melhorar a performance.

Essas zonas são ideais para cenários como streaming de mídia, jogos em tempo real, ou aplicações sensíveis à latência, onde cada milissegundo conta.

### WaveLength

**Wavelength** é um serviço da AWS que estende os serviços de computação e armazenamento da AWS para as redes 5G, permitindo que você crie aplicações que exigem latências ultra-baixas para dispositivos móveis e conectados.

### Como funciona o Wavelength?

O AWS Wavelength integra serviços da AWS, como Amazon EC2, Amazon EBS e Amazon VPC, diretamente nas redes 5G dos provedores de telecomunicações. Isso significa que as aplicações podem ser executadas muito mais próximas dos dispositivos móveis, como smartphones, carros conectados ou dispositivos IoT, reduzindo drasticamente a latência.

### Outposts

**Outposts** é um serviço da AWS que permite que você execute serviços da AWS diretamente em suas próprias instalações, como se estivesse usando a infraestrutura da AWS na nuvem. Com o AWS Outposts, você pode levar a infraestrutura, os serviços, as APIs e as ferramentas da AWS para praticamente qualquer data center, espaço de colocation ou instalação local.

### Como Funciona o AWS Outposts?

O AWS Outposts é uma solução de infraestrutura totalmente gerenciada que traz o mesmo hardware usado nas regiões da AWS diretamente para suas instalações. Ele é projetado para fornecer uma experiência consistente de nuvem híbrida, onde você pode usar os mesmos serviços, APIs e ferramentas AWS, independentemente de onde seus dados ou aplicações estejam rodando.

## AWS Share Responsibility Model

![[2024-09-03_17-28-15_.png]]

### Estrutura do Shared Responsibility Model

1. **Responsabilidades da AWS ("Segurança DA Nuvem")**:
    
    - **Infraestrutura Global**: A AWS é responsável pela proteção da infraestrutura que executa todos os serviços oferecidos na Nuvem AWS. Isso inclui hardware, software, redes e instalações que executam os serviços da AWS.
    - **Segurança Física**: A segurança física dos data centers da AWS, onde os servidores e equipamentos estão localizados, é de responsabilidade da AWS.
    - **Gerenciamento de Rede e Virtualização**: A AWS é responsável pela segurança da rede que conecta seus data centers, pela virtualização de servidores e pela infraestrutura subjacente que executa as máquinas virtuais (EC2, por exemplo).
    - **Segurança das Regiões, Zonas de Disponibilidade e Ponto de Presença**: A AWS gerencia e protege as regiões e zonas de disponibilidade globais, garantindo que sejam resistentes a falhas.
    
1. **Responsabilidades do Cliente ("Segurança NA Nuvem")**:
    
    - **Gerenciamento de Dados**: Os clientes são responsáveis pela proteção e criptografia de seus dados enquanto estão em trânsito e em repouso. Isso inclui a configuração de regras de acesso e políticas de gerenciamento de chaves.
    - **Gerenciamento de Identidade e Acesso**: Os clientes devem gerenciar as permissões e políticas de acesso, usando ferramentas como IAM (Identity and Access Management) para definir quem pode acessar os recursos na AWS.
    - **Configuração de Segurança de Aplicações**: Assegurar que as aplicações que você implementa na AWS estejam configuradas corretamente em termos de segurança, como firewalls, gerenciamento de patches, etc.
    - **Segurança do Sistema Operacional, Rede e Firewall**: Para serviços em que o cliente tem controle direto, como instâncias EC2, o cliente é responsável pela configuração do sistema operacional, firewall e segurança de rede.
    - **Gerenciamento de Patches**: Manter o sistema operacional e aplicações atualizados, aplicando patches de segurança e correções regularmente, também é responsabilidade do cliente.