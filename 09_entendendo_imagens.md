# **Entendendo imagens**

[00:00] Chegou o grande momento de explicar o que são as imagens. Nós vamos entender efetivamente agora o que são as imagens, como elas funcionam, como elas viram containers e como criar nossas próprias imagens, porque não podemos depender só do trabalho alheio para desenvolver o nosso.

[00:15] Então chegou agora a hora de entender o que são as imagens. Por enquanto nós estamos aceitando que as imagens são uma receita para criar um container. Mas efetivamente como elas funcionam?

[00:28] Uma imagem nada mais é do que um conjunto de camadas, que na imagem estamos representando pelas cores vermelha, azul, rosa claro e cinza. É um conjunto de camadas, e quando juntamos essas camadas nós formamos imagens.

[00:45] E essas camadas em si são independentes, cada uma tem seu respectivo ID, por exemplo, cada uma tem o seu respectivo identificador.

[00:55] Então vamos voltar mais uma vez para o caso do dockersamples no nosso terminal para visualizarmos.

[01:04] Quando fazemos um docker run na nossa imagem, nós podemos ver agora as imagens que temos baixadas no nosso sistema através do comando docker images, ou docker images ls.

[01:19] Dando um docker images eu posso ver que tenho baixada a nossa imagem “dockersamples/static-site”, com a tag latest e seu respectivo ID. E ela foi criada há 5 anos pelo grupo do dockersamples. E o tamanho dela é de 191 MB.

[01:39] Nós podemos ir um pouco mais além. Podemos dar o comando docker inspect em uma imagem. Vou fazer novamente o docker images para copiar o ID da imagem. E agora vou fazer docker inspect, passando o identificador do que nós queremos inspecionar.

[02:00] Nós temos diversas informações. Tem um conjunto muito grande de informação que podemos saber detalhadamente sobre determinado recurso dentro do nosso Docker.

[02:10] Temos o ID, qual é a tag do repositório, o digest que foi utilizado para validação da imagem, se tem alguma imagem que é um parent, uma imagem pai ou mãe, a data de criação, o container, container config. Então temos diversas informações acerca dos recursos que podemos ter dentro do Docker.

[02:36] Inclusive, no final nós conseguimos ver mais informações na parte de layers, que são as camadas. Mas podemos ir um pouco mais além. Tem um comando específico para ver quais são as camadas de uma imagem. Vou limpar o terminal.

[02:53] Temos o comando docker history. Vou fazer docker images para pegar mais uma vez o ID. E vamos fazer o comando docker history, passando esse ID. Nós temos a nossa imagem, que é a f589ccde7957, e ele mostra todas as camadas. Ela tem 13 camadas para essa imagem.

[03:28] E quando essas camadas são aglutinadas, empilhadas umas nas outras, elas formam essa imagem final que é “dockersamples/static-site”.

[03:38] E caso alguma outra imagem venha a depender desses camadas, nós conseguimos reutilizá-las. Vamos entender isso daqui a pouco.

[03:45] Mas ele mostra detalhadamente qual é o tamanho de cada uma dessas camadas, a ordem de cada uma delas, o command, workdir, copy. Nós conseguimos ver também a data de criação. Conseguimos ver todas essas informações e entender o que está acontecendo.

[04:05] Mas agora que nós entendemos que uma imagem é um conjunto de camadas empilhadas para formar determinada regra de execução de um container, voltando à nossa apresentação, vamos ver como podemos visualizar um pouco melhor.

[04:22] Quando fizemos nosso docker run pela primeira vez ou simplesmente um docker pull para não executar o container, mas só baixar a imagem, nós fazemos o download das nossas imagens, das nossas camadas.

[04:36] Mas pode ser que, por exemplo, como eu falei para vocês agora, no nosso host nós já tenhamos algumas das camadas que queremos. Então no momento em que fizermos um pull ou um run, que vai fazer um pull consequentemente, nós vamos fazer simplesmente download só das camadas que necessitamos.

[04:52] Então o Docker é inteligente o suficiente para reutilizar essas camadas para compor novas imagens.

[04:58] Então conseguimos ter uma performance muito boa nesse sentido, já que não precisaremos ter informação duplicada ou triplicada, enfim. Porque nós conseguimos reutilizar as camadas em outras imagens. Isso por si só já é muito interessante. Então no fim das contas, conseguimos ter essa reutilização.

[05:17] Mas o que mais podemos ver na parte da criação de imagens? No fim das contas, quando temos a nossa imagem, ela é read only. Isso significa que não conseguimos modificar as camadas dessa imagem depois que ela foi criada.

[05:34] Então voltando ao nosso container, no momento em que nós temos essa imagem “dockersamples/static-site”, ela é imutável, assim como, por exemplo, a imagem que temos do nosso Ubuntu.

[05:55] Vou fazer mais uma vez docker run ubuntu –it bash para executar de modo interativo o nosso bash. Eu já tinha apagado a imagem, e veremos como fazer isso aos poucos, mas vamos baixar a camada necessária para ter a nossa imagem de execução para que consigamos executar nosso container do Ubuntu. Ele baixou, extraiu e vai abrir o nosso terminal.

[06:26] Ele deu um erro porque eu coloquei na ordem errada. O correto é docker run –it ubuntu bash.

[06:37] Nós vimos que tínhamos criado na nossa home, por exemplo, um arquivo qualquer com o comando touch um-arquivo-qualquer.txt. Nós estamos meio que escrevendo dentro do container.

[06:47] Mas como estamos conseguindo fazer isso se a imagem que gera o nosso container é apenas para leitura, ou read only? Se ela é bloqueada para escrita como é que o container consegue escrever informação dentro dela?

[07:01] Porque no fim das contas, quando criamos o container, o container nada mais é do que uma imagem com uma camada adicional de read-write, de leitura e escrita.

[07:13] Então quando criamos um container nós criamos uma camada temporária em cima da imagem, onde conseguimos escrever informações. E no momento em que esse container é deletado, essa camada extra também é deletada.

[07:26] Por isso que quando fizemos aquele experimento anteriormente, a nossa informação dentro do container era perdida quando nosso container era apagado. Porque essa camada é temporária, bem fina e leve para que o container tenha um ambiente de execução muito leve e fácil de ser executado.

[07:43] E agora voltamos naquela primeira pergunta da primeira parte desse curso, que era por que os containers são tão leves?

[07:52] Além da parte de eles serem simplesmente processos dentro do nosso sistema, nós também podemos falar que quando um container entra em execução, nós estamos sempre reaproveitando a mesma imagem.

[08:08] Porque como a imagem é apenas de leitura, nós podemos ter um, dois, 100 ou 10 mil containers baseados na mesma imagem. A diferença é que cada um desses containers vai ter só uma camada diferente de um para o outro de read-write.

[08:23] E como essa camada é extremamente leve, a fim de manter essa performance, nós temos uma reutilização da imagem para múltiplos containers.

[08:32] Então no fim das contas o que acontece é que quando definimos um container ou outro baseado na mesma imagem também logo em seguida, o tamanho do container no fim das contas vai ser só o tamanho da camada de escrita que estamos gerando para ele, porque a imagem em si será reutilizada para cada um deles.

[08:52] E isso é muito legal. Nós veremos um experimento prático em breve, conforme formos avançando na criação e no fluxo das nossas imagens.

[08:59] Mas basicamente agora nós entendemos porque efetivamente o container é tão leve e otimizado. Porque ele consegue reaproveitar as camadas das imagens prévias que já temos.

[09:10] E quando criamos novos containers ele simplesmente só reutiliza as mesmas imagens e camadas, consequentemente, e utiliza a camada de read-write para utilizar de maneira mais performática o que ele já tem no ecossistema do Docker. Isso por si só é muito legal.

[09:28] E no fim das contas, basicamente é isso. Vamos entender ainda a partir de agora como definir um arquivo chamado “dockerfile” que vai nos ajudar a criar nossas próprias imagens, e no fim das contas como gerar os nossos containers através das imagens que vamos criar.

[09:46] Por esse vídeo é só. Agora desmistificamos efetivamente o que é uma imagem, como transformar uma imagem num container e porque o container é tão leve.

[09:56] E ainda vai ficar mais fácil de entender conforme formos avançando e criando a nossa própria imagem e vermos como são as etapas de criar uma camada, uma imagem, transformar em container. Mas isso nós faremos nos próximos vídeos. Eu te vejo lá e até mais.
