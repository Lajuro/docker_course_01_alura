# **Fluxo de criação de containers [Transcrição]**

[00:00] Vamos entender o que aconteceu. Primeiro: por que o container não rodou? Vamos voltar ao nosso terminal mais uma vez.

[00:07] Vamos tentar mais uma vez por teimosia colocar docker run ubuntu. Nada aconteceu de novo. Mas vamos entender e aproveitar para conhecer outros comandos do Docker que vão nos auxiliar a entender se o container realmente executou ou não, e por que ele não exibiu nada.

[00:26] Um comando muito útil que vamos utilizar bastante é chamado docker ps. Ele vai exibir quais containers estão em execução no presente momento. Vou limpar a tela e fazer docker ps, e ele exibiu só o cabeçalho.

[00:40] No fim das contas significa que minha tabela de containers em execução está vazia. Então não tem nenhum container efetivamente em execução.

[00:48] Apenas a título de curiosidade, outra maneira um pouco mais semântica para utilizar o docker ps, é o comando docker container ls. É a mesma coisa, um pouco mais verboso, mas ao mesmo tempo mais semântico. É o mesmo comando que será executado, então a saída tinha que ser a mesma também.

[01:09] Nós já sabemos que nosso container não está em execução. Então como é que podemos ver todos os containers, inclusive os que já não estão mais em execução, para saber se o nosso docker run fez alguma coisa efetivamente ou não?

[01:21] Esse comando pode ser simplesmente o docker ps –a, ou o docker container ls –a, que é a mesma coisa. Vamos executar.

[01:30] Repara que ele tem nosso “hello-world”, que executamos no caso há 9 minutos. Tem o Ubuntu que fizemos no vídeo anterior e o outro Ubuntu que é o que acabamos de fazer na base da teimosia.

[01:49] Vamos entender cada uma dessas colunas. A primeira é o container ID, que é um identificador. O ID, obviamente, tem que ser único para cada container que vai ser criado.

[01:58] Depois temos a imagem que foi usada como base para criação desse container. Temos docker run ubuntu duas vezes e docker run hello-world.

[02:06] Depois o comando que foi executado ao criar esse container. Para os comandos do Ubuntu foi executado um bash, para o hello-world foi executado um /hello. Em seguida temos o momento que foi criado, um deles foi criado há um minuto, outro há 4 e outro há 9.

[02:19] E em seguida temos o status, que está como exited para todos. Por isso que eles não foram exibidos no docker ps ou no docker container ls, só quando passamos a flag -a.

[02:29] Depois temos a questão das portas, que vamos entender em breve. E a coluna de names, que é simplesmente o nome que ele cria automaticamente para o container quando não especificamos um nome para ele. Por enquanto não estamos nos preocupando com isso, é só um preciosismo do Docker, que cria um nome aleatório para os containers.

[02:45] Mas vamos voltar e responder à pergunta: por que o container não está em execução? A resposta já está na tela inclusive. É por causa da linha de comando.

[02:57] No momento em que um container é executado a partir dessa imagem, está definido que quando o container subir e for executado ele vai executar o comando bash, no caso do Ubuntu. No caso da imagem do hello-world ele vai executar um /hello.

[03:14] No momento em que executamos mais uma vez o docker run ubuntu, ele vai subir o container, vai executar o comando bash e pronto. Quando ele executa o comando bash ele já fez o que tinha que fazer, já cumpriu o objetivo dele.

[03:32] Então voltando à nossa apresentação, no fim das contas o container foi executado. Ele subiu, executou o bash, fez o que tinha que ser feito, que era executar. E a partir desse momento não tinha mais nenhum processo segurando a existência desse container. Então por isso ele foi encerrado.

[03:48] Para que um container esteja em execução deve ter no mínimo um processo dentro dele para que o container fique vivo. Então se não houver processos em execução, o container não vai ficar em execução. E como só pedimos para ele executar um bash, ele abriu, fez o papel e fechou.

[04:06] Então essa é a primeira questão: no momento em que executamos o run, ele fez esse comando e fechou logo em seguida, porque nós não mantivemos nenhum processo em execução. Então vou limpar o terminal, e se executarmos o comando docker run ubuntu mais uma vez, o que podemos fazer?

[04:26] Vou passar um docker run --help para lembrarmos do que vimos, na verdade. Quando nós especificamos a imagem, nós podemos passar um comando para que esse container execute.

[04:41] Nós já sabemos que dentro do Ubuntu com um todo nós temos a linha de comando que nós podemos executar. Então eu quero que esse container, por exemplo, execute o comando de docker run ubuntu sleep 1d.

[04:56] Eu quero que o comando que o container execute quando esse Ubuntu subir seja um sleep de um dia. Então tecnicamente, quando esse container subir ele vai ter um processo de sleep travando ele por um dia. Será que vai funcionar? Vamos ver agora. Eu vou dar um “Enter”.

[05:15] Ele travou o nosso terminal a princípio. Como ele travou nosso terminal, vamos abrir um novo e vamos executar docker ps.

[05:42] Nós temos um container ID, com a imagem Ubuntu. O comando é um sleep 1d. Como esse comando vai demorar um dia para ser executado, esse container vai ter um tempo de vida de um dia. E ele está rodando, o status dele contém “Up” há 27 segundos. A questão de portas, mais uma vez, vamos relevar por enquanto. E o nome dele é “funny_pike”.

[06:02] Entendemos agora como conseguimos manter um container em execução e porque ele parou de executar, quando simplesmente não especificamos um comando que deveria ser executado. Porque não tinha nada travando a execução dele, agora tem, que é o nosso sleep de um dia que passamos que esse container deveria executar.

[06:21] E agora, a segunda pergunta que ainda temos que responder, voltando à nossa apresentação é: o que o docker run fez por baixo dos panos para que nosso container executasse daquela primeira vez?

[06:33] No momento em que tínhamos o nosso host, no caso o nosso Ubuntu, executando o comando docker run ubuntu ou docker pull ubuntu, ele simplesmente foi no Docker Hub e falou: “Eu preciso dessa imagem chamada Ubuntu”.

[06:46] E o Docker Hub falou: “Eu tenho essa imagem e vou passá-la para você”. Então fizemos o download dessa imagem e depois o que o nosso host fez, naquela parte que dizia “digest sha256”, foi simplesmente uma validação para verificar a autenticidade da imagem, se realmente era a imagem que estávamos procurando.

[07:08] Então no momento em que fazemos o docker run, se não tivermos a imagem localmente nós a buscamos no Docker Hub, fazemos uma validação em cima de um hash e executamos nosso container, que como vimos no caso do Ubuntu, vai ter geralmente um comando padrão a ser executado. Se colocarmos mais uma vez o -a para comparar, veremos que esse comando será o bash.

[07:29] Então se simplesmente não tivermos cuidado, e vamos ver como lidar com isso no decorrer da criação dos nossos containers, nós simplesmente acabaremos criando containers zumbi. Eles vão subir e morrer logo em seguida, porque não teremos nenhum processo travando eles.

[07:43] Mas no caso de agora, vimos que se mantivermos no mínimo um processo, o nosso container vai ficar sempre em execução.

[07:51] Então por esse vídeo é isso. Entendemos agora o que mantém um container vivo, em execução versus o que mantém um container parado e o que o docker run faz para que consigamos executar efetivamente um container quando não possuímos uma imagem localmente.

[08:07] Então por esse vídeo é só. Nos vemos na próxima. Te vejo lá.
