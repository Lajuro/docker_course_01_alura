# **Conhecendo o Problema [Transcrição]**

[00:00] Vamos partir do nosso problema inicial. Os sistemas atualmente têm diversas aplicações e ferramentas que interagem entre si para compor o todo desse sistema. E é mais ou menos esse caso que vamos visualizar nesse curso e entender porque os containers vão nos ajudar nessas situações. Mas antes vamos partir bem do básico da ideia de porque vamos chegar nessa solução.

[00:22] Nós teremos uma aplicação Nginx, que vai servir como um load balancer do nosso sistema. Temos uma aplicação Java e também uma aplicação C# rodando com o .NET.

[00:33] Isso é para ilustrar a nossa situação. E como queremos que todas essas aplicações estejam em execução para que o nosso sistema como um todo esteja ok, nós precisamos de uma máquina para que essas aplicações e, consequentemente, o nosso sistema estejam rodando.

[00:48] A nossa aplicação C# está rodando na porta 80, ela precisa da porta 80 para executar. A nossa aplicação Java também, assim como o Nginx. O C# estamos utilizando na versão 9, o Java na versão 17 e o Nginx na versão 1.17.0.

[01:05] E quais possíveis problemas podem ocorrer nessa situação? Se formos observar cada uma dessas aplicações e ferramentas, podemos acabar tendo um conflito de portas, porque as três aplicações desse cenário dependem da porta 80 para executar o fluxo que elas precisam.

[01:24] Além disso, como é que podemos alterar as versões de maneira prática? Será que se eu simplesmente fizer um downgrade ou um upgrade da versão do C#, atualizando meu .NET, eu vou quebrar alguma coisa? Será que eu preciso desinstalar para instalar uma nova?

[01:37] A mesma coisa para o Java e para o Nginx: será que eu vou conseguir atualizar de maneira prática?

[01:45] E outra questão é como teremos um controle de recursos de memória e de CPU para essas aplicações? Eu quero que, por exemplo, a minha aplicação C# precise de 100 milicores de CPU e 200 MB de memória para funcionar. Como é que eu posso definir isso de maneira fácil?

[02:00] A mesma coisa para as minhas outras aplicações. Como eu posso fazer essa definição de consumo de recursos desse sistema de maneira prática? É uma questão que precisamos levantar.

[02:09] E por fim, juntando todos esses problemas de uma vez só, como é que podemos fazer o processo de manutenção dessas aplicações? Como conseguiremos mudar a versão? Como conseguiremos ter esse controle sobre as portas da nossa aplicação, gerenciar os recursos e manter isso no longo prazo?

[02:28] Então uma solução que poderíamos pensar inicialmente e que seria bem simples, mas ao mesmo tempo problemática, e nós veremos o porquê, seria simplesmente comprarmos uma máquina para cada aplicação.

[02:40] Teremos uma máquina para nossa aplicação .NET, uma máquina para nossa aplicação Java e uma máquina para nossa aplicação Nginx.

[02:48] Assim nós temos o problema resolvido do conflito de portas. Cada máquina teria sua respectiva porta 80.

[02:55] Conseguiríamos controlar os recursos de maneira mais fácil, porque não teria essa dependência das aplicações entre si.

[03:01] E também faríamos o controle do versionamento um pouco mais facilmente, porque não teria diversas aplicações num mesmo sistema.

[03:10] Qual o problema disso? A questão é que o nosso dinheiro vai para o ralo, porque se temos uma máquina para cada aplicação, vamos pensar que tem sistemas com milhares ou milhões de aplicações executadas ao mesmo tempo. Então imagine ter milhares ou milhões de máquinas para que o seu sistema esteja operante. O dinheiro vai embora.

[03:31] Então existe uma solução já bem difundida, ela não foi criada agora, já é até razoavelmente antiga, que nos ajuda nesse tipo de problema, que são as máquinas virtuais, onde teremos nosso hardware bem definido, um sistema operacional, seja Windows, Linux, Mac e afins.

[03:51] E teremos também uma camada de hypervisor, que vai fazer um meio de campo entre virtualizar um novo sistema operacional, que pode ser um Windows, um Linux, um Mac, rodando dentro de outro sistema. Mas graças a essa camada de hypervisor nós teremos uma camada de isolamento desse sistema operacional original.

[04:10] E conseguiremos instalar nossas dependências e aplicações de maneira isolada, porque cada uma delas terá seu respectivo sistema operacional.

[04:19] É uma questão que já resolve esses problemas iniciais, mas a pergunta que fica nesse momento é: será que é realmente necessário fazer isso? Porque nós vamos querer executar nossas aplicações, como vimos, de maneira isolada uma da outra, ter um controle de recursos, ter um controle de versionamento bem definido.

[04:41] Então será que essa camada de hypervisor é realmente necessária? Será que precisamos sempre nessas situações virtualizar o sistema operacional? Pode ser que sim, pode ser que não. Mas o caso que veremos durante esse curso é a utilização de containers. O que um container é?

[04:58] Repara que se formos comparar os desenhos, não temos a camada de sistema operacional virtualizado e hypervisor, e sim diretamente a camada de container rodando no nosso sistema operacional, e mesmo assim essas aplicações estão isoladas entre si e também isoladas do nosso sistema operacional original.

[05:18] E é isso que vamos entender a partir de agora. Temos algumas perguntas que temos que responder de início: por que os containers são mais leves, além desse argumento visual que vimos agora?

[05:27] Como eles vão garantir esse isolamento? E também como eles vão funcionar sem instalar um sistema operacional? Porque no caso da máquina virtual, a nossa aplicação C# terá um sistema operacional para ela. A nossa aplicação Java também.

[05:39] Se olharmos dentro do nosso sistema de containers, a nossa aplicação C# está diretamente dentro do container. E qual sistema operacional ela vai usar? É Windows, é o Linux? Precisa instalar um sistema? Nós precisamos responder a essas perguntas, de onde vêm essas informações?

[05:57] E também como é que vai ficar a divisão de recursos entre essas aplicações que estarão a partir de agora containerizadas?

[06:02] Nós entenderemos a partir de agora, no próximo vídeo, como essas situações acontecem. Como o container será mais leve em questão de consumo de recursos, como ele vai garantir isolamento, como ele funciona sem instalar um sistema operacional, por assim dizer.

[06:18] Agora que já vimos como os containers nos ajudam, o que eles fazem, assim como as máquinas virtuais ajudam, vamos entender os diferenciais de como o container opera dentro do nosso sistema. Veremos isso na próxima aula. Te vejo lá.
