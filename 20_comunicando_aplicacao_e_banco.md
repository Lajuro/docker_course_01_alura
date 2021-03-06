# **Comunicando aplicação e banco**

[00:00] Agora vamos colocar um pouco de prática para vermos como funciona realmente a questão de comunicação de containers através da rede do Docker.

[00:10] Vamos fazer um docker images. Até então nós temos imagens que vamos utilizar a partir de agora nesse vídeo, que eu já baixei com o comando docker pull. Mas vou deixar o comando para você também baixar.

[00:20] Vou reexecutar, mas no caso ele não vai baixar porque eu já tenho, a imagem mongo na versão 4.4.6 e a “aluradocker/alura-books” na versão 1.0.

[00:34] Ênfase na versão 4.4.6 do mongo, e não na versão latest. Quando você for baixar a imagem do mongo você vai utilizar o comando docker pull mongo:4.4.6 e dar o “Enter”. Então ele fará o download dessa versão em específico.

[00:53] É a mesma coisa para a imagem alura-books. Então vai ser docker pull aluradocker/alura-books:1.0.

[01:04] Agora o primeiro passo que precisamos dar é comunicar o container que será gerado pela imagem alura-books com um banco de dados que vai ser gerado pela imagem do mongo, com um container.

[01:18] Mas como é que faremos essa comunicação? Através da rede do Docker. Então de início eu vou fazer um docker run no meu banco de dados: docker run mongo:4.4.6.

[01:31] Mas ainda faltam alguns detalhes. Por exemplo, eu não quero travar o meu terminal, então eu vou executar em modo detached com a flag -d.

[01:37] Eu vou definir que a minha rede vai ser a “minha-bridge”, que foi a rede que criamos. Se fizermos um docker network ls veremos a rede que nós já criamos.

[01:48] Caso você tenha apagado, por favor, crie sua própria bridge com o comando docker network create --driver bridge minha-bridge. Se eu executar esse comando vai dar erro, porque a rede já existe. Mas a ideia é executar esse comando, caso você tenha apagado.

[02:06] E agora o que estamos fazendo é um docker run –d com o container nessa rede: docker run -d --network minha-bridge mongo:4.4.6.

[02:13] E o ponto agora é o seguinte: o nosso container de alura-books vai se comunicar com o banco de dados mongo. E como eles estarão numa rede bridge criada por nós, ou seja, criada manualmente, a comunicação poderá ser feita via host name.

[02:27] Só que como será o host name que a nossa aplicação alura-books está buscando? Qual é o nome de banco que ela está buscando para se conectar?

[02:36] Para isso eu também vou disponibilizar para vocês o código-fonte da aplicação que foi usada como base para gerar a imagem que será usada para gerar esse container.

[02:45] Mas o que importa é que no arquivo de configuração dessa aplicação, no host ele está procurando por um host chamado “meu-mongo”. Então no momento em que essa imagem foi construída, esse arquivo estava definido dessa maneira.

[03:02] Isso significa que eu preciso que o host name, ou seja, o nome desse container, seja “meu-mongo”. Então o comando vai ficar docker run -d --network minha-bridge --name meu-mongo mongo:4.4.6. E a partir de agora, se eu der um “Enter” nesse comando, ele vai criar o container.

[03:17] E agora eu preciso fazer o run do nosso alura-books. Então docker run aluradocker/alura-books:1.0. E agora vamos adicionar os detalhes com os quais precisamos nos preocupar, como o -d; a rede, que precisa ser a mesma rede, para que os containers consigam se comunicar: docker run -d --network minha-bridge aluradocker/alura-books:1.0.

[03:43] O nome nesse caso é irrelevante, porque a aplicação está procurando pelo banco, e não o contrário. Não estou falando que sempre vai ser essa regra, mas nesse caso que estamos fazendo nós não precisamos nos preocupar com o nome desse container especificamente, então vou deixar como “alura-books”: `docker run -d --network minha-bridge --name alurabooks aluradocker/alura-books:1.0´.

[04:04] E outro detalhe também é que precisamos fazer o mapeamento de portas, que vai ser a porta 3000 na porta 3000 também do nosso container: `docker run -d --network minha-bridge --name alurabooks –p 3000:3000 aluradocker/alura-books:1.0´.

[04:16] Eu preciso fazer o mapeamento de portas, porque eu não estou e nem posso nesse caso utilizar a rede host. Eu estou utilizando a rede “minha-bridge”. Vou dar um “Enter” e ele vai executar.

[04:27] Vou abrir uma nova aba no meu navegador, e agora vamos fazer “localhost:3000”, que vai acessar a nossa aplicação. E ela tem um endpoint, o “/seed”, que vai popular o banco. E agora se atualizarmos a página, todos os dados do banco estão sendo carregados na nossa aplicação.

[04:55] Então a partir desse momento, se eu voltar ao terminal e simplesmente parar o container do meu mongo com o comando docker stop meu-mongo, os dados no navegador vão sumir, porque a comunicação com o banco parou.

[05:14] Se eu voltar ao terminal e executar docker start meu-mongo, fizer um seed novamente e recarregar a página, tudo volta ao normal.

[05:28] Então nós estabelecemos a comunicação entre dois containers que estão na mesma rede, e conseguimos ter um resultado real, bem próximo do que vemos no dia a dia de utilização de aplicações.

[05:47] Nós tivemos uma aplicação back-end, que também tem um front, se comunicando com o banco e trazendo os dados para o usuário no fim das contas.

[05:55] Só que precisamos levantar alguns questionamentos agora. Será que a melhor maneira é fazermos a inicialização de containers sempre manualmente? Porque eu tive que me preocupar em fazer o docker run de um, depois o docker run do outro.

[06:09] Será que quando vamos fazer as coisas realmente em produção nós sempre subimos tudo na mão? É um ponto sobre o qual precisamos pensar. Só que veremos isso nas próximas aulas. Eu te vejo lá e até mais.
