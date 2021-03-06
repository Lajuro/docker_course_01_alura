# **As redes none e host**

[00:00] Agora veremos como funcionam as duas redes restantes. Vamos dar um docker network ls.

[00:06] Já vimos como funciona a bridge, e nós criamos nossa própria bridge também. Mas vamos olhar como funciona a rede host, que utiliza o driver host, e a rede none, que utiliza o driver null.

[00:19] Vamos começar pela rede none, que utiliza o driver null. Como é que ela funciona? Vamos exemplificar para ver como realmente ela impacta a vida do nosso container.

[00:31] Vamos executar um docker run –d. Coloquei o -d porque não vamos nos preocupar com questão de terminal em modo interativo. Em seguida vou falar que meu container será executado na minha rede chamada none, que já existe: docker run -d --network none.

[00:48] Vou executar a imagem do Ubuntu, e o comando que eu quero executar para o container se manter em execução é o sleep, como fizemos no início para manter o container em execução e não precisar travar o terminal para ele: docker run -d --network none ubuntu sleep 1d. Vou executar esse comando. Ele mostrou o ID completo do container.

[01:08] E se fizermos docker inspect nesse ID para vermos quais são as características desse container, repara que no final ele está falando que está utilizando agora o none e toda a descrição da rede desse none.

[01:25] Mas o que isso impactará diretamente nesse container? No fim das contas, quando utilizamos o driver none, estamos simplesmente falando que esse container não terá qualquer interface de rede vinculada a ele. Ele ficou completamente isolado a nível de rede.

[01:41] Nós não conseguimos fazer nenhum tipo de operação envolvendo a rede desse container, porque o driver dele é none, ele utiliza o driver null no fim das contas.

[01:53] O que precisamos fazer agora, caso queiramos fazer o contrário disso, por exemplo? Queremos que nosso container tenha interface de rede, e já vimos como fazer com a bridge, mas de uma maneira um pouco mais prática em alguns casos. Nós queremos fazer o contrário de não ter uma interface de rede, e sim ter uma interface de rede, mas vinculada ao nosso host, por exemplo.

[02:13] Vamos fazer uma leitura das nossa redes com docker network ls. Nós temos a nossa rede que utiliza o driver host e possui também o nome host.

[02:24] E como vai funcionar agora? Vamos fazer praticamente o mesmo teste. Se eu fizer um docker ps, eu vejo que não estou com mais nenhum container em execução além desse Ubuntu que eu acabei de criar.

[02:35] E agora eu vou fazer docker run -d --network host aluradocker/app-node:1.0.E antes do nome da imagem vou dizer que esse container será executado na rede host. Vamos ver o que vai acontecer. Vou copiar o ID do container e fazer docker inspect. Agora no final ele está informando que está utilizando a rede host na saída desse inspect.

[03:09] Só que o que isso muda na prática? Agora eu vou simplesmente abrir uma nova aba do meu navegador e tentar acessar essa aplicação.

[03:20] Mas não como eu vou acessar se eu não fiz o mapeamento de portas como já aprendemos? Se eu colocar “localhost” e definir qual porta eu quero acessar, vamos lembrar que a versão 1.0 da nossa aplicação app-node executava por padrão sempre na porta 3000.

[03:40] E depois nós parametrizamos as versões 1.1 e 1.2. Mas a 1.0 sempre era executada na porta 3000. Então se no meu navegador eu tentar acessar a aplicação na porta “localhost:3000”, eu consigo.

[03:54] Mas por que eu consegui? Porque nós simplesmente agora retiramos quaisquer isolamentos que tinham entre a interface de rede do container e do host. Porque utilizando o driver host nós estamos utilizando a mesma rede, a mesma interface do host que está hospedando esse container, por assim dizer.

[04:14] Então caso tivesse alguma outra aplicação na minha porta 3000 com meu host em execução, eu não conseguiria fazer a utilização desse container dessa maneira, daria um problema de conflito de portas, porque a interface seria a mesma.

[04:29] Basicamente a ideia desse vídeo foi essa, para finalizar e ver como funcionam os outros dois drivers, o host e o null para que consigamos fechar toda essa parte de rede e não passar nada batido por nós.

[04:43] Agora veremos um pouco de prática para ver como fazer a comunicação de dois containers, mas em um ambiente um pouco mais elegante entre duas aplicações. Veremos isso no próximo vídeo. Eu te vejo lá e até mais.
