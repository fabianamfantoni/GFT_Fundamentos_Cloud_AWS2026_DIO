# Desafio: Stack com AWS CloudFormation- Bootcamp DIO

*Durante esse estágio, desenvolvemos nossos conhecimentos sobre a implementação das Stacks na AWS CloudFormation.*

*Aprendemos sobre os processos de criação e manutenção de firewalls. Além de como operar as portas de acesso para não ter problemas na execução.*

## AWS CloudFormation

**Para aqueles que não conhecem:**

**O que é?**

---
*O AWS CloudFormation é um serviço da Amazon Web Services que permite automatizar a criação e gerenciamento de recursos na nuvem utilizando templates em JSON ou YAML.*

*Com ele, é possível definir toda a infraestrutura, garantindo consistência, repetibilidade e segurança na implantação de ambientes.*

---

**Utilidades:**

- Automação: elimina a necessidade de criar recursos manualmente.

- Infraestrutura como Código (IaC): toda configuração é versionável e documentada.

- Segurança: permite validar e revisar stacks antes da execução.

- Reprodutibilidade: ambientes podem ser recriados de forma idêntica em diferentes regiões ou contas.

## Bootcamp DIO.
*
*Durante o bootcamp, foram realizados exercícios que mostraram como:*

- Criar stacks (conjuntos de recursos) utilizando CloudFormation.

- Verificar a segurança das stacks, garantindo que portas e acessos estivessem corretamente configurados.

- Configurar instâncias EC2 com Apache e aplicar regras de firewall via Security Groups.

---
**Configurações Realizadas**

1.  Portas

- Configuração de Security Groups para liberar apenas portas necessárias, além de evitar conflitos de portas entre aplicações.

- Exemplo: liberar apenas a porta 80 (HTTP) para acesso público.

```

Resources:
  GrupoSeguranca:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Acesso Liberado Porta 80
      SecurityGroupIngress:
        IpProtocol: tcp
        FromPort: 80
        ToPort: 80
        CidrIp: 0.0.0.0/0

``` 
2.  Apache

- Instalação automática do servidor Apache via UserData.

- Configuração inicial para servir uma página HTML simples.

```

UserData:
  Fn::Base64: !Sub |
    #!/bin/bash -xe
    yum install -y httpd.x86_64
    systemctl start httpd.service
    systemctl enable httpd.service
    echo "<h1>Servidor Apache configurado com CloudFormation</h1>" > /var/www/html/index.html

``` 

3. Firewall

- Associação da instância EC2 ao Security Group configurado. Garantindo de que apenas tráfego autorizado (porta 80) fosse permitido.

``` 

Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-xxxxxxxx
      SecurityGroups:
        - Ref: GrupoSeguranca

```
---

*Em resumo, aprendemos a criar ambientes completos, automatizar serviços e configurar firewalls para garantir a segurança das aplicações. Embora pareça repetitivo, é essencial reforçar a atenção à segurança em projetos e dados, já que uma pequena falha pode desencadear uma "avalanche de erros" e comprometer todo o trabalho desenvolvido. Assim, aquilo que foi criado para agilizar processos pode acabar se transformando em seu maior obstáculo.*
