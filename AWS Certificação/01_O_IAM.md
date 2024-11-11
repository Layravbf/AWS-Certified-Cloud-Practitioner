# 01_O_IAM

Identity and Access Management → organizar os usuários que tem ou não acesso a plataforma da AWS por meio da definição de políticas de acesso à usuários/grupo de usuários/roles.

A partir da conta Root podemos criar usuários e habilitar acesso específicos para cada. Pode-se criar grupos de usuários (Admin, Developer) que faz sentido quando vários usuários terão o mesmo nível de acesso. Um usuário pode ser associado a mais de um grupo.

A criação de Roles está associada a serviços, dar acesso a uma máquina à acessar outros serviços dentro da plataforma.

# IAM Identity Center

Sucessor do AWS Single Sign-On (SSO)

Fazer com que vários serviços compartilhem de um mesmo usuário e mesma senha

IAM x Identity Center

IAM → criar usuários, grupos e roles com acesso a serviços dentro da plataforma

Identity Center → o mesmo do IAM além de poder associar a aplicações (por exemplo, o mesmo usuário que você acessa na aws você poderá acessar o seu provedor de email), ou seja, acesso à aplicações hospedadas pela sua empresa dentro da AWS

Para habilitar o Identity Center é necessário ter uma organização criada.

# MFA

Terceira camada de acesso à sua conta além do usuário e senha → é um código de 6 dígitos que atualiza a cada 30 segundos que está em seu telefone celular.

# Organizações

AWS Organizations → Seria como criar subcontas, por exemplo departamentos diferentes, clientes diferentes, projetos de sedes diferentes garantindo a conectividade pois se trata de uma única conta master e melhor gerenciamento de custos e políticas.

Características principais do AWS Organizations:
  

1. **Gerenciamento Centralizado de Contas**: O AWS Organizations permite agrupar e gerenciar todas as suas contas AWS de um único local centralizado. Isso facilita o gerenciamento de contas e recursos em uma organização.
    
2. **Controle de Acesso Hierárquico**: Com o AWS Organizations, você pode criar uma estrutura hierárquica de Unidades Organizacionais (OUs) para agrupar suas contas. Isso ajuda a organizar suas contas em uma estrutura que melhor se alinhe com o uso dos recursos em sua organização.
    
3. **Políticas de Controle de Serviço**: O AWS Organizations oferece políticas de controle de serviço (SCPs) que permitem que você controle as permissões para as contas em sua organização. Isso permite que você aplique regras de acesso uniformes em todas as suas contas.
    
4. **Consolidação de Cobrança**: O AWS Organizations também oferece a capacidade de consolidar sua cobrança em todas as suas contas AWS, o que pode simplificar a gestão de custos e permitir um melhor rastreamento e controle dos gastos da AWS.
    
5. **Automação**: Com o AWS Organizations, você pode automatizar a criação e o gerenciamento de contas por meio de APIs e integrações com outras ferramentas da AWS, como o AWS CloudFormation.
# CloudShell e CLI

CLI → fornece credenciais AWS a um software em seu computador(local) que te fornece uma linha de comando para executar scripts, acaba reduzindo muitos processos feitos manualmente na interface da aws

CloudShell → não é necessário instalar na sua máquina, ele nao é local, ele está na nuvem, é uma máquina linux que você consegue acessar todos os serviços sem precisar autenticar

