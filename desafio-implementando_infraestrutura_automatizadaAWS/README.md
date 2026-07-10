# Desafio: Implementando Infraestrutura Automatizada com AWS CloudFormation

*Nessa etapa do desafio, revisamos a importância da linguagem YAML e JSON, vimos como a linguagem YAML, embora seja uma forma mais simplificada e prática, tende a necessitar mais atenção, já que um parâmetro errado pode impedir a fluidez do processo.*

**Formato tradicional JSON:**
```
    {
        "Resources":{
            "MyInstance":{
                "Type":"AWS::EC2::Instance",
                "Properties":{
                    "InstanceType":"t2.micro",
                    "Imageld":"ami-12345678"
                }
            }
        }
    }

```

**Formato em YAML:**

```
     Resources
        MyInstance:
            Type: "AWS::EC2::Instance"
            Properties:
                InstanceType:"t2.micro"
                Imageld:"ami-12345678"

```

*Durante todo o processo de criação, foi mostrada a praticidade ao criar, gerenciar os acessos e supervisionar toda a infraestrutura do projeto através do AWS CloudFormation, demonstrando a importância desse aprendizado para aqueles que buscam entrar na área de tecnologia.*

*Porém, devemos destacar que, para dar certo, qualquer aplicação precisa também de um bom manuseio do utilizador, cuidados esses que impedem que o fluxo de trabalho seja interrompido.*


## Erros comuns e como resolvê-los:

---
- Erro: **YAML/JSON mal formatado**: vírgulas faltando, indentação incorreta ou chaves não fechadas.

    - **Atenção em**: Validar o template com aws cloudformation validate-template e usar linters/IDE com suporte a YAML/JSON.
---

- Erro: **Parâmetros inválidos**: Valores fora do tipo esperado (ex: string em vez de número).

    - **Atenção em**: Conferir tipos e valores esperados na documentação; usar AllowedValues e AllowedPattern para restringir entradas.
---

- Erro: **Dependências e Recursos**: Ordem incorreta de dependências: recursos que dependem de outros não declarados corretamente.

    - **Atenção em**: Revisar uso de DependsOn, Ref e GetAtt; garantir que não haja referências circulares.
---

- Erro: **Permissões e IAM - Políticas insuficientes**: O usuário não tem permissões para criar/alterar determinados recursos.

    - **Atenção em**: Ajustar políticas e roles; garantir que o usuário/role tenha permissões necessárias para criar/alterar recursos.
---

- Erro: **Região incorreta**: Tentar criar recursos em regiões onde não estão disponíveis.

    - **Atenção em**: Confirmar que os recursos estão disponíveis na região escolhida; ajustar Region no template.
---