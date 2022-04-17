# **Mapeando portas**

[00:00] Agora veremos um exemplo mais visual para vermos todo o fluxo, e veremos como interagir efetivamente com nosso container para ver uma saída, um output real, mais bonito, para realmente vermos como devemos interagir com um container.

[00:16] Ao invés de voltarmos a exe cutar docker run com Ubuntu e hello-world, vamos um pouco mais além. Vamos executar um exemplo prático de uma aplicação web cuja saída vamos conseguir visualizar através do nosso navegador.

[00:29] Que aplicação é essa? Se voltarmos no Docker Hub, existe um grupo de usuários, uma organização chamada “dockersamples”, que disponibiliza diversos tipos de aplicação a fim de exemplificar a utilização do Docker, um pouco mais bonitas e elegantes.

[00:48] Então repara que ao contrário da nossa imagem do Ubuntu, essa imagem do “dockersamples” não é oficial.

[00:56] E além de ela não ter aquele símbolo de verificado, como no Ubuntu, quando uma imagem não é feita por usuários reconhecidos pela comunidade ela segue o seguinte padrão: vai ter um nome do usuário ou organização barra o nome da imagem. Então conseguimos reconhecer que essa imagem não é oficial por conta desse padrão.

[01:17] Então é uma boa prática você sempre tentar manter a utilização de imagens oficiais dentro do seu projeto o máximo possível, mas nesse caso estamos utilizando essa imagem a fim de exemplificar e visualizar o Docker em execução com um container.

[01:34] Eu vou copiar mais uma vez o nome dessa imagem e vou fazer docker run, passando o dockersamples/static-site.

[01:44] Mas vimos quando executamos o Ubuntu que se simplesmente executarmos um docker run e o nosso container ficar em execução, assim como fizemos com o sleep naquele momento, ele vai travar o nosso terminal.

[01:55] Então se eu quiser executar esse comando e manter o comando em background no terminal, para que eu consiga manter o terminal em execução sem travar, eu posso passar a flag -d, de detached.

[02:07] Então ele vai executar o container baseado nessa imagem, mas não vai travar o terminal. Vamos ver o que vai acontecer. Ele vai efetuar o download das camadas necessárias para que esse container baseado nessa imagem “dockersample/static-site” execute.

[02:24] Nós já vimos esse fluxo, ele está indo no Docker Hub, validando todas as camadas que ele precisa para fazer a execução desse container, que é basicamente essa imagem que ele encontrou. E está fazendo a verificação depois de fazer todo o download e extração das camadas na nossa máquina.

[02:42] Então ele terminou a extração, fez o download, e repare que ele não travou nosso terminal, graças à flag -d. Mas agora se eu executar um docker ps, vamos ver o que vai acontecer.

[02:57] Nós temos nosso docker ps, nosso ID do container, nossa imagem baseada, o comando que ele manteve em execução; que ele foi criado há 22 segundos e que ele está em execução há 19 segundos.

[03:13] Então ao contrário do Ubuntu e do “hello-world”, por exemplo, a imagem que foi usada para criação desse container definiu que o comando para o container ser executado trava o terminal.

[03:25] Então esse comando que começa com /bin/sh –c, é um comando que mantém um processo vivo dentro do terminal do nosso container.

[03:37] Então o container em si vai continuar em execução. Se fizermos docker ps várias vezes, a aplicação em si está em execução, graças ao comando padrão que foi executado quando o container subiu.

[03:47] E agora temos a nossa coluna de portas falando que a nossa aplicação está sendo executada na porta 80 e na 443, além do nosso nome, que é “friendly_lamarr”.

[03:59] Então se nossa aplicação está sendo executada na porta 80, vamos abrir no nosso navegador o nosso “localhost:80”. Não acessou. Por quê? Mais uma vez voltando à nossa apresentação, graças aos namespaces, nesse caso principalmente ao NET, nós temos um isolamento das interfaces de rede.

[04:20] Então a porta 80 do meu container não é exatamente uma porta que já está mapeada na minha máquina, no meu host. Eu não vou conseguir acessá-la diretamente assim, elas estão isoladas.

[04:30] Então vamos voltar ao nosso terminal para entender o que está acontecendo. Precisamos visualizar o seguinte: essa porta 80 é de uso do container, e é a porta 80 de dentro da interface de rede do container. Se eu quiser acessá-la de outras maneiras, nós precisamos expor essa porta de alguma maneira.

[04:53] Mas antes disso inclusive, precisamos fazer outra coisa. O nosso container já está em execução. Nós vamos parar e remover esse container de uma vez só, então podemos ser um pouco mais agressivos.

[05:10] Ao invés de fazer o docker stop e depois o docker rm, podemos copiar o ID e fazer docker rm 1b6d75073457, passar diretamente o ID e acrescentar --force. Assim ele vai parar e remover o container de uma vez só. Agora se eu fizer docker ps, não tem mais nenhum container em execução.

[05:30] Vamos executar agora mais uma vez o docker run –d -P dockersamples/static-site. Só que ao invés de só executarmos esse comando mais uma vez, agora vamos colocar a flag -P, com P maiúsculo.

[05:45] Vamos descobrir agora o que essa flag vai fazer. Ele vai executar o nosso container, sem travar mais uma vez, por conta do -d; e ele não fez o download porque ele já tinha o conteúdo na nossa máquina agora.

[05:56] E se fizermos um docker ps, ele está fazendo um mapeamento maluco na nossa coluna de portas, que está um pouco difícil de entender. Mas o resto é a mesma coisa.

[06:11] Vamos executar um comando agora docker port b0e93e405db6 seguido do ID, que é um comando voltado para mostrar como está o mapeamento de portas de um container em relação ao host.

[06:29] Então vamos passar o container, e agora ele está falando que a porta 80 do meu container foi mapeada para a porta 49154 do meu host.

[06:40] Isso significa que se agora no meu navegador eu executar o “http://localhost:49154”, nós conseguimos acessar o nosso container. O conteúdo do nosso container foi acessado, porque agora fizemos um mapeamento de uma porta interna do container para uma porta do nosso host.

[07:12] E no fim das contas nós poderíamos ter feito isso também de uma maneira mais bem definida. Vamos executar o nosso docker rm, passando o ID do nosso container com --force. Vamos executar um novo container.

[07:34] Como eu matei o container, se voltarmos para o navegador e dermos um “F5”, não tem mais o container, não tem mais conteúdo.

[07:39] Mas se executarmos o docker run -d -p dockersanples/static-site mais uma vez, só que agora com a flag -p com P minúsculo, nós conseguimos fazer um mapeamento específico de uma porta do nosso host.

[07:51] Por exemplo, vamos mapear a porta 8080 do nosso host. Ela deve refletir em qual porta do nosso container?

[07:57] Nós vimos que por padrão ele expôs naquelas colunas de porta as portas 80 e 443. Então quero que a porta 8080 da minha máquina reflita na porta 80 do meu container.

[08:09] Ele vai executar. E agora, se voltarmos para o navegador e acessarmos “localhost:8080”, conseguimos fazer esse mapeamento de uma porta agora específica do nosso host para o nosso container.

[08:23] Voltando na nossa apresentação mais uma vez, nós temos esse isolamento de rede, mas conseguimos fazer um mapeamento para que consigamos acessar o conteúdo do nosso container e vê-lo de maneira que consigamos validar o que está acontecendo.

[08:38] Fazemos isso para que não fiquemos às cegas do que está sendo executado dentro do nosso container e para que, no fim das contas, nós consigamos expor nossa aplicação também para que algum usuário consiga acessar.

[08:50] Nessa aula fizemos essa parte de voltar a execução e entender mais alguns atalhos, como a flag -d, por exemplo, que mantém nosso terminal destravado; e também fazer o mapeamento de portas entre o nosso host e o nosso container.

[09:05] Por esse vídeo é só, nos vemos na próxima. Até mais.
