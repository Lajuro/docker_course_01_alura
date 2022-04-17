# **Outros comandos importantes**

[00:00] Agora vamos entender mais alguns comandos que serão muito úteis para nós no decorrer desse curso para que consigamos desenvolver nosso conhecimento com o Docker.

[00:12] Até então nós temos a criação de containers, já vimos o que o docker run faz, como ele funciona; a questão do comando padrão, que a princípio é executado quando executamos uma imagem. E vimos como sobrescrever esse comando, no caso colocando um sleep de um dia.

[00:28] Mas o que mais é importante de saber? Tem uma coisa que ainda precisamos entender. Eu vou limpar a tela e fazer um docker ps novamente. Temos nosso container em execução com nosso sleep de um dia.

[00:48] Ele está em execução, nós mantivemos um terminal travado para isso, o que é um pouco chato. Mas o que acontece, por exemplo, se eu quiser fazer um fluxo um pouco mais utilizável, por assim dizer?

[01:01] Vamos fechar esse terminal que está travando o nosso. Se eu der um docker ps agora, ele vai manter o meu container em execução, porque eu fechei o outro.

[01:14] Mas se eu quiser parar a execução desse container, eu posso executar o comando docker stop e passar para ele o ID ou o nome do container que eu quero. Eu posso copiar o ID ou o nome do container que eu quero parar e colar logo após o comando docker stop.

[01:38] Ele vai demorar um tempo e vai parar a execução desse container. Então no momento em que damos um docker ps de novo, não teremos mais nenhum output. Não temos mais nenhum container em execução.

[01:53] E se eu quiser por algum motivo reexecutar o meu container que foi parado? Vou fazer docker ps –a.

[02:01] Eu posso pegar o ID do meu container e simplesmente fazer docker start, e passar o ID dele mais uma vez. Nesse momento ele vai voltar a executar o meu container.

[02:13] Se fizermos um docker ps de novo, ele está em execução. Ele foi criado há 11 minutos, mas o status dele é de execução só há 4 segundos.

[02:21] Então conseguimos parar e reexecutar os nossos containers com esses dois comandos, o docker start e o docker stop.

[02:32] Para que eu consiga a fazer inicialização a partir de um start é preciso que meu container esteja em estado de parada. E vice-versa: se eu quiser parar ele precisa estar no estado de execução.

[02:43] Vamos um pouco mais além. O meu container do Ubuntu que estamos usando para exemplificar está em execução. Mas eu como é que eu interajo com ele? Porque a princípio nós não estamos conseguindo fazer nada. Ele está em execução, mas não está servindo para nada.

[03:02] Então como é que eu posso interagir com esse container de maneira interativa para que eu consiga fazer alguma coisa?

[03:09] Existe um comando, também dentro desse universo todo do Docker, que é o docker exec. Eu posso simplesmente falar que eu posso executar algum comando dentro do meu container em modo interativo.

[03:23] Então para que seja em modo interativo eu vou adicionar docker exec -it ao comando. O I é de modo interativo, e o T é que eu quero acessar o tty, o terminal padrão desse container.

[03:37] E eu coloco também o ID do container que eu quero fazer isso, e em seguida eu posso executar algum comando.

[03:43] Qual comando eu posso usar para navegar dentro do meu Ubuntu, que estamos assumindo esse conhecimento de terminal? Eu posso executar simplesmente um bash.

[03:56] Ele alterou meu terminal, agora ele está com um usuário root nessa máquina, e se formos comparar é exatamente o ID do meu container.

[04:05] Então agora eu estou dentro do terminal do meu container. Então tudo que eu fizer agora, como vimos naquela questão dos namespaces, estará devidamente isolado.

[04:14] Se voltarmos à apresentação, por exemplo, nós conseguiríamos ver que na verdade tudo está devidamente isolado por conta dos namespaces. Nós temos processo isolado, rede isolada, a intercomunicação de processos, file system, o Kernel.

[04:33] Se voltarmos para o terminal e acessarmos, por exemplo, a home desse container e criarmos um arquivo touch eu-sou-um-arquivo.txt, o que vai acontecer? Eu vou dar um ls e vai aparecer o meu arquivo.

[04:52] Mas se eu vier na minha máquina e abrir minha home não aparece nada, porque são sistemas de arquivos isolados, graças ao namespace de MNT. É o file system que está completamente isolado.

[05:07] Nós podemos fazer diversas coisas agora nesse Ubuntu, porque ele vai estar devidamente isolado do nosso sistema. Nós poderíamos executar os comandos apt, com apt-get update, apt-get install, conforme nossa demanda, e vai estar tudo isolado do nosso sistema original.

[05:29] Vou parar essa execução do apt update, porque não estamos nos importando com isso e vou limpar a tela com “Ctrl + L”. Tudo que fizermos estará dentro desse terminal, desse container.

[05:40] No caso do Ubuntu, podemos até executar o comando top, e ele vai mostrar os processos que estão em execução, do nosso usuário root, que é exatamente nosso sleep que estava mantendo o nosso container em execução, e o nosso bash, que estamos escutando agora.

[05:55] Então nosso container está com dois processos neste momento no nosso usuário root.

[06:00] Vou parar novamente e dar um “Ctrl + L”. Vou dar um “Ctrl + D” para sairmos do container e um docker ps de novo. Ele ainda vai estar em execução porque o nosso sleep ainda está em execução.

[06:15] Eu vou dar um docker stop nesse meu container e reexecutar. E vou dar um docker start mais uma vez para vermos o que acontece.

[06:41] Mais uma vez vou executar aquele comando para acessarmos o terminal em modo interativo. E nesse momento, se eu voltar para minha home e der um ls, está aparecendo meu arquivo.

[06:53] Agora vou dar um top. Ele simplesmente resetou toda minha árvore de processos, ele deu um sinal de SIGKILL, por assim dizer, em toda minha árvore de processos, porque eu parei todos os processos e os recomecei. Então o tempo de execução deles foi zerado. Toda a contagem do processo foi reiniciada.

[07:13] Então essa é uma questão que quando executamos o stop acontece. Vou sair do terminal mais uma vez e executar outro comando como, por exemplo, docker pause e passar o ID do nosso container de novo. Com isso nós podemos também pausar o nosso container.

[07:34] Se fizermos docker ps ele vai aparecer ainda, mas no status de pausado, e não de parado. E se dermos um docker ps de novo, repara que a contagem do status dele continua.

[07:50] Se eu tentar acessar o container agora eu não vou conseguir, porque ele está pausado. E eu posso simplesmente despausar esse container com o comando docker unpause.

[07:59] E se eu tentar acessar agora eu vou conseguir. E se eu der um top vemos que nossa árvore de processos a princípio foi mantida, porque ele mantém todo o nosso fluxo de execução, assim como nossos arquivos. Mas essa é uma situação menos agressiva em relação ao stop que podemos fazer.

[08:20] Então nós vimos como podemos parar um container, dispará-lo, no caso, voltar a execução. Vimos como podemos pausar e despausar e a diferença entre cada um desses tipos de operação.

[08:35] E vimos também que devidamente os nossos containers estão isolados do nosso host original, graças à utilização do namespace NMT.

[08:48] Eu vou fazer um último detalhe para ficarmos com uma pulga atrás da orelha. Eu vou dar um docker ps. Mas agora eu vou pegar esse meu container ID e fazer um docker stop mais uma vez.

[09:05] E se eu quiser evitar que ele fique demorando 10 segundos para executar eu posso colocar a flag -t=0, antes do nome do meu container, para que não tenha nenhum tempo para parar, porque por padrão ele espera 10 segundos para nosso container parar de maneira saudável. Mas se quisermos nos apressar, podemos colocar o -t=0, que ele vai parar instantaneamente.

[09:31] E agora eu posso remover esse meu container com docker rm, que é o comando de remoção, passando o ID do meu container. Com isso ele vai remover.

[09:46] Se eu criar mais uma vez com o nosso docker run Ubuntu sleep 1d e manter um sleep de um dia, ele vai travar nosso terminal. E por fim, se eu abrir um novo e fizer um docker exec –it 48aac971d7fb bash neste nosso terminal que foi criado, nós acessamos o nosso terminal. Se entrarmos na nossa home com ls o nosso arquivo sumiu.

[10:30] Como o nosso container deixou de existir e ele estava completamente isolado dos outros containers e do nosso host, todo o conteúdo dele foi perdido.

[10:39] Então o container tem essa questão de ser efêmero nesse sentido. Os containers devem estar sempre prontos para deixar de ser executados, e nós devemos estar prontos para perder esses dados caso não configuremos nada em relação a isso. Então é uma questão que também veremos mais à frente, como lidar com a persistência de arquivos em container.

[10:58] E para finalizar, mais um comando interessante é o seguinte: ao invés de ter que fazer docker exec toda hora depois de dar um sleep, teria que ter uma maneira mais prática de já começarmos a executar nosso container e mantê-lo em execução sem precisar ficar dando sleep, sem precisar ficar roubando nesse sentido.

[11:18] Nós podemos simplesmente dar um docker run ubuntu bash, mas indo mais além, podemos falar que queremos executá-lo em modo interativo, assim como nosso exec: docker run -it ubuntu bash. E vamos simplesmente criar um container novo, e já estamos diretamente no terminal dele.

[11:39] Se abrirmos mais um terminal e dermos um docker ps, nós temos o que criamos com o sleep de um dia ainda há pouco, e o nosso bash que acabamos de criar há 10 segundos.

[11:52] Se fizermos qualquer coisa dentro dele, como ls, criar algum arquivo na home, dá certo. Mas no momento em que eu sair desse terminal ele vai matar o meu container, por aquele motivo que explicamos. Agora não há mais nenhum processo, antes tinha o nosso bash, agora não tem mais o nosso terminal que estava travando a execução de um processo para que o container se mantivesse em execução.

[12:20] Então a partir de agora, no momento em que finalizamos a execução do nosso único processo, o container morreu.

[12:27] Nós vimos agora alguns pontos que são muito importantes nessa parte de ciclo de vida dos containers, e entendemos que por eles serem devidamente isolados, nós não conseguimos manter as informações de alguma maneira. Mas vamos responder isso também em breve, fique tranquilo, fique tranquila.

[12:43] Essa aula foi para entendermos mais alguns comandos que são muito úteis e interessantes, e alguns parâmetros que podemos e devemos utilizar com o Docker. Eu te vejo na próxima e até mais.
