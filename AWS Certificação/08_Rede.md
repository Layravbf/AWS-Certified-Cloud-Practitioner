# 08_Rede

Virtual Private Cloud

### 1. **Conceitos Básicos de VPC**

- A VPC é uma rede virtual definida pelo usuário na AWS, onde os recursos, como instâncias EC2, podem ser implantados.
- Permite controlar completamente o ambiente de rede, incluindo a seleção do intervalo de endereços IP, sub-redes, tabelas de roteamento e gateways de rede.

### 2. **Componentes Principais da VPC**

- **Subnets:** São divisões lógicas da VPC que permitem separar os recursos em sub-redes públicas e privadas.
    - **Sub-rede Pública:** Conectada à Internet por meio de um Internet Gateway.
    - **Sub-rede Privada:** Sem conexão direta à Internet.
- **Internet Gateway (IGW):** Permite a comunicação entre a VPC e a Internet.
- **NAT Gateway:** Habilita instâncias em sub-redes privadas a acessar a Internet de forma segura, sem aceitar tráfego de entrada da Internet.
- **Tabelas de Roteamento:** Controlam o direcionamento do tráfego de rede para dentro e fora da VPC.
- **Security Groups:** Atuam como firewall em nível de instância, controlando o tráfego de entrada e saída.
- **Network ACLs (NACLs):** Funcionam como firewall em nível de sub-rede, fornecendo controle adicional de segurança.
#### **Security Group**

- **Nível de Segurança:** Atua no nível da instância, ou seja, aplica-se diretamente aos recursos, como instâncias EC2.
- **Estado:** Stateful, o que significa que ele rastreia o estado das conexões. Se uma conexão de entrada for permitida, a resposta de saída correspondente será automaticamente permitida e vice-versa.
- **Regra de Tráfego:** As regras definem o que é permitido; qualquer coisa não explicitamente permitida é bloqueada por padrão.
- **Aplicação de Regras:** As regras podem ser aplicadas para permitir tráfego de entrada e saída com base em IPs, protocolos e portas específicas.
- **Número de Regras:** Pode ter regras para tanto entrada quanto saída.
#### **Network ACL (NACL)**

- **Nível de Segurança:** Atua no nível da sub-rede, controlando o tráfego que entra e sai de toda a sub-rede.
- **Estado:** Stateless, ou seja, não mantém o estado das conexões. Cada solicitação e resposta precisa ser explicitamente permitida.
- **Regra de Tráfego:** Pode ter regras de **permitir** e **negar** tráfego, o que oferece um controle mais granular.
- **Aplicação de Regras:** As regras são avaliadas em ordem numérica, começando pela regra de menor número até encontrar uma correspondência.
- **Número de Regras:** Tem limites para o número de regras, mas geralmente oferece mais flexibilidade para cenários complexos.

### 3. **CIDR (Classless Inter-Domain Routing)**

- Define o intervalo de endereços IP da VPC. Por exemplo, `10.0.0.0/16` significa uma VPC com 65.536 endereços IP disponíveis.
- Cada sub-rede também tem seu próprio intervalo CIDR dentro do intervalo da VPC.

### 4. **Peering e Conectividade**

- **VPC Peering:** Permite que duas VPCs se conectem para compartilhar recursos. Não há transição por meio da Internet, garantindo comunicação segura.
- **VPN Gateway e Direct Connect(link dedicado):** Oferecem conectividade entre a VPC e uma rede local (on-premises).
- **VPC Endpoints:** é um serviço que permite a conexão privada de sua VPC com serviços da AWS, como S3 e DynamoDB, sem a necessidade de um gateway de Internet, NAT ou VPN, mantendo o tráfego seguro dentro da rede da AWS. (Gateway → s3 e DynamoDB e Interface → outros serviços)
- **VPN Client:** permite que dispositivos individuais se conectem de forma segura a uma VPC na AWS por meio de uma conexão VPN, como se estivessem na mesma rede local.
- **VPN Site-to-Site:** estabelece uma conexão segura entre uma rede local (on-premises) e uma VPC na AWS, permitindo comunicação entre as duas redes como se fossem parte da mesma infraestrutura.
- **AWS PrivateLink:** permite acessar serviços da AWS de forma privada e segura por meio de interfaces de rede dentro da VPC, evitando que o tráfego passe pela Internet pública.
- **AWS Transit Gateway:** é um serviço que facilita a interconexão e gerenciamento de múltiplas VPCs e redes locais (on-premises) em uma arquitetura centralizada, funcionando como um hub para roteamento de tráfego e comunicação entre redes

### 5. **Casos de Uso Comuns**

- **Hospedagem de Aplicações Web:** Usar sub-redes públicas para servidores web e sub-redes privadas para bancos de dados.
- **Segurança e Compliance:** Implementar security groups e NACLs para proteger os recursos.

### 6. **Boas Práticas de Segurança**

- **Segmentação de Rede:** Usar sub-redes públicas e privadas para isolar serviços.
- **Gerenciamento de Tráfego:** Configurar tabelas de roteamento para controlar o fluxo de dados.
- **Monitoramento e Logs:** Utilizar serviços como CloudWatch e VPC Flow Logs para monitorar e auditar o tráfego.