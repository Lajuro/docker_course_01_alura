# **O problema de persistir dados**

[00:00] Antes de seguirmos no nosso fluxo original, vamos revisar os comandos importantes que já vimos.

[00:10] Vamos dar um docker ps. Não temos nenhum container em execução. Se fizermos um docker ps –a, temos vários containers parados.

[00:18] Vamos dar aquela revisada e remover todos os containers. Então vou fazer docker container rm. E vou usar como entrada a saída do meu comando docker container rm $(docker container ls –aq).

[00:32] Na flag -aq, o q é para pegarmos somente os IDs e o -a é porque eu quero pegar todos os meus containers, inclusive os que estão parados. Se eu der um “Enter”, ele vai remover. Vamos fazer um docker images. Nós temos algumas imagens.

[00:52] Agora o que vamos fazer é um docker rmi $(docker image ls –aq). Com isso ele está removendo todas as imagens. Repara que ele deu um conflito.

[01:09] Ele está falando que algumas imagens estão sendo referenciadas por múltiplos repositórios, então precisamos forçar essa remoção. Vamos fazer o mesmo comando, mas passando o docker rmi $(docker image ls –aq) --force no final. Assim ele consegue agora remover essas imagens também.

[01:26] Então caso você não consiga, a flag --force vai dar essa força para nós. Agora se nós fizermos um docker images, não temos mais nada, foi tudo removido.

[01:37] Qual é a grande mágica que veremos durante essa etapa do curso? Vamos voltar às origens e dar um docker run –it ubuntu, porque eu quero iniciar um container do Ubuntu em modo interativo. Nós vamos entender o porquê.

[01:54] Vou dar um “Enter” para ele baixar a imagem rapidamente. Nesse caso, como a imagem é bem curta, vai ser rápido, não precisamos fazer nenhum corte nesse caso.

[02:06] Estou com meu container já praticamente em execução, ele está terminando de extrair. E eu vou abrir já outro terminal e fazer docker ps. E com isso ele mostra as informações desse container.

[02:25] Até então nada de novo. Mas existe uma flag bem interessante de vermos, que é a -s. Então se fizermos docker ps –s ou docker container ls –s, repara que surgiu uma coluna extra. Nessa coluna ele fala que o tamanho desse container é 0B, mas o tamanho virtual dele é 72.8 MB. O que isso quer dizer?

[02:53] Vamos voltar à nossa apresentação original falando sobre imagens, como elas funcionam e afins. Lembra que uma imagem, no fim das contas, é um conjunto de camadas que estão empilhadas uma em cima da outra? Nós conseguimos, aliás, ver essa informação com docker history.

[03:12] Se eu fizer um docker history na imagem do Ubuntu, por exemplo, vejo que ela é composta por duas camadas, uma de 0B e outra de 72.8MB.

[03:21] Então repara que o tamanho virtual do meu container é meio que o tamanho total da minha imagem. Isso faz total sentido, porque no fim das contas o container nada mais é do que a imagem com uma camada extra de read-write.

[03:43] No momento em que criamos esse container, até então não tem nenhum dado dentro dele além das informações originais da imagem, então o tamanho dele vai ser igual ao tamanho da imagem. Mas o tamanho mesmo dele efetivamente será 0B. O tamanho virtual dele vai ser só o tamanho da imagem no fim das contas.

[04:03] Vamos voltar ao nosso outro terminal e fazer algumas outras operações. Por exemplo, vamos fazer apt-get update. Vamos fazer algumas operações dentro do nosso container para ver o que vai começar a acontecer com aquele tamanho que estamos vendo.

[04:19] Ele vai atualizar o repositório, nós podemos criar alguns arquivos. Você também pode fazer os experimentos que você quiser. Eu só estou dando uma atualização no repositório.

[04:29] Se eu fizer agora docker ps –s, repara que o size dele já está em 16.2MB. Agora o tamanho virtual do meu container é o tamanho que era original da imagem que tínhamos com o docker history mais o tamanho das informações de dados que eu tenho dentro do meu container.

[04:56] Então essa informação na coluna de size nada mais é do que as informações que estão agora na nossa camada de read-write. São informações a princípio temporárias, porque lembra que essa camada é fina e temporária, só para informações que serão escritas dentro daquele container.

[05:14] E é por isso que se criarmos outros containers a partir da imagem do Ubuntu, teremos cada um com uma camada de read-write diferente e os containers terão o mesmo tamanho base no fim das contas, para que consigamos fazer essas operações. Mas cada um terá a sua camada de escrita separada.

[05:34] Então repara que se dermos um docker ps –s mais uma vez, o tamanho já vai estar praticamente o dobro, porque o apt-get update já foi executado provavelmente.

[05:42] Mas é aquela velha história: se eu voltar no meu container, sair dele e der um docker ps, ele já não está mais em execução. Mas agora eu vou criar um novo container com docker run –it ubuntu bash.

[05:59] Se eu voltar no meu outro terminal e fizer docker ps –s, teremos um novo, que é a mesma história: repara que o tamanho dele zerou, porque as camadas de read-write são isoladas umas das outras, cada container terá a sua.

[06:13] Se fizermos docker ps –sa, nós temos agora o antigo, que não está mais em execução, e o outro que ainda está em execução.

[06:22] Então agora precisamos entender como podemos persistir essas informações de alguma maneira para que containers que já foram removidos e talvez subam de novo com alguma informação mantenham esses dados.

[06:35] Porque vimos que essa camada não é persistente entre containers, ela também não é persistente caso eu remova esse container e suba um novo, eu não vou ter essa informação mais. Então como podemos persistir essas informações?

[06:49] A primeira informação que podemos seguir de uma maneira, além da documentação, é utilizar os volumes. Existem três tipos principais.

[06:58] Um deles é a parte do bind mount, que é uma maneira com que podemos fazer um build entre o file system do nosso sistema operacional e o sistema de arquivos do nosso container. Então teremos uma ponte entre essas duas partes, que vai persistir essa informação no nosso host.

[07:11] Temos o volume efetivamente, que será gerenciado pelo Docker. Mas vamos entender tudo isso em mais detalhes. E tem o tmpfs, que é temporário. Mas vamos entender a utilidade dele também.

[07:22] Agora que já entendemos o problema que precisamos enfrentar e como resolver ele, com essas três possíveis soluções, vamos terminar essa aula por aqui para ficar com essa parte mais instigada de entender com o que vamos resolver. Eu te vejo no próximo vídeo e até lá.
