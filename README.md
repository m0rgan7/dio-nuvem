# Resumo de Aprendizado sobre Computação em Nuvem

- A **nuvem também precisa de um data center**, o que me deixou curiosa, farei mais pesquisas para entender isso certinho, gosto de saber o por que das coisas. Mas entendi que ela depende de uma estrutura física para funcionar, o que faz sentido.

- É um modelo **baseado em custo por uso**: você (ou empresas) pagam conforme consomem os recursos, isso torna mais fácil prever os custos (que na maior parte dos casos só sao cobrados no outro mês, tipo cartão de crédito).

## Capex vs Opex

- **Capex**: são despesas de capital, como infraestrutura física. Essas despesas são altas no começo, mas se diminuem com o tempo (pois no inicio você gasta comprando os materiais, depois os custos são apenas para manter, que comparado com a obtenção dos materiais é muito menor).
  
- **Opex**: são despesas operacionais, como gastos com serviços e produtos. Você paga pelo que estiver ativo e por quanto tempo ficou ativo (se vc criou algo que ficou ativo só 7 dias, vc paga somente por esses 7 dias).

## Tipos de Nuvem

- Existem **nuvens públicas, privadas, híbridas e mistas**.
  
  - A **nuvem privada** é criada e mantida pela própria empresa. Ela mesma é responsável pela segurança e custos, sendo usada exclusivamente para suas operações. (acho que pode ser considerado o on-premises /que é basicamente quando todos os recursos de TI, tipo banco de dados, sistema e infraestrutura/ instalados dentro da propria empresa, sob total controle da organização)
  
  - A **nuvem pública** é oferecida por provedores (como AWS, Azure, etc), onde várias empresas usam os mesmos recursos compartilhados.
  
  - A **nuvem híbrida** mistura os dois tipos (pública e privada), e a empresa escolhe onde quer rodar cada parte da aplicação, aproveitando o melhor de cada uma.
  
  - A **nuvem mista**... bom, ainda fiquei em dúvida se ela realmente é diferente da híbrida. Aparentemente, na híbrida você tem os benefícios de ambas; na mista, você simplesmente usa as duas. Mas ainda parece bem parecido pra mim.

---


# Benefícios da Nuvem

## Contrato

Na nuvem, os recursos são disponibilizados com base em contrato de uso. Você paga apenas pelo que consome, com possibilidade de ajustar o ambiente conforme as necessidades do negócio e ser ressarcido caso algo fugir do acordo.


## Escalabilidade
Capacidade de **ajustar o ambiente** (aumentar ou diminuir) para atender à demanda. Exemplo: aumentar a capacidade do servidor durante horários de pico.

## Elasticidade
É a habilidade de **crescer ou reduzir recursos automaticamente**, mesmo sem previsão. Exemplo: em uma Black Friday, você não sabe exatamente quantos acessos terá, então o sistema se ajusta automaticamente.

## Confiabilidade
Serviços na nuvem são gerenciados por provedores confiáveis (como a Microsoft), o que garante **alta disponibilidade**. Caso ocorra alguma falha, é **mínima** e o sistema é rapidamente restabelecido.

## Previsibilidade
Refere-se à **confiança no desempenho e no comportamento esperado** do ambiente. Se um recurso sempre funcionou de um jeito estável, não há motivo para mudar — isso dá segurança operacional.

## Segurança
A nuvem oferece **plataformas e ferramentas de segurança**, mas a **responsabilidade de configuração é do usuário**. Manter os recursos atualizados e bem configurados é essencial.

## Governança
É a **gestão e controle sobre o ambiente**. Inclui definição de regras, políticas e autorizações, como **bloquear acessos indevidos** ou **controlar quem pode alterar recursos**.

## Gerenciabilidade
Você pode **gerenciar a nuvem de diversas formas**:
- Portal Azure (interface gráfica)
- PowerShell
- VS Code com extensões
- Terraform (infraestrutura como código)


## SLA – Service Level Agreement

O **SLA** define o **tempo máximo que um recurso pode ficar fora do ar** antes que a Microsoft tenha que compensar o cliente (contrato).

- Quanto **mais “noves” (%)** no SLA, **menor a chance de indisponibilidade**.
- **Mais disponibilidade = mais caro**, então o ideal é **escolher conforme a necessidade do cliente**.

| SLA (%)       | Tempo máximo de inatividade por mês |
|---------------|--------------------------------------|
| 99%           | ~7h18min                             |
| 99.9%         | ~43min                               |
| 99.99%        | ~4min                                |
| 99.999%       | ~26 segundos                         |

**iaas (instrutura como serviço) ->** nos envolvemos mais nessa parte e temos mais monitoramento e personalização desses serviços (todos são "problema seu")

**paas (plataforma como serviço) ->** tem o servidor e o banco de dados, você não se envolve ou se preocupa como servidor, apenas com a aplicação, vc deixa de ver o sistema operacional.

**saas (software como serviço) ->** depende da licença, a plataforma e serviços já existem, mas para acessar depende da licença nenhum é de sua responsabilidade pra criar e manter atualizado e monitorar.

---

# Componentes de arquitetura do azure

Regiões: não tem um valor tabelado, dependendo do país tem recursos e valores diferentes devido a taxações e etc, mas tem que avaliar se compensa pois quanto mais longe mais lento vai acabar ficando

tem os mesmos recursos em diferentes data centers, então se um cair tem outros funcionando, so ficam mais lentos. (zona de disponibilidade) (desaster recover)

baixa latência = alta performance
independente de onde a escrita tiver sendo feita tem que estar disponível em hora real para todos os data centers

zonas de disponibilidade são tipo os lugares que estão com os hardwares, mas se preparar pro caso de se cair, qual vai ser a consequência? vale a pena gastar mais pra ter mais uma zona de disponibilidade? tem outra forma também sem ser em outro data cneter, pode ser em uma "gaveta" diferente, vai ser um tema abordado mais a frente.

Pares de região: se vc configurar em uma e acontecer algo nela vc tem uma parecida (não necessariamente na mesma região física, mas sim no quesito capacidade mesmo), as vs essa troca é automática, mas depende do recurso que estiver usando.

a china tem uma diferente, ela é operada pela 21vianet.

Grupo de recursos: 

pra criar um rrecurso no azure vc nao pode deixar solto, entao vc tem que ter um local para localizar ele e as coisas que vierem em conjunto

eles podem ser movidos para diferentes grupos de recursos, mas so podem existir em mais de um grupo de recursos, tipo, eles podem ser movimentados entre diferentes e tals, mas nao podem ser como se fossem "duplicados", a mesma coisa em grupos diferentes.

assinaturas: uma conta pode ter diversas assinaturas mas uma assinatura so ta associada a uma conta (tipo, vc pode ter quantas casas quiser, mas elas todas vao estar e ter apenas seu nome)

ai entra a questão do controle de cobrança. que vai gerar separados para cada assinatura e necessidade, além do controle de acesso por uma questão de segurança

grupos de gerenciamento: as mesmas regras são dadas as assinaturas que tiverem la dentro
