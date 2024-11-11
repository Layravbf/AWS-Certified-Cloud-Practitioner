# 09_Content_Delivery

Serviço de DNS da AWS (faz a tradução de URL para endereçamento IP)

- **Gerenciamento de Domínios**: O Route 53 permite registrar novos domínios e gerenciar domínios existentes, incluindo a configuração de registros DNS.
    
- **Serviço de DNS**: Oferece resolução de nomes para serviços na AWS e fora dela. Os registros DNS suportados incluem A (endereço IPv4), AAAA (endereço IPv6), CNAME (nome canônico), MX (Mail Exchange), entre outros.
    
- **Health Checks**: Permite monitorar a saúde de recursos, como servidores web. Se um recurso falhar, o Route 53 pode redirecionar o tráfego para outro recurso saudável.
    
- **Routing Policies**:
    
    - **Simple Routing**: Direciona o tráfego para um único recurso.
    - **Weighted Routing**: Distribui o tráfego com base em pesos definidos, útil para testes A/B.
    - **Latency-based Routing**: Direciona o tráfego para a região com a menor latência.
    - **Geo DNS**: Roteia com base na localização geográfica do usuário.
    - **Failover Routing**: Redireciona o tráfego em caso de falha de um recurso.
- **Integração com outros serviços AWS**: O Route 53 se integra com serviços como Amazon S3, CloudFront, Elastic Load Balancing (ELB) e outros, facilitando a configuração de DNS para aplicações na AWS.
    
- **Escalabilidade e Disponibilidade**: O Route 53 é projetado para ser altamente disponível e escalável, suportando grandes volumes de tráfego.

### AWS Cloud Front

o Amazon CloudFront é uma solução de CDN segura, escalável e de alto desempenho que melhora a experiência do usuário, acelerando a entrega de conteúdo, enquanto protege seus aplicativos contra ameaças.
### S3 Transfer Acceleration

o S3 Transfer Acceleration é uma solução eficiente quando se precisa transferir grandes volumes de dados por longas distâncias. Ele maximiza a velocidade de transferência de dados, melhorando o desempenho e a eficiência das operações de negócios que envolvem o S3.

### AWS Global Accelerator

o AWS Global Accelerator é uma solução útil para melhorar a velocidade, a disponibilidade e a segurança de aplicações na AWS, proporcionando uma experiência de usuário mais suave e agradável.