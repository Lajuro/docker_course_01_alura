# **Utilizando tmpfs**

[00:00] Chegamos ao terceiro tipo que podemos utilizar de persistência com o Docker, nem tanto de dados, que são os tmpfs.

[00:11] Antes de seguirmos, algumas peculiaridades: a primeira é que ele só vai funcionar no host Linux. Então por isso é importante estarmos utilizando o Linux, porque diversas funcionalidades, como essa, por exemplo, são feitas para rodar em ambiente Linux.

[00:27] Então essa é a importância de você estar seguindo provavelmente esse curso no Linux também, porque é uma questão que já está disponível dentro desse ambiente.

[00:35] Mas vamos ver como o tmpfs funciona e o que vai mudar. Nós já executamos containers diversas vezes. E agora qual será a diferença?

[00:45] Temos toda a nossa parte de definir como um container vai funcionar. Mas como é que fazemos para utilizar agora um tmpfs?

[00:55] No fim das contas, se fôssemos olhar na documentação, mas eu não vou dar spoiler para vocês, nós vamos defini-lo de maneira bem simples, porque não vamos utilizar o -v agora. Ele possui uma flag própria já, que no caso é a --tmpfs.

[01:11] Se fizermos docker run –it --tmpfs=/app ubuntu bash e dermos um “Enter”, seguido de um ls, veremos que ele criou a pasta “app”.

[01:20] Mas repara uma coisa muito importante: diferente das outras vezes que criamos essa pasta através de volumes, agora ela está com um fundo verde, assim como a pasta tmp. O que será que isso quer dizer?

[01:34] Isso significa que essa pasta “/app” é temporária. Então ela está sendo escrita na memória do nosso host.

[01:44] Eu vou criar um arquivo dentro do meu diretório app, por exemplo: touch app/um-arquivo-qualquer. Vou dar um ls app/, para ver meu arquivo. Agora vou sair com exit e vou criar um novo. E se eu der um ls app/ de novo, agora não tem nada dentro dele.

[02:08] Então qual é a utilidade prática desse tipo de armazenamento que não armazena? A ideia do tmpfs é basicamente persistir dados na memória do seu host, mas esses dados não estão sendo escritos na camada de read-write. Eles estão sendo escritos diretamente na memória do host.

[02:37] Isso é importante, por exemplo, quando temos algum dado sensível que não queremos persistir na camada de read-write por questões de segurança talvez, mas queremos tê-los dentro de alguma maneira. Nesses casos podemos utilizar o tmpfs.

[02:50] Então esses dados não serão escritos na camada de read-write, e sim ficar em memória temporariamente.

[02:55] Então é uma questão de segurança que seria interessante também em alguns cenários como, por exemplo, arquivos de senha ou algum arquivo que você não quer carregar durante a execução como um todo e manter na camada de escrita.

[03:11] Então o tmpfs é basicamente isso. Ele só funciona no host Linux. Mas assim como todas as outras abordagens que já vimos, tanto de bind mount quanto de volume, ao invés de fazermos a parte de tmpfs com a flag --tmpfs, podemos utilizar também a flag --mount, seguindo uma ideia bem parecida com a do bind mount, em que definimos o tipo que vamos utilizar.

[03:43] A ideia será a mesma: basta colocar o tipo como tmpfs. E o nosso destination nesse caso é o /app dentro do nosso container: docker run –it --mount type=tmpfs,detination=/app ubuntu bash.

[03:52] Se executarmos isso e fizermos um ls, mais uma vez está o nosso “/app” temporário, porque o fundo está verde, assim como nosso tmp. Se criarmos um arquivo com touch app/um-arquivo-qualquer e fizermos um ls app/, temos nosso arquivo. Só que se criarmos um novo container de novo, não vai ter nenhuma informação dentro do nosso app.

[04:17] Então essa é a ideia do tmpfs. Caso queiramos colocar algum dado temporário que não deve ser armazenado de maneira alguma na camada de read-write, podemos utilizar o tmpfs também.

[04:30] A ideia é basicamente essa. Na questão de persistência de dados no fim das contas nós vimos três possibilidades. Temos o tmpfs, que acabamos de ver.

[04:39] Temos os bind mounts, que foi o primeiro que vimos e que fazem um bind, uma ligação direta entre o sistema de pastas do nosso host e do nosso container.

[04:52] E também os volumes, que são a solução recomendada, inclusive, para utilização, porque eles são gerenciados pelo Docker e conseguimos ter um controle maior sobre isso, sem depender diretamente da estrutura de pastas do nosso host efetivamente.

[05:11] Essa parte de persistência de dados nós terminamos por aqui. E agora vamos pensar em algumas questões mais elaboradas, como podemos fazer um grande apanhado de tudo isso que já vimos para colocar alguma aplicação mais legal em produção e ver como isso vai funcionar interagindo com outras questões também.

[05:28] Terminamos essa parte de volumes agora. Eu te vejo na próxima aula e até mais.
