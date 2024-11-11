# 04_Armazenamento_EC2

## EBS (Elastic Block Store)

O Amazon EBS (Elastic Block Store) é um serviço de armazenamento em blocos oferecido pela AWS que permite que você crie volumes de armazenamento persistentes para uso com instâncias EC2. Esses volumes são duráveis e independentes das instâncias, o que significa que seus dados permanecem armazenados mesmo que a instância EC2 seja parada ou terminada.

Alguns pontos importantes sobre o EBS:

- **Persistência de dados**: Ao contrário do armazenamento local nas instâncias EC2, os volumes EBS mantêm os dados mesmo após o encerramento da instância.
- **Flexibilidade**: Você pode aumentar a capacidade ou ajustar o tipo de volume conforme necessário, sem perder dados.
- **Tipos de volume**: O EBS oferece diferentes tipos de volumes para atender a diferentes necessidades de desempenho, como o **gp3** (desempenho balanceado) e o **io2** (alta performance para workloads críticos).
- **Snapshots**: É possível criar snapshots (cópias) dos volumes EBS para backups ou migrações de dados.
- **Segurança**: O EBS oferece criptografia nativa para proteger os dados.

Os volumes EBS estão vinculados a uma **zona de disponibilidade (Availability Zone)** específica dentro da região AWS. Isso significa que o volume deve ser criado e usado na mesma zona de disponibilidade da instância EC2 à qual ele está anexado, garantindo uma conectividade de baixa latência e alta performance. Você não pode anexar um volume EBS diretamente a uma instância que esteja em outra zona de disponibilidade, mas é possível fazer backups (snapshots) e recriar o volume em outra zona, se necessário.

Essa restrição ajuda a garantir a **alta disponibilidade** e a **resiliência** dentro da zona, evitando a necessidade de replicação entre diferentes zonas, que pode adicionar latência.

## Valores e Tipos de EBS

### 1. **Volumes SSD (Solid State Drive)**

Esses volumes são otimizados para operações de leitura/escrita com alta frequência e baixa latência, como bancos de dados transacionais, sistemas de arquivos e aplicativos sensíveis ao desempenho. São mais rápidos e com menos espaço.

- **gp3 (General Purpose SSD)**:
    
    - **Uso**: Workloads gerais, como servidores web, bancos de dados pequenos e médios.
    - **Performance**: Até 16.000 IOPS e 1.000 MB/s de throughput.
    - **Custo**: Mais barato que o gp2, oferece performance previsível e customizável de IOPS sem depender do tamanho do volume.
- **io2 (Provisioned IOPS SSD)**:
    
    - **Uso**: Workloads críticos, como grandes bancos de dados e aplicações de baixa latência.
    - **Performance**: Até 500 IOPS por GiB, com um máximo de 256.000 IOPS.
    - **Custo**: Mais caro, mas oferece alta performance e durabilidade (99,999% de disponibilidade).

### 2. **Volumes HDD (Hard Disk Drive)**

Esses volumes são otimizados para cargas de trabalho sequenciais com grande volume de dados, como processamento em lote, data warehouses, e backup. São mais lentos e com mais espaço.

- **st1 (Throughput Optimized HDD)**:
    
    - **Uso**: Workloads intensivos de leitura sequencial, como análise de Big Data e ETL.
    - **Performance**: 500 MB/s de throughput máximo.
    - **Custo**: Mais barato que SSD, ideal para grandes volumes de dados acessados sequencialmente.
- **sc1 (Cold HDD)**:
    
    - **Uso**: Workloads de acesso esporádico e de baixo custo, como backups ou arquivos menos acessados.
    - **Performance**: Até 250 MB/s de throughput.
    - **Custo**: O mais barato entre os tipos de volumes EBS, mas com menor desempenho.

### Comparação de Custo e Performance:

- Volumes **gp3** e **gp2** são recomendados para cargas de trabalho gerais com um bom balanço entre custo e desempenho.
- **io2** é a opção mais cara, mas oferece a maior performance e é usada em aplicações críticas e bancos de dados de grande escala.
- Volumes HDD, como **st1** e **sc1**, são opções mais econômicas para armazenar grandes quantidades de dados com acessos esporádicos ou sequenciais.

### Fatores de Custo:

O custo do EBS varia com base em:

- **Tipo de volume** (SSD ou HDD).
- **Tamanho do volume** (medido em GiB).
- **Performance provisionada** (IOPS no caso de volumes io2).
- **Uso de snapshots** (backups incrementais podem gerar custos adicionais).

Esses preços são cobrados de acordo com o volume provisionado (tamanho em GiB), independentemente do uso real de dados.

## Snapshots

Os **snapshots** do Amazon EBS são cópias de backup dos volumes EBS que são armazenadas no Amazon S3 de maneira incremental e durável. Eles permitem criar um ponto de recuperação dos dados em um determinado momento, que pode ser usado para restaurar volumes ou replicar dados entre diferentes zonas de disponibilidade ou regiões.

### Características dos Snapshots:

1. **Backup Incremental**:
    
    - Apenas os blocos de dados que foram modificados desde o último snapshot são armazenados no próximo. Isso otimiza o uso de armazenamento e reduz o custo, já que você não está duplicando dados que não mudaram.
2. **Recuperação de Dados**:
    
    - Os snapshots podem ser usados para criar novos volumes EBS. Esse recurso é útil tanto para recuperação de desastres quanto para migração de dados entre zonas de disponibilidade ou regiões da AWS.
3. **Portabilidade entre Regiões**:
    
    - Embora os volumes EBS sejam restritos a uma zona de disponibilidade, os snapshots podem ser copiados para outras regiões AWS. Isso é útil para replicação geográfica e alta disponibilidade em cenários de desastre.
4. **Criação de Novos Volumes**:
    
    - Com base em um snapshot, você pode criar novos volumes EBS em qualquer zona de disponibilidade dentro de uma região, ou copiar o snapshot para outra região antes de criar o volume. O novo volume conterá todos os dados capturados no momento da criação do snapshot.
5. **Automação e Programação**:
    
    - Snapshots podem ser automatizados com **AWS Backup** ou scripts personalizados usando **AWS Lambda** e **Amazon CloudWatch**, o que ajuda a garantir backups regulares sem intervenção manual.
6. **Criptografia**:
    
    - Snapshots herdam a criptografia do volume original, se ele foi criptografado. Além disso, os snapshots podem ser copiados com a opção de criptografia habilitada ou desabilitada conforme necessário.

### Benefícios:

- **Resiliência e Disponibilidade**: Snapshots fornecem uma forma confiável de recuperar dados em caso de falha, corrupção ou exclusão acidental.
- **Eficiência de Custo**: A abordagem incremental garante que o armazenamento seja utilizado de forma eficiente, resultando em menores custos do que armazenar backups completos repetidamente.
- **Facilidade de Gestão**: Eles podem ser facilmente gerenciados e restaurados via AWS Management Console, CLI, ou APIs.

### Uso Típico:

- **Backup Regular**: Manter snapshots regulares de volumes de produção para garantir a recuperação em caso de falhas.
- **Migração e Replicação**: Usar snapshots para mover dados entre diferentes zonas de disponibilidade ou regiões.
- **Clonagem de Ambientes**: Criar volumes idênticos a partir de snapshots para testar ou clonar ambientes de desenvolvimento e produção.

Os snapshots são uma ferramenta essencial no AWS para garantir a segurança e a recuperação de dados, além de serem um recurso fundamental para migração e replicação de dados.

## AMI (Amazon Machine Image)

A **Amazon Machine Image (AMI)** é uma imagem pré-configurada que contém o software necessário para iniciar uma instância virtual no Amazon EC2 (Elastic Compute Cloud). Ela inclui o sistema operacional, bibliotecas, pacotes de software, configurações e, opcionalmente, dados de aplicação.

### Componentes da AMI:

1. **Sistema Operacional (OS)**: A AMI inclui uma cópia do sistema operacional que será executado na instância, como Linux, Windows ou qualquer outro sistema compatível com o EC2.
    
2. **Pacotes de Software**: Além do sistema operacional, a AMI pode conter softwares e pacotes adicionais, como servidores web, bancos de dados, ou qualquer aplicação específica que o usuário queira rodar nas instâncias.
    
3. **Configurações**: As AMIs podem incluir configurações personalizadas, como arquivos de configuração de rede ou software, que preparam a instância para um uso específico assim que ela for inicializada.

### Tipos de AMIs:

- **AMIs Públicas**: Criadas pela AWS ou pela comunidade e disponíveis para qualquer usuário. Por exemplo, AMIs oficiais da AWS incluem distribuições populares de Linux como Amazon Linux, Ubuntu, Red Hat, e versões do Windows Server.
    
- **AMIs Privadas**: Criadas por usuários e mantidas privadas, usadas apenas dentro da própria conta AWS. Elas são ideais para criar imagens personalizadas com configurações e software específicos para um projeto.
    
- **AMIs do AWS Marketplace**: Fornecedores terceiros podem criar e vender AMIs no AWS Marketplace, oferecendo soluções prontas para diversas necessidades, como segurança, gerenciamento de dados, ou desenvolvimento de software.

### Usos Comuns de AMIs:

1. **Iniciar Instâncias EC2**: Quando você lança uma instância EC2, deve escolher uma AMI como ponto de partida. A instância será inicializada com a configuração exata da AMI, incluindo sistema operacional, software e configurações.
    
2. **Replicar Ambientes**: Se você tem um ambiente configurado com softwares e pacotes específicos, pode criar uma AMI da instância atual e replicar esse ambiente facilmente ao iniciar novas instâncias a partir da AMI.
    
3. **Backup de Configurações**: As AMIs podem servir como uma cópia de backup de uma configuração de servidor bem-sucedida, facilitando a restauração ou clonagem do servidor.
    
4. **Automatização de Ambientes**: Em ambientes de desenvolvimento ou produção, as AMIs podem ser usadas para automatizar a criação de novos servidores já configurados com todas as dependências e software necessários.

### Criando uma AMI:

Você pode criar sua própria AMI a partir de uma instância EC2 em execução. Isso envolve:

1. **Personalizar a Instância**: Instalar e configurar o software desejado.
2. **Criar uma Imagem da Instância**: Usar o console do EC2 ou a CLI para criar a imagem, que captura o estado da instância naquele momento.
3. **Lançar Instâncias a Partir da AMI**: Uma vez criada, a AMI pode ser usada para iniciar novas instâncias com a mesma configuração.

### Vantagens das AMIs:

- **Consistência**: Garante que todas as instâncias iniciadas a partir de uma AMI tenham a mesma configuração e software.
- **Escalabilidade**: Facilita a criação de múltiplas instâncias rapidamente, o que é útil em arquiteturas de escalabilidade horizontal.
- **Recuperação Rápida**: Se você tiver uma AMI pronta, pode rapidamente restaurar um ambiente ou iniciar um novo servidor em caso de falhas ou problemas.

As AMIs são uma parte fundamental da infraestrutura AWS, pois permitem a criação de ambientes de computação altamente repetíveis e escaláveis.

## EFS (Elastic File System)

Criado para Linux

A principal diferença entre o **Amazon EBS (Elastic Block Store)** e o **Amazon EFS (Elastic File System)** está no tipo de armazenamento que cada serviço oferece, como ele é gerenciado e as situações em que são mais apropriados para uso. Aqui estão as principais distinções:

### 1. **Tipo de Armazenamento**:

- **Amazon EBS**: É um serviço de armazenamento em blocos (block storage). Cada volume EBS é anexado diretamente a uma única instância EC2, funcionando de forma semelhante a um disco rígido de uma máquina física. O EBS é ideal para armazenar dados persistentes e estruturados que exigem acesso de baixa latência, como sistemas de arquivos locais ou bancos de dados.
    
- **Amazon EFS**: É um serviço de armazenamento de arquivos (file storage), que oferece um sistema de arquivos distribuído acessível via protocolo NFS. O EFS pode ser montado por várias instâncias EC2 ao mesmo tempo, permitindo compartilhamento de dados entre instâncias e sendo mais adequado para casos onde múltiplos servidores precisam acessar os mesmos arquivos.

### 2. **Acesso Simultâneo**:

- **EBS**: Um volume EBS pode ser anexado a **apenas uma instância EC2 por vez** (com exceção de instâncias em modo multi-attach, que são limitadas a casos de uso específicos), o que significa que ele é mais adequado para cenários onde um único servidor precisa acessar os dados.
    
- **EFS**: Permite o **acesso simultâneo por múltiplas instâncias EC2** ou outros serviços, sendo ideal para aplicações distribuídas onde vários servidores precisam compartilhar os mesmos dados ao mesmo tempo.

### 3. **Escalabilidade**:

- **EBS**: A capacidade de armazenamento precisa ser provisionada manualmente. Quando você cria um volume EBS, define o tamanho e, se precisar de mais espaço, é necessário redimensionar o volume manualmente. Portanto, ele não se ajusta automaticamente conforme a necessidade de armazenamento aumenta ou diminui.
    
- **EFS**: É **elástico**, ajustando automaticamente o tamanho de acordo com a demanda, sem a necessidade de intervenção manual. O sistema de arquivos cresce e encolhe dinamicamente conforme os dados são adicionados ou removidos.

### 4. **Desempenho**:

- **EBS**: Oferece diferentes tipos de volumes (SSD e HDD) que variam em termos de IOPS e throughput, o que significa que você pode escolher o tipo de volume com base na necessidade de desempenho de sua aplicação. O desempenho do EBS é consistente e dedicado à instância à qual ele está conectado.
    
- **EFS**: É otimizado para fornecer acesso compartilhado e alta disponibilidade. Ele também oferece diferentes modos de performance (Standard e Max I/O) e diferentes níveis de armazenamento (Standard e Infrequent Access), mas seu desempenho pode variar com base no número de instâncias acessando o sistema de arquivos ao mesmo tempo.

### 5. **Use Cases (Casos de Uso)**:

- **EBS**: É mais adequado para aplicações que requerem armazenamento dedicado de baixa latência e que são executadas em uma única instância EC2, como bancos de dados, servidores de aplicações, ou sistemas de arquivos locais persistentes.
    
- **EFS**: É ideal para **aplicações distribuídas** ou de grande escala que exigem que várias instâncias EC2 compartilhem os mesmos dados, como sistemas de gerenciamento de conteúdo, servidores web com múltiplos backends, ou aplicativos de machine learning que precisam de acesso compartilhado aos mesmos datasets.

### 6. **Preços**:

- **EBS**: Você paga pela capacidade provisionada, mesmo que não esteja usando todo o espaço do volume. O custo é baseado no tipo de volume (gp3, io2, st1, sc1) e na quantidade de espaço provisionado.
    
- **EFS**: Cobra pelo espaço utilizado, ajustando-se automaticamente conforme os dados são adicionados ou removidos. Oferece dois níveis de armazenamento: **Standard** para dados acessados com frequência e **Infrequent Access (IA)** para dados acessados esporadicamente, com preços mais baixos para o IA.

### 7. **Disponibilidade e Durabilidade**:

- **EBS**: Cada volume EBS está restrito a uma **única zona de disponibilidade (AZ)**. Se você quiser alta disponibilidade entre diferentes zonas, é necessário criar snapshots do EBS e restaurá-los em outra zona ou região.
    
- **EFS**: É projetado para ser altamente disponível e durável, distribuindo automaticamente seus dados em várias zonas de disponibilidade dentro de uma região da AWS, sem a necessidade de gerenciamento adicional.

### Resumo:

- **EBS** é a escolha ideal quando você precisa de armazenamento persistente dedicado a uma única instância EC2, com baixa latência e controle sobre o desempenho.
- **EFS** é mais adequado para cenários em que múltiplas instâncias EC2 precisam acessar os mesmos arquivos ao mesmo tempo, com escalabilidade automática e alta disponibilidade distribuída.

## FSx 

O Amazon FSx é um serviço de armazenamento de arquivos totalmente gerenciado da AWS que facilita o lançamento e a execução de sistemas de arquivos de terceiros. O FSx fornece o rico conjunto de recursos e a rápida performance que esses tipos de aplicativos precisam, e atualmente suporta dois sistemas de arquivos: Windows File Server para aplicações baseadas em Windows, e Lustre para cargas de trabalho de computação intensiva.

Aqui estão alguns pontos chave sobre o Amazon FSx:

1. **FSx para Windows File Server**: Ele fornece um sistema de arquivos nativamente compatível com o Windows, permitindo que você mova com facilidade as aplicações baseadas em Windows que exigem o sistema de arquivos do Windows para a AWS. É construído sobre o Windows Server e oferece suporte a recursos como deduplicação de dados, criptografia de dados em repouso, e acesso via SMB (Server Message Block) e NFS (Network File System).
    
2. **FSx para Lustre**: O Lustre é um sistema de arquivos popular para cargas de trabalho de computação intensiva, como análise de big data, modelagem de machine learning e processamento de mídia. O FSx para Lustre é totalmente gerenciado pela AWS, simplificando o processo de criação e execução de um sistema de arquivos Lustre.
    
3. **Desempenho**: O Amazon FSx foi projetado para oferecer o desempenho rápido necessário para suportar aplicações exigentes. Ele fornece baixa latência e altas taxas de transferência de dados.
    
4. **Compatibilidade e Integração**: O Amazon FSx é totalmente compatível com os sistemas de arquivos que suporta, o que significa que você pode usar suas ferramentas e aplicações existentes sem modificação. Além disso, o FSx se integra com uma série de outros serviços AWS para coisas como backup, monitoramento e acesso seguro a arquivos.
    
5. **Segurança**: O Amazon FSx oferece várias funcionalidades de segurança, como a capacidade de armazenar dados em redes virtuais privadas da Amazon (VPCs), suporte a redes de acesso (ACLs) para o Windows File Server, criptografia de dados em repouso e em trânsito, e integração com AWS Key Management Service (KMS) para gerenciamento de chaves de criptografia.