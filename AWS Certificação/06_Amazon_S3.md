# 06_Amazon_S3

- **Amazon S3 (Simple Storage Service)**: Um serviço de armazenamento de objetos que oferece armazenamento ilimitado na nuvem.

- **Limite de tamanho de objetos**: O tamanho máximo de um objeto que pode ser armazenado no S3 é 5 TB.

- **Multi-part upload**: Objetos maiores que 5 GB devem ser enviados utilizando o recurso de **multi-part upload**, que permite fazer o upload do objeto em partes menores

## Classes

### 1. **S3 Standard**

- **Descrição**: Classe padrão, ideal para dados acessados com frequência.
- **Uso**: Recomendado para dados de acesso frequente, como sites, aplicativos móveis, conteúdo dinâmico, backups ou análises de dados.
- **Durabilidade e Disponibilidade**: Alta durabilidade (99,999999999% - 11 noves) e disponibilidade de 99,99%.
- **Custo**: Mais cara comparada às outras classes de armazenamento.

### 2. **S3 Intelligent-Tiering**

- **Descrição**: Ajusta automaticamente o armazenamento entre níveis de acesso frequente e infrequente, com base nos padrões de uso.
- **Uso**: Ideal para dados com padrões de acesso variáveis ou desconhecidos.
- **Durabilidade e Disponibilidade**: Mesma durabilidade e disponibilidade da classe Standard.
- **Custo**: Varia conforme o uso, otimizando custos automaticamente.

### 3. **S3 Standard-IA (Infrequent Access)**

- **Descrição**: Armazenamento para dados acessados com menos frequência, mas que ainda precisam estar rapidamente disponíveis quando necessário.
- **Uso**: Adequado para backups, dados de recuperação de desastres ou qualquer dado que seja acessado esporadicamente.
- **Durabilidade e Disponibilidade**: Durabilidade de 11 noves e disponibilidade de 99,9%.
- **Custo**: Mais barato que o S3 Standard, mas cobra por recuperação de dados.

### 4. **S3 One Zone-IA**

- **Descrição**: Armazenamento para dados infrequentes em uma única zona de disponibilidade (AZ).
- **Uso**: Para dados que podem ser facilmente recriados em caso de perda de uma zona de disponibilidade, como backups secundários.
- **Durabilidade e Disponibilidade**: Durabilidade de 11 noves, mas com menor disponibilidade de 99,5%.
- **Custo**: Mais barato que o Standard-IA, com risco maior, já que está armazenado em uma única AZ.

### 5. **S3 Glacier**

- **Descrição**: Armazenamento de baixo custo para arquivamento de dados que raramente precisam ser acessados, com tempos de recuperação variando de minutos a horas.
- **Uso**: Ideal para arquivamento de longo prazo e dados que não precisam de acesso frequente.
- **Durabilidade e Disponibilidade**: Durabilidade de 11 noves, com disponibilidade ajustada conforme a necessidade de recuperação.
- **Custo**: Extremamente baixo custo de armazenamento, com cobrança por recuperação de dados.

### 6. **S3 Glacier Deep Archive**

- **Descrição**: Classe de armazenamento mais barata, voltada para arquivamento de longo prazo com tempos de recuperação mais lentos (de 12 a 48 horas).
- **Uso**: Ideal para dados que raramente ou nunca serão acessados, mas que precisam ser mantidos por questões de conformidade.
- **Durabilidade e Disponibilidade**: Durabilidade de 11 noves.
- **Custo**: A opção mais econômica, com alta latência para recuperação de dados.

## Versionamento

### 1. **Habilitando o Versionamento**

- O versionamento deve ser ativado em nível de bucket. Isso é feito por meio do console do S3, da CLI da AWS ou usando o SDK.
- Quando o versionamento está **habilitado** em um bucket, cada vez que um objeto é alterado ou sobrescrito, o S3 cria uma nova versão desse objeto em vez de substituir a versão anterior.

### 2. **Como o Versionamento Funciona**

- **Novos objetos**: Quando você coloca um novo objeto em um bucket com versionamento habilitado, ele recebe um **ID de versão único**. Se você fizer upload do mesmo objeto novamente, o S3 armazenará a nova cópia com um novo ID de versão.
- **Múltiplas versões**: O S3 mantém **todas as versões** de um objeto. Isso significa que, se um objeto for atualizado várias vezes, todas essas versões serão preservadas.
- **Recuperação de versões anteriores**: Você pode restaurar versões antigas de um objeto a qualquer momento, especificando o ID da versão que deseja recuperar.

### 3. **Exclusão de Objetos com Versionamento**

- **Soft Delete**: Quando você "exclui" um objeto em um bucket com versionamento habilitado, o S3 não remove o objeto permanentemente. Em vez disso, ele coloca um **marcador de exclusão**. As versões anteriores ainda estarão acessíveis, a menos que você exclua explicitamente cada versão.
- **Exclusão de versões específicas**: Se você quiser remover uma versão específica de um objeto, deve fornecer o ID da versão exata que deseja excluir. Somente essa versão será removida, enquanto outras versões continuarão no bucket.

### 4. **Casos de Uso do Versionamento**

- **Proteção contra exclusões acidentais**: Mesmo se um usuário ou processo tentar excluir um arquivo por engano, as versões antigas estarão disponíveis para recuperação.
- **Controle de versões de arquivos**: Útil em cenários de desenvolvimento ou colaboração, onde diferentes versões de um arquivo precisam ser mantidas.
- **Recuperação de desastres**: Em caso de corrupção de dados ou perda de arquivos importantes, é possível restaurar versões anteriores.

### 5. **Custos Relacionados ao Versionamento**

- Como o versionamento armazena **todas as versões** de um objeto, o espaço utilizado pode aumentar rapidamente, o que também afeta o custo de armazenamento.
- Para gerenciar custos, é possível usar **regras de ciclo de vida** (Lifecycle Rules) para configurar a exclusão automática de versões antigas ou mover versões mais antigas para classes de armazenamento de menor custo, como o S3 Glacier.

### Exemplo de Operação:

- Você faz upload de um arquivo chamado `relatorio.pdf` no S3 e habilita o versionamento.
- A primeira vez que o arquivo é carregado, ele recebe uma **ID de versão**, por exemplo, `V1`.
- Após algumas edições no arquivo, você faz upload de uma nova versão do `relatorio.pdf`, que recebe o ID de versão `V2`.
- Se precisar recuperar a versão original, basta acessar o arquivo com o ID de versão `V1`.
- Se alguém excluir o arquivo, o S3 irá adicionar um **marcador de exclusão**, mas você ainda poderá recuperar qualquer versão anterior.

## Replicação

### 1. **SRR (Same-Region Replication)**

- **O que é?**: O SRR permite replicar dados entre dois buckets **dentro da mesma região** da AWS.
- **Finalidade**: SRR é útil em casos onde você deseja manter cópias dos dados em diferentes buckets por motivos de **conformidade, backups** ou para **separação lógica** de dados entre diferentes equipes ou aplicativos na mesma região (produção e desenvolvimento).
- **Casos de uso**:
    - **Conformidade**: Manter cópias de dados em buckets separados para atender a requisitos regulatórios.
    - **Backup**: Criar uma cópia de segurança dos dados para recuperação em caso de falha do bucket principal.
    - **Separação de dados**: Segregar dados para diferentes ambientes (produção, desenvolvimento) ou departamentos.
- **Funcionamento**:
    - Após a configuração do SRR, qualquer objeto novo ou atualizado no bucket de origem será replicado automaticamente para o bucket de destino na mesma região.
    - **Permissões**: Você precisa configurar permissões de replicação, incluindo políticas de bucket e permissões do IAM, para permitir que o S3 realize essa operação.

### 2. **CRR (Cross-Region Replication)**

- **O que é?**: O CRR permite replicar dados de um bucket em uma **região da AWS** para um bucket em **outra região da AWS**.
- **Finalidade**: CRR é usado para garantir **resiliência geográfica** e para atender a requisitos de **latência**, **conformidade** ou **recuperação de desastres**.
- **Casos de uso**:
    - **Resiliência geográfica**: Criar cópias de dados em regiões diferentes para proteção contra falhas regionais.
    - **Redução de latência**: Melhorar a entrega de dados ao manter cópias próximas aos usuários finais em diferentes regiões.
    - **Conformidade**: Atender a regulamentos que exigem armazenamento de dados em regiões específicas.
    - **Recuperação de desastres**: Manter uma cópia em uma região separada como parte de um plano de recuperação de desastres.
- **Funcionamento**:
    - Assim como no SRR, após a configuração do CRR, qualquer objeto criado ou atualizado no bucket de origem será replicado automaticamente para o bucket de destino, mas **em uma região diferente**.
    - **Permissões**: Requer configuração adequada de permissões, similar ao SRR, mas inclui permissões entre buckets em diferentes regiões.

### Como SRR e CRR Funcionam:

- Ambos os recursos exigem que o **versionamento esteja habilitado** tanto no bucket de origem quanto no bucket de destino.
- A replicação ocorre para **novos objetos** e **atualizações de objetos** no bucket de origem após a configuração. Objetos já existentes antes da replicação ser configurada não são replicados automaticamente.
- Você pode configurar **filtros** para replicar somente objetos com um prefixo específico ou com determinadas tags.
- A replicação é assíncrona, ou seja, a cópia do objeto pode não aparecer imediatamente no bucket de destino após o upload no bucket de origem.

### Diferença Principal:

- **SRR (Same-Region Replication)** replica dados **dentro da mesma região**, enquanto **CRR (Cross-Region Replication)** replica dados **entre diferentes regiões**.
- **SRR** é mais adequado para backups, separação de dados e conformidade dentro da mesma região, enquanto **CRR** é mais usado para recuperação de desastres, conformidade entre regiões e redução de latência para usuários distribuídos globalmente.

### Considerações de Custos:

- Ambos SRR e CRR têm custos associados, que incluem:
    - **Custos de armazenamento** no bucket de destino (os dados replicados são cobrados como armazenamento adicional).
    - **Custos de transferência de dados** para CRR, já que os dados são transferidos entre regiões.
    - Custos adicionais para **operações de replicação**.

## AWS Snow Family

A **AWS Snow Family** é uma série de dispositivos físicos oferecidos pela Amazon Web Services (AWS) para mover grandes quantidades de dados entre suas instalações locais e a nuvem da AWS de forma segura e eficiente. Ela é especialmente útil quando a transferência via internet ou redes dedicadas é muito lenta, cara ou inviável devido ao volume de dados ou limitações de conectividade. A Snow Family inclui os dispositivos **Snowcone**, **Snowball** e **Snowmobile**, cada um com características e capacidades diferentes.

### 1. **AWS Snowcone**

- **Descrição**: O Snowcone é o menor e mais portátil dispositivo da família, pesando cerca de 2,1 kg. Ele é usado para transferências de dados menores ou em locais com pouca conectividade.
- **Capacidade**: Ele pode armazenar até **8 TB de dados utilizáveis**.
- **Casos de uso**:
    - Transferência de dados em ambientes desafiadores ou remotos, como navios, áreas de mineração, ou locais de guerra.
    - Coleta de dados de campo e transporte físico dos dados para a AWS.
- **Características**:
    - Suporta transferência offline e sincronização com o AWS Storage Gateway para migração de dados quando a conectividade for limitada.
    - Possui opções de alimentação via USB, o que o torna ideal para ambientes sem infraestrutura elétrica estável.

### 2. **AWS Snowball (Snowball Edge)**

- **Descrição**: O Snowball é um dispositivo de médio porte da família, ideal para transferências maiores de dados. Ele vem em duas variantes: **Snowball Edge Storage Optimized** e **Snowball Edge Compute Optimized**.
- **Capacidades**:
    - **Snowball Edge Storage Optimized**: Aproximadamente **80 TB de armazenamento utilizável** para transferências de dados em larga escala.
    - **Snowball Edge Compute Optimized**: Aproximadamente **42 TB de armazenamento**, com poder computacional adicional (incluindo GPUs opcionais) para executar tarefas de processamento e análise localmente antes de transferir os dados.
- **Casos de uso**:
    - Migração de grandes volumes de dados de datacenters para a AWS.
    - Coleta de dados em áreas remotas e processamento local antes da transferência.
    - Transferência de backups de grandes volumes.
- **Características**:
    - Equipado com funcionalidades de computação que permitem rodar **AWS Lambda** e **Amazon EC2** no próprio dispositivo.
    - Segurança robusta com criptografia de dados e proteção física do dispositivo.

### 3. **AWS Snowmobile**

- **Descrição**: O Snowmobile é o maior dispositivo da AWS Snow Family, literalmente um **caminhão** que pode armazenar **exabytes** de dados. Ele é usado para transferir volumes massivos de dados de forma física.
- **Capacidade**: Cada Snowmobile pode transportar até **100 petabytes** de dados.
- **Casos de uso**:
    - Migração massiva de datacenters inteiros para a AWS.
    - Grandes migrações que são inviáveis por meio de transferência online.
    - Transferências para setores como mídia e entretenimento, que lidam com enormes volumes de dados de vídeo.
- **Características**:
    - O Snowmobile é um contêiner de 12 metros com medidas de segurança de nível militar, incluindo vigilância 24/7, monitoramento GPS e escolta armada, dependendo da necessidade.
    - Ideal para migrações de empresas que possuem muitos petabytes ou mesmo exabytes de dados.

### Principais Vantagens da AWS Snow Family:

1. **Transferência Rápida e Segura de Dados**:
    
    - A Snow Family permite a movimentação de grandes volumes de dados de forma física, eliminando limitações de conectividade à internet ou banda larga. Todos os dados são **criptografados** com chaves de criptografia gerenciadas pelo cliente por meio do AWS Key Management Service (KMS), garantindo a segurança dos dados durante o transporte.
2. **Redução de Custos**:
    
    - Quando comparado ao custo de fazer grandes transferências de dados pela internet (com base no volume de dados ou tempo necessário), a AWS Snow Family pode ser mais econômica, especialmente para locais com largura de banda limitada ou altas tarifas de transferência.
3. **Capacidade de Computação Local**:
    
    - Dispositivos como o **Snowball Edge** oferecem a possibilidade de processar dados no local, antes mesmo de transferi-los para a AWS, economizando largura de banda e agilizando processos, como análise de dados de sensores, IoT ou outras aplicações em locais remotos.
4. **Facilidade de Uso**:
    
    - A AWS entrega o dispositivo físico no local indicado, você carrega os dados no dispositivo, e depois ele é enviado de volta para AWS, onde os dados são automaticamente carregados para o Amazon S3 ou outro serviço de armazenamento configurado.
5. **Alta Escalabilidade**:
    
    - De pequenos volumes com o **Snowcone** a datacenters inteiros com o **Snowmobile**, a AWS Snow Family cobre uma ampla gama de necessidades de transferência de dados.

### Quando Utilizar a AWS Snow Family?

- Quando há necessidade de mover grandes volumes de dados para a AWS rapidamente, mas a conectividade com a internet é insuficiente para uma transferência eficiente.
- Para realizar backups em massa, migração de datacenters, ou em situações onde a segurança e o tempo de transferência são críticos.
- Para implementar soluções em locais remotos e desafiadores com pouca ou nenhuma conectividade com a internet, como estações de pesquisa, plataformas de petróleo, ou navios.