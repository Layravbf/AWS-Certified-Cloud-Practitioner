# 07_Banco_de_Dados

## Amazon RDS

O **Amazon RDS (Relational Database Service)** é um serviço gerenciado da AWS que facilita a configuração, operação e escalabilidade de bancos de dados relacionais na nuvem. Ele automatiza tarefas comuns de gerenciamento de bancos de dados, como backups, aplicação de patches, monitoramento e provisionamento de hardware, permitindo que os usuários se concentrem mais no desenvolvimento de aplicações e menos na administração de bancos de dados.

O RDS oferece suporte a vários motores de banco de dados populares, incluindo:

- **Amazon Aurora** (compatível com MySQL e PostgreSQL)
- **MySQL**
- **MariaDB**
- **PostgreSQL**
- **Oracle**
- **Microsoft SQL Server**

## ElastiCache

O **Amazon ElastiCache** é um serviço gerenciado da AWS que facilita a implantação, operação e escalabilidade de caches na memória na nuvem. Ele é usado para aumentar o desempenho de aplicações, especialmente em cenários que exigem alta performance e baixa latência. O ElastiCache permite armazenar dados frequentemente acessados em memória, o que reduz a carga em bancos de dados subjacentes e melhora a rapidez de recuperação de dados.

O ElastiCache oferece suporte a dois mecanismos de cache populares:

### 1. **Redis**

- **O que é?**: Redis é um sistema de armazenamento em cache de dados na memória de código aberto que oferece recursos avançados, como persistência de dados, replicação, scripts Lua, transações e suporte a estruturas de dados mais complexas (listas, hashes, sets, etc.).
- **Casos de uso**:
    - Armazenamento de sessões de usuário em aplicações web.
    - Filas de mensagens ou publicação/assinatura (pub/sub).
    - Cache de dados frequentemente acessados para reduzir consultas a bancos de dados.
    - Contadores em tempo real e classificação (leaderboards) em jogos.
    - Análise em tempo real.
    - Uso de Redis como um banco de dados NoSQL em memória.
- **Benefícios**:
    - **Alta disponibilidade** com replicação.
    - **Failover automático** com Redis Cluster.
    - **Escalabilidade** horizontal com particionamento de dados (sharding).

### 2. **Memcached**

- **O que é?**: Memcached é outro sistema de cache de código aberto, conhecido por ser simples e voltado apenas para caching de dados, sem suporte a persistência ou funcionalidades avançadas como as do Redis.
- **Casos de uso**:
    - Cache de resultados de consultas a bancos de dados.
    - Armazenamento de fragmentos de páginas para sites dinâmicos.
    - Melhorar a resposta de APIs ou consultas em aplicações que fazem uso pesado de bancos de dados.
- **Benefícios**:
    - Simplicidade e velocidade para cenários de cache puro.
    - **Escalabilidade** horizontal através da adição de nós.

## DynamoDB

Banco não relacional

O **Amazon DynamoDB** é um serviço de banco de dados NoSQL totalmente gerenciado pela AWS, que oferece alta escalabilidade, desempenho rápido e baixa latência. Ele foi projetado para atender às necessidades de aplicativos que exigem grandes volumes de dados e alto desempenho de leitura e escrita, tudo isso sem que os desenvolvedores precisem se preocupar com a administração de infraestrutura, como configuração de servidores ou manutenção de software. É serverless, ou seja, não utiliza servidores.

## Amazon Neptune

O **Amazon Neptune** é um serviço de banco de dados grafo totalmente gerenciado pela AWS, projetado para aplicações que exigem armazenamento e consulta de dados em forma de grafos. Ele oferece suporte a dois modelos principais de grafos: **Property Graph** e **RDF (Resource Description Framework)**, permitindo trabalhar com relações complexas e conexões entre dados de forma eficiente.

### Casos de Uso:

- **Redes Sociais**: Armazenar e analisar conexões entre usuários, amigos e interações.
- **Recomendações**: Explorar relações entre produtos, usuários e preferências para oferecer recomendações personalizadas.
- **Grafos de Conhecimento**: Construir sistemas que capturam conhecimento interligado em áreas como ciência, finanças ou mídia.

## Amazon Glue

O **Amazon Glue** é um serviço de integração de dados totalmente gerenciado pela AWS que facilita a preparação, transformação e movimentação de dados para análises e machine learning. Ele automatiza muitas tarefas de ETL (Extract, Transform, Load), permitindo que você extraia dados de diferentes fontes, transforme-os conforme necessário e carregue-os em destinos como data lakes ou data warehouses.

### Casos de Uso:

- **ETL para Data Lakes**: Extração de dados de várias fontes, transformação e carregamento em data lakes como o **Amazon S3** para análise.
- **Migração de Dados**: Automatizar a migração de dados de sistemas legados para novos sistemas ou data warehouses.
- **Análise de Dados em Tempo Real**: Usar Glue para preparar e transformar dados antes de analisá-los com ferramentas como **Amazon Athena** ou **Redshift**.