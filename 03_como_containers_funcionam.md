# **Como containers funcionam**

Nesta aula, vamos responder algumas perguntas sobre como funcionam os containers.

- **Por que são mais leves?**
- **Como garantem o isolamento?**
- **Como funcionam sem `instalar um Sistema Operacional`?**
- **Como fica a divisão de recursos do sistema?**

## Transcrição

[00:00] Vamos responder às perguntas: por que os containers são mais leves em relação a uma máquina virtual? O que muda no fim das contas?

[00:08] O container funciona da seguinte maneira: dentro do nosso sistema operacional nós temos diversos containers, diversas aplicações que estarão sendo executadas no nosso sistema operacional. Só que no fim das contas eles vão funcionar diretamente como processos dentro do nosso sistema.

[00:26] Enquanto uma máquina virtual terá toda aquela etapa de virtualização dos sistemas operacionais, dentro do nosso sistema original, os containers vão funcionar diretamente como processos dentro do nosso sistema.

[00:38] Então a grosso modo, conseguimos visualizar como o consumo de recursos, a carga para que ele consiga ser executado é um pouco menor. Porque eles serão processos, e não uma virtualização completa.

[00:53] Mas como o processo vai conseguir garantir isolamento, como é que vai funcionar sem instalar o sistema? Como vamos conseguir resolver e responder a essas perguntas?

[01:04] A outra questão é que quando os nossos containers estiverem em execução dentro do nosso sistema operacional, a fim de garantir o isolamento entre cada um deles e o nosso sistema operacional original, existe um conceito chamado namespace, que vai garantir que cada um desses containers tenha a capacidade de se isolar em determinados níveis.

[01:25] Mas que níveis são esses? Nós teremos os principais namespaces, que são os de PID, que garantem o isolamento a nível de processo dentro de cada um dos containers. Então um processo dentro de um container, que consequentemente é um processo dentro do nosso sistema operacional, vai estar isolado de todos os outros do nosso host, da nossa máquina original.

[01:46] Nós teremos o NET também, o namespace de rede, que vai garantir o isolamento entre uma interface de rede de cada um dos containers e também do nosso sistema operacional original.

[01:56] O de IPC, que vai ser de intercomunicação entre cada um dos processos da nossa máquina.

[02:01] O de MNT, que é da parte de files system, sistema de arquivos, montagem, volumes e afins. Também estará devidamente isolado.

[02:09] E o de UTS, que faz um compartilhamento, um isolamento ao mesmo tempo também, de host do nosso Kernel da máquina que está escutando o container.

[02:19] Esse último em específico, o UTS, ajuda a responder até a próxima pergunta, que é como o container dentro do nosso sistema operacional vai funcionar sem um sistema operacional?

[02:32] Porque na verdade graças ao namespace de UTS, se estivermos executando os nossos containers, por exemplo, em uma máquina que tem o Kernel Linux, cada um desses containers a princípio também vai ter um pedaço desse Kernel, só que devidamente isolado.

[02:49] Então conseguimos já responder a essa pergunta. Nós não precisamos necessariamente instalar um sistema operacional dentro de um container porque ele já vai ter, graças a esse namespace de UTS, também esse acesso ao Kernel do sistema original, só que isoladamente.

[03:06] E por fim, também na parte de gerenciamento de recursos, vamos dizer que queremos definir o que levantamos no problema anteriormente, de definir o consumo máximo de memória, de CPU e afins para cada um dos nossos containers.

[03:18] Existe um outro conceito que se chama “Cgroups”, que vai garantir que consigamos definir tanto de maneira automática quando de maneira manual como os consumos serão feitos para cada um desses containers dentro do nosso sistema operacional.

[03:33] Então no fim das contas, voltando às nossas perguntas originais, graças aos namespaces e aos Cgroups nós conseguimos garantir isolamento, conseguimos garantir que nosso container funcione sem instalar um sistema operacional dentro dele, e também conseguiremos ter um controle de gerenciamento de recursos, como memória de CPU.

[03:55] Sobre a parte de porque eles são mais leves, nós vimos que eles funcionam como processos diretamente do nosso sistema operacional, mas no decorrer desse curso vamos entender ainda mais porque eles conseguem ser tão mais práticos em relação à maquina virtual a nível de consumo de recurso e de tamanho de armazenamento no nosso sistema operacional.

[04:14] Nós respondemos as principais perguntas de quem está começando agora no mundo de containers sobre como vai garantir isolamento, como ele funciona sem instalar um sistema operacional e afins.

[04:25] Agora que entendemos como um container se diferencia de uma máquina virtual tradicional, veremos como instalar o Docker, inicialmente no Windows e depois também no Linux, que vai ser onde abordaremos as principais utilizações do Docker.
