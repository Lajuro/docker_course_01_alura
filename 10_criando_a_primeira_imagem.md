# **Criando a primeira imagem**

[00:00] Agora vamos criar nossa primeira imagem. Vimos o que é uma imagem, como ela vira um container, qual a diferença de imagem para container.

[00:09] Mas precisamos entender agora como criar nossa imagem efetivamente para não dependermos 100% de imagens de outras pessoas diretamente. Nós vimos na nossa apresentação que precisamos no fim das contas seguir esse fluxo.

[00:23] Nós precisamos definir esse arquivo que é o Dockerfile. E a partir dele vamos criar nossa imagem. E imposta nossa imagem basta executar usando run para que o container seja gerado a partir da imagem.

[00:37] Voltando ao nosso projeto como um todo, nós temos uma aplicação Node. Não precisa se preocupar, nós não vamos entrar em nenhum detalhe específico de Node e de nenhuma linguagem de programação, você não precisa saber Node.

[00:53] Só estamos usando como exemplo para termos uma aplicação efetivamente para empacotar e transformar numa imagem e depois num container. Não precisa se preocupar quanto a isso.

[01:04] O que nós queremos no fim das contas é que quando formos executar nosso container e acessarmos via host, por exemplo, mapeando as portas, que tenhamos essa visualização, que é a nossa aplicação realmente em execução.

[01:15] Mas não queremos simplesmente clicar duas vezes no arquivo e abrir. Nós queremos um servidor que disponibiliza essa aplicação para nós. Então nós precisamos de alguma maneira colocar todo esse conteúdo dentro de uma imagem, instalar o Node, que será responsável por executar o servidor.

[01:32] E no fim das contas, quando nosso container executar, queremos que ele execute algum comando que mantenha esse servidor em execução.

[01:38] Então o que precisamos fazer de início é o seguinte: eu estou utilizando o Visual Studio Code para fazer a edição de texto nesse caso, mas você pode usar o da sua preferência.

[01:49] O que vou fazer é criar um novo arquivo dentro da nossa pasta do nosso exemplo, que estará disponível para você fazer o download. E dentro dessa pasta vou criar um arquivo chamado “Dockerfile”, que é basicamente o arquivo que nós vamos criar. E vou dar um “Enter”.

[02:14] Repara na parte superior esquerda que o VS Code tem esse charme de reconhecer que é um arquivo Dockerfile. E agora nós vamos simplesmente, dentro desse arquivo, definir como vai ser a criação da nossa imagem. O que nós queremos fazer?

[02:30] Nós queremos que dentro do nosso projeto como um todo nós tenhamos o Node para que consigamos rodar um servidor.

[02:46] Então se queremos usar o Node como base para nossa aplicação, nós podemos pegar emprestado do que já desenvolveram. Então vamos fazer o pull dessa imagem já existente para que possamos utilizar no nosso projeto, e a partir daí só fazer as nossas modificações para customizar o projeto à nossa maneira.

[03:09] No fim das contas nós precisamos do Node. Mas como nós colocamos o Node dentro da nossa imagem por padrão? Nós podemos colocar a princípio um Ubuntu, e dentro desse Ubuntu podemos instalar o Node e fazer toda a configuração necessária.

[03:26] Mas lembra que não precisamos ter necessariamente um sistema operacional dentro do nosso container. Nós podemos simplesmente utilizar alguma imagem que disponibilize o Node para nós, por exemplo, a própria imagem do Node no Docker Hub, que é uma imagem oficial, inclusive.

[03:43] Se olharmos a descrição como um todo, tem todas as versões do Node que nós podemos definir, como as versões 16, 17, 14, 12.

[03:53] Então o que nós podemos fazer nesse cenário? Nós podemos simplesmente falar que queremos pegar uma dessas versões do Node para que possamos executar o nosso projeto, usar essa imagem como base para a nossa. Então a partir da imagem que nós vamos definir nós vamos começar a usar a nossa.

[04:15] Como podemos pegar essa imagem emprestado? Por exemplo, queremos usar o Node na versão 14, então dentro do nosso “Dockerfile” eu quero pegar a partir do Node na versão 14. Como eu explicito a versão? Utilizando dois pontos e a versão que eu quero: FROM Node:14. Então a partir do Node na versão 14.

[04:40] Como eu sei que é a versão 14? Porque na documentação da imagem do Node ele está mostrando quais são as tags suportadas, inclusive a 14. E a partir do Node na versão 14, o que nós queremos fazer? Queremos colocar todo o nosso projeto, que são esses arquivos, menos o próprio “Dockerfile”, dentro dessa imagem. Então nós queremos copiar esse conteúdo do nosso host para a nossa imagem.

[05:18] Para isso podemos simplesmente colocar COPY. Nós queremos copiar todo o conteúdo do nosso diretório atual. Em que diretório está o nosso “Dockerfile”? No diretório “exemplo.node”.

[05:30] Então todo o conjunto do nosso diretório atual nós queremos copiar para algum diretório dentro do nosso container, por exemplo, para uma pasta chamada “/app-node”, só para termos a distinção do que nós queremos fazer: COPY . /app-node.

[05:42] Então a partir desse momento nós estamos copiando esse conteúdo do diretório do nosso host para o diretório de dentro da nossa imagem que vai virar um container, chamada “/app-node”.

[05:58] Nós queremos executar o comando RUN npm install. Só que esse comando terá que ser executado dentro do nosso diretório /app-node, para que consigamos instalar as dependências da nossa aplicação.

[06:11] Caso você não conheça Node, esse comando está sendo responsável só por instalar as dependências que o nosso projeto precisa em um projeto Node. Então basicamente estamos instalando as dependências e o Node está resolvendo isso automaticamente.

[06:24] E por fim nós queremos que o ponto de entrada do nosso container, ao executar esta imagem e começar a ter seu container devidamente em execução, seja startar a aplicação, então eu faço ENTRYPOINT npm start.

[06:40] E isso também tem que ser executado dentro desse diretório /app-node. Só que nós teríamos que ficar passando em todos os lugares o “/app-node”. Será que podemos resolver isso de uma maneira mais simples?

[06:55] Eu quero que, por exemplo, esses comandos todos, por padrão, sejam executados no meu diretório que eu estou atualmente. E como é que eu defino o diretório que a imagem vai tratar como padrão? Qual será o meu diretório de trabalho, por assim dizer?

[07:10] Para isso eu tenho a instrução WORKDIR, e com ela podemos definir o nosso diretório padrão: WORKDIR /app-node.

[07:21] Inclusive, no nosso COPY eu posso fazer um COPY de ponto. Esse ponto é o nosso diretório atual dentro do nosso host, para ponto também, que vai ser o nosso diretório atual dentro da nossa imagem: COPY . .. E qual será nosso diretório atual? O nosso /app-node, que foi definido através do nosso WORKDIR.

[07:44] Então o que nós estamos fazendo? Nós estamos definindo que vamos utilizar imagem do Node na versão 14 como base para nossa imagem. E nós vamos definir o nosso diretório de trabalho padrão como sendo o /app-node.

[07:58] Vamos copiar do diretório atual, onde está o nosso “Dockerfile” do nosso host, que é a pasta “exemplo-node”, para a pasta atual dentro da nossa imagem “/app-node” que foi definida dentro do nosso WORKDIR.

[08:14] E vamos executar o comando npm install enquanto a imagem estiver sendo criada. Esse comando será executado na etapa de criação da imagem. Então esse npm install será executado enquanto a imagem estiver sendo criada.

[08:26] E quando o container for executado a partir dessa imagem, o comando executado vai ser o npm start. Vamos dar um “Ctrl + S” agora, vamos ao nosso terminal e vamos acessar cd Desktop/exemplo-node/.

[08:45] Como é que a partir desse Dockerfile eu posso gerar uma imagem? Através do comando docker build.

[08:54] Também passamos o -t para podermos criar um nome, etiquetar nossa imagem. No caso vou colocar o meu nome, então docker build -t danielartine/app-node:1. Com o :1 nós podemos explicitar qual é a versão que estamos criando. Eu vou colocar a versão 1.0 só para ficar mais bonito. Então docker build ´t danielartine/app-node:1.0.

[09:18] Em qual contexto tudo isso terá que ser executado? No contexto de diretório atual, ou seja, ponto, que é a referência ao diretório atual: docker build -t danielartine/app-node:1.0 ..

[09:26] Eu dou um “Enter”, e no Docker Hub, nesse exato momento, ele vai pegar a imagem do Node na versão 14 e baixar. Então ele vai pegar todo esse conteúdo para a nossa máquina, como já vimos que o Docker faz, e vai construir uma nova imagem utilizando essa como base.

[09:47] Então no momento em que isso terminar nós vamos executar o comando docker history para ver o que ele vai fazer no fim das contas e ver como essa imagem vai se comportar dentro do nosso sistema.

[09:58] Com o que precisamos nos preocupar agora? Fazendo um breve apanhado no nosso Dockerfile, ele está na etapa FROM Node:14, onde ele foi no Docker Hub e pegou a imagem do Node na versão 14. É isso que ele está fazendo agora.

[10:15] Mas um ponto interessante: você pode me perguntar como eu sei dessas instruções, como eu as deduzi. Essa é uma pergunta muito boa.

[10:22] Nós podemos entender tudo isso através da própria documentação do Docker, que eu vou mostrar para vocês. É uma documentação muito completa, na qual podemos e devemos sempre nos basear para seguir os nossos projetos e criação de imagens.

[10:38] Nós temos todas as principais instruções para a criação de uma imagem. Ele mostra os comandos e as principais instruções. Ele tem o FROM, que usamos agora há pouco; ele mostra como todas as sintaxes funcionam, como escapar caracteres.

[10:57] Temos o ADD, o COPY. Nós ainda não vimos algumas, mas veremos, por exemplo, o ENV, o EXPOSE. Já vimos o FROM. Com o LABEL podemos etiquetar e colocar algumas labels na nossa imagem; podemos definir algumas questões de volume, que ainda não sabemos o que é; o WORKDIR, que já vimos.

[11:15] Ele tem diversos exemplos que podemos ver como funcionam dentro da documentação e aplicar aos nossos projetos. Então vou deixar também o link da documentação nas atividades para vocês conseguirem ver como é que funciona.

[11:29] Mas ainda teremos outros exemplos de criação de imagens. Esse é só o primeiro para entendermos realmente como vai funcionar.

[11:35] Voltando para o terminal, ele está terminando de extrair nesse momento as últimas camadas dos downloads que ele fez da imagem do Node. Então vamos ver qual vai ser o resultado final.

[11:53] Ele está agora na etapa de WORKDIR, depois copiando os arquivos, executando o npm install. E por fim, no ENTRYPOINT ele definiu o npm start. Agora vou limpar o nosso terminal e vou fazer docker images. Olha o que temos agora.

[12:09] Temos “danielartine/app-node” na versão 1.0 e temos o ID dessa imagem. E se agora eu simplesmente fizer um docker run nessa imagem “danielartine/app-node” e fizer um mapeamento?

[12:27] Lembra que nós definimos a nossa aplicação dentro do container, mas ela é isolada? Então como eu posso agora saber em qual porta essa aplicação está rodando dentro do meu container?

[12:40] A princípio nós precisaríamos ser um pouco malandros. Se olharmos dentro do nosso “index.js”, veríamos que ela está sendo executada na porta 3000. Tem um breve problema que precisaremos resolver. Mas vamos colocar isso no terminal.

[12:55] Na nossa máquina nós vamos querer na porta 8080 de novo, mas nós queremos que a porta 8080 reflita na porta 3000, que é onde vimos que nossa aplicação vai ficar em execução dentro do nosso container: docker run –p 8080:3000 danielartine/app-node.

[13:13] Vou colocar também um -d para ficar em modo detached. E faltou especificar a versão, que é a 1.0, então docker run -d -p 8080:3000 danielartine/app-node:1.0.

[13:25] Na verdade ele deu um problema porque a porta 8080 já está em uso por causa dos nossos exemplos anteriores. Obviamente não podemos usar a mesma porta, então vou mudar para 8081.

[13:35] E agora se viermos no nosso navegador e tentarmos acessar o “http://localhost:8081”, está tudo funcionando, conseguimos acessar a nossa aplicação agora de maneira conteinerizada.

[13:50] Então nós criamos nossa própria imagem e executamos um container a partir dela. Isso é muito legal.

[13:56] Mas ainda tem algumas questões que precisamos resolver. Nós deixamos em aberto aquela questão de como saber em qual porta nossa aplicação estava em execução, como sabemos como expor ou não expor.

[14:07] Tem algumas questões que precisamos deixar menos obscuras para o nosso Dockerfile, para que consigamos deixar tudo muito mais fácil de ser entendido.

[14:18] Mas vamos terminar esse vídeo por aqui. Nós criamos nossa primeira imagem, mas precisamos entender mais alguns detalhes acerca da criação de imagens. Mas por esse vídeo é só. Eu te vejo na próxima e até mais.
