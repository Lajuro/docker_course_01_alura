# **Conhecendo a rede bridge**

[00:00] Voltando um pouco, lembra que nós vimos sobre a questão de como os containers são isolados em relação ao nosso host e como precisamos nos preocupar em como eles vão se comunicar?

[00:09] Porque no fim das contas estávamos debatendo aquela questão de que um sistema complexo é composto por diversas aplicações atualmente.

[00:16] Então pode ser que tenhamos uma aplicação Java se comunicando com uma C#, que se comunica com uma Nginx. Ou podemos pensar num caso clássico de uma aplicação back-end se comunicando com um servidor de banco de dados, por exemplo.

[00:28] Então se os containers estão isolados, como podemos lidar com essa questão da comunicação entre containers?

[00:37] Se voltarmos naquela questão dos namespaces, nós temos toda aquela parte que já provê isolamento para nós nas interfaces de rede. Mas como será que isso funciona dentro do Docker?

[00:50] Vamos voltar ao nosso terminal. E nesse momento podemos testar o nosso experimento clássico de execução de um container Ubuntu. Então vou fazer docker run –it Ubuntu bash. E vou colocar também um bash para executarmos.

[01:06] O que vai acontecer nesse momento? Já sabemos que o container vai ficar em execução. Mas eu vou abrir um novo terminal com um docker ps. Temos o nosso container que acabou de subir.

[01:21] Existe um comando interessante com que podemos inspecionar as configurações, os detalhes de um container quando ele já está em execução ou até mesmo em outras ocasiões também. É o docker inspect. Colocando o ID desse container e dando um “Enter”, ele vai dar diversos detalhes.

[01:42] Já no final tem a parte que estamos procurando, que é a parte de networks, de redes. E dentro desse conjunto de redes ele tem uma chamada bridge que tem diversas configurações.

[01:56] Mas em que momento nós configuramos essa rede? A questão é que nós não configuramos. Quem fez isso foi o próprio Docker.

[02:03] Vamos fazer uma comparação. Eu vou abrir mais um terminal e executar mais um container do Ubuntu com docker run –it ubuntu bash. E vamos comparar a saída desses outputs de rede.

[02:25] Então vou abrir mais terminal e fazer um docker ps e um docker inspect com o ID desse outro Ubuntu que acabamos de criar.

[02:35] Repara que se colocarmos lado a lado, toda essa parte de rede que ele está mostrando é igual. A parte de IPAMconfig como null, o network ID é igual.

[Aula5_video1_imagem1]

[02:49] Então todos esses pontos dentro do nosso sistema, exceto o endpoint ID e o IP address, são iguais. Por quê? Isso significa então que esses containers no fim das contas estão na mesma rede.

[03:04] Mas será que conseguimos fazer algum tipo de comunicação entre eles, já que eles estão na mesma rede, que é um driver que o Docker está colocando para nós? Antes de pensar nisso, precisamos entender o que é a bridge.

[03:15] Então vou abrir mais um terminal para ficar tudo bem separado o que estamos fazendo. E existe, dentro de todo o arsenal de comandos que o Docker provê para nós, uma parte sobre redes. Temos o docker run, o docker images, o docker build, e temos o docker network.

[03:34] E como eu faço para listar as redes que o Docker já tem no sistema, criado de maneira automática? Basta eu fazer docker network ls. Ele mostra três redes para nós, uma se chama bridge, que tem seu ID, o driver bridge, e um escopo local. Tem uma que se chama host, que usa o driver host e o escopo também é local. E no fim das contas também temos uma última, que se chama none, que poderíamos não colocar nenhuma rede dentro do nosso container.

[04:10] Mas como isso vai funcionar no fim das contas? O que isso tudo significa e por que precisamos nos preocupar com isso?

[04:17] Se compararmos nossos IDs, pegando um dos meus inspects, nós temos que o ID da rede começa com 80a1db. Na sua máquina vai ser diferente. E repara que é exatamente a mesma rede que estamos vendo no nosso network ls.

[04:33] Isso significa que os nossos dois containers que criamos sem definir nenhuma rede foram colocados nessa rede padrão bridge, com esse nome e utilizando esse driver também de bridge.

[04:43] E o que isso significa? Significa que se, por exemplo, eu tentar acessar algum desses containers, como o container de ID 8ea67 e fizer um docker ps e um docker inspet, ele tem o IP address dele, que é 172.17.0.2.

[05:17] E se fizermos um docker ps no outro, que começa com b02, e fizermos um docker inspect, nós temos o IP address de 172.17.0.3.

[05:29] Então se eu tentar, por via das dúvidas, acessar o meu b02, cujo IP address termina com 03, e por algum motivo eu tentar comunicá-lo com o outro via IP, eu devo conseguir, já que eles estão na mesma interface de rede.

[05:55] Só que como é que isso vai funcionar? Como estamos usando uma imagem do Ubuntu, bem provavelmente, caso tentemos executar algum ping, ele não vai conseguir.

[06:04] Então é a velha etapa: nós precisaríamos usar uma imagem base que já contém o ping ou podemos simplesmente fazer apt-get update, e depois instalamos o ping para fazer esse experimento.

[06:16] Existem imagens que já vêm com ping, mas como estamos padronizando os nossos primeiros testes com a imagem do Ubuntu, para mantermos o padrão vale nós continuarmos com toda essa parte de utilizar o Ubuntu.

[06:28] Existem outras imagens voltadas para essa parte de teste de rede e afins que também você pode consultar no Docker Hub, mas como eu falei, só na questão de ping mesmo nós vamos fazer esses testes.

[06:40] Então ele vai atualizar os pacotes rapidamente e quando ele terminar vamos instalar o pacote do ping para que consigamos fazer essa comunicação. Assim que ele terminar todo o processo de atualização e instalarmos o ping eu volto.

[06:56] Nós fizemos o apt-get update, e logo depois para agilizar eu já executei o comando de instalação também, que foi apt-get install iputils-ping.

[07:11] Se eu der um “Enter” ele já vai ter instalado. Mas a ideia é só para fazermos a instalação do ping. Então se eu tentar agora dar um ping no 172.17.0.2, que no caso é o de início 8ea, ele vai fazer a comunicação sem nenhum problema.

[07:57] Então estamos conseguindo fazer essa comunicação entre containers via IP. Mas quais são os problemas que isso pode levantar? Porque estávamos fazendo uma comunicação diretamente via IP. Mas já vimos que os containers estão suscetíveis a reiniciar, a serem recriados e afins. E isso não vai garantir que o contêiner vai ter sempre o mesmo IP. Então teremos uma conexão muito instável nesse sentido.

[08:22] Precisamos ter uma maneira mais certa de fazer isso, como, por exemplo, via um DNS, talvez um host name seria interessante.

[08:29] Mas como vamos entender isso? Nós já entendemos primeiro o que são as redes, vimos que podemos containers que estão na mesma rede.

[08:37] Mas vamos aprofundar isso um pouco mais vendo a questão de como podemos criar a nossa própria rede e como ela vai se comportar nesse sentido. Só que isso nós faremos no próximo vídeo. Eu te vejo lá e até mais.
