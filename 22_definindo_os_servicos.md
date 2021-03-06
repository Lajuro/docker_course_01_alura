# **Definindo os serviços**

[00:00] Agora precisamos traduzir esses dois comandos que já executamos anteriormente para subir o nosso alura-books e também o comando para subir o nosso mongo. Nós vamos traduzir, por assim dizer, para essa estrutura yml.

[00:17] Seguiremos uma estrutura bem parecida com a que está na própria documentação. Vamos definir uma versão para o yml que vamos utilizar; vamos definir quais são os serviços. A diferença é que não seguiremos exatamente igual à documentação, mas grande parte será bem parecida.

[00:32] O que eu vou fazer nesse momento é abrir um novo terminal e criar uma nova pasta na área de trabalho, chamada “ymls”: mkdir Desktop/ymls. Eu vou acessá-la com cd Desktop/ymls/ e vou abrir o VS Code dentro dela. Você pode usar o seu editor de texto favorito.

[00:58] No VS Code, dentro dessa pasta eu vou criar um “docker-compose.yml”. Repara que o VS Code é inteligente o suficiente para saber que esse arquivo se trata de algo relacionado ao Docker, ele colocou até o símbolo da baleia ao lado do nome.

[01:16] Vou criar o arquivo e a ideia é que dentro desse arquivo nós configuremos o nosso yml. Como vamos definir todas as configurações? Eu vou simplesmente, como eu falei de início, definir a versão do yml que vamos utilizar, que será a 3.9, então version: “3.9”.

[01:42] E agora nós vamos definir os nossos serviços, que no fim das contas serão nossos containers. Então quais serão os nossos serviços? Nós queremos repetir o que fizemos anteriormente, de subir o alura-books e o banco de dados.

[01:56] Então eu posso simplesmente colocar services:. E nesse momento vamos definir que temos um serviço chamado mongodb, por exemplo, mas eu poderia dar o nome que eu quisesse.

[02:09] E esse serviço vai ter as peculiaridades dele. Precisamos definir a partir de agora qual é a imagem que vamos utilizar para esse serviço, se queremos dar um nome para o container, se vamos colocá-lo em alguma rede.

[02:22] Nós queremos fazer isso. Eu quero que a imagem que ele vai utilizar para esse serviço seja a do mongo na versão 4.4.6, que é a que fizemos na nossa execução. Então image: mongo:4.4.6.

[02:38] Nós também queremos dar o nome do container de “meu-mongo”. Então vamos colocar container_name: meu-mongo. E queremos que ele esteja numa rede. Não precisamos manter a minha-bridge. Eu vou colocar uma rede chamada “compose-bridge”.

[03:03] Para a definição da rede eu faço networks:, dou um “Enter”, um “Tab” e um traço, para colocarmos o elemento dessa lista. E vou colocar - compose-bridge.

[03:16] Então agora eu defini minha rede, o nome do meu container e a imagem que eu quero utilizar, que foi a mesma coisa que definimos anteriormente quando fizemos manualmente no terminal.

[03:27] Agora eu preciso fazer a mesma coisa, só que para o meu alura-books. Então vou quebrar mais uma linha, para ficar um pouco mais visível. E eu vou definir o nosso serviço chamado alura-books. E dentro dele eu vou utilizar a imagem: image: aluradocker/alura-books:1.0. Depois o nome do container, que eu vou colocar como “alurabooks”: container_name: alurabooks. Depois a rede, que precisa ser a mesma, então vou colocar compose-bridge.

[04:04] E agora também eu vou precisar colocar o mapeamento de portas que fizemos anteriormente. Para definir as portas eu coloco ports:, e faço de maneira bem parecida com a rede: dou um “Enter”, um “Tab” e um traço e coloco a porta em que minha aplicação está executando, que é a 3000. E eu quero que ela rode na minha máquina também na porta 3000, então - 3000:3000.

[04:35] Basicamente o que já definimos agora foi que o alurabooks está rodando dentro do container na porta 3000 e vai rodar no nosso host na porta 3000; definimos a imagem; a rede; e o nome.

[04:52] Agora falta um pequeno detalhe, que é configurar essa rede, porque ela não existe até então. Então o que precisamos fazer no final é, alinhado com a parte de services, colocar networks:, dar um “Enter” e definir a minha rede, que é a compose-bridge:.

[05:11] Vou dar mais um “Enter” e vou informar o driver dela, que vai ser o bridge: driver: bridge.

[Aula6_video2_imagem1]

[05:18] E agora eu simplesmente vou abrir um terminal nesse diretório que eu já tenho, e vou executar o comando docker-compose up.

[05:28] Antes de executar esse comando vou fazer um ls para garantir que eu estou nesse diretório que o meu arquivo “docker-compose” foi criado com esse nome.

[05:37] Então eu vou colocar docker compose up. E ele vai criar. Não coloquei em modo detached para entendermos o que ele está fazendo. Ele está criando o banco.

[05:53] Ele já subiu todo o banco. E também, se formos subindo, conseguimos ver que ele mostra um output bem misturado, tanto do nosso “meu-mongo” quanto do nosso “alurabooks”. Tem toda essa questão deles sendo executados.

[06:14] Agora temos garantia de que está tudo em execução. Se voltarmos ao nosso navegador e executarmos “localhost:3000”, conseguimos acessar nossa aplicação. Populei o banco com um “/seed”, e se eu atualizar a página, está tudo aparecendo.

[06:31] Mas apesar de tudo ter funcionado, ainda tem mais detalhes que podemos ver sobre como isso tudo funcionou.

[06:37] Só que antes de terminar essa aula, dentro do terminal que nós executamos e está travado, eu vou dar um “Ctrl + C”. Repara que ele vai parar os dois containers, tanto o “alurabooks” quanto o “meu-mongo”. E se voltarmos ao navegador e atualizarmos a página com “F5”, veremos que ele já derrubou.

[06:54] Mas antes de terminarmos o assunto do sobre Docker Compose, ainda teremos mais um vídeo dando alguns detalhes sobre o que aconteceu e o que podemos fazer também utilizando essa ferramenta. Eu te vejo lá e até mais.
