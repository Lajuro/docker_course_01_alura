# **Incrementando a imagem**

[00:00] Agora vamos voltar ao nosso projeto e entender algumas questões que ficaram pendentes e que poderíamos aperfeiçoar na criação do nosso Dockerfile, até mesmo em relação ao projeto.

[00:11] Primeiro vamos voltar ao nosso terminal e antes de mais nada, vamos entender um comando novo, que na verdade nem é tão novo, é a junção de dois comandos que já conhecemos. Vamos fazer docker ps e olhar que eu estou com vários containers em execução.

[00:30] Se eu quiser parar todos de uma vez, como eu faço? Eu posso colocar o comando docker stop, e eu posso simplesmente falar que eu quero parar todos os meus containers passando os IDs deles. Para fazer isso basta eu executar junto o comando docker container ls.

[00:49] Só que não tão rápido assim. Eu preciso falar que eu quero executar o comando docker container ls e usá-lo como entrada para o meu stop. Para isso eu uso docker stop $(docker container ls).

[01:01] E no fim das contas também eu preciso falar que eu quero pegar só o ID, então eu coloco a flag –q, de quiet. Assim ele pega só o ID, docker stop $(docker container ls -q).

[01:11] Vou dar um “Enter”. Ele vai ter aqueles 10 segundos para parar os containers de maneira segura, por assim dizer. E ele vai parar todos os containers a partir desse momento.

[01:22] Mas enquanto ele vai parando, o que podemos observar no nosso “Dockerfile”? Nós construímos a nossa imagem, e no momento em que executamos, o que acontece?

[01:32] Vamos mais uma vez no terminal fazer um docker run -p 8080:3000 -d danielartine/app-node:1.0. Ele rodou. E agora vamos dar um docker ps mais uma vez.

[02:01] Repara que ele está mostrando para nós o mapeamento de portas que estamos fazendo graças à flag -p. Mas e se eu executar esse mesmo container sem fazer o -p e colocar só o -d? Vamos ver o que vai acontecer. Vamos dar um docker ps de novo.

[02:21] Repare que ele não está exibindo nada na coluna de portas. E sabemos que a nossa aplicação roda na porta 3000.

[02:28] Então como é que poderíamos documentar isso para que outras pessoas que fossem utilizar o nosso container posteriormente, baseado na nossa imagem, soubessem que a aplicação está exposta na porta 3000?

[02:40] Existe na verdade uma maneira que podemos fazer essa documentação para que fique explícito em qual porta a aplicação está sendo executada. Basta colocarmos a instrução EXPOSE.

[02:57] No nosso caso, colocamos EXPOSE 3000. Nesse momento estamos falando que a nossa aplicação estará exposta na porta 3000. Isso não é obrigatório, até porque já fizemos anteriormente e funcionou esse mapeamento.

[03:09] Mas agora vamos fazer o seguinte teste: vou salvar o arquivo e gerar uma nova imagem com o comando docker build –t danielartine/app-node:1.1 .. Coloquei a versão 1.1 e o ponto no final, que é o nosso diretório atual.

[03:31] Ele está fazendo todo o processo de build. E no momento em que eu executar agora mais uma vez o container sem fazer nenhum tipo de definição de porta, vamos ver o que vai acontecer. Se eu der um docker ps, repare que ele fala que a porta 3000 está exposta.

[03:55] Então qualquer pessoa que olhar agora vai saber que a porta 3000 tem alguma aplicação dentro daquele container executando na porta 3000 do container. Então não precisamos adivinhar, e fica muito mais fácil de fazer um possível mapeamento de portas a partir daí.

[04:12] Mas mais uma vez, vamos aperfeiçoar ainda mais a nossa imagem. Vamos entender o que está acontecendo.

[04:17] Nós deixamos exposta a porta 3000. Mas o que poderíamos fazer se a nossa aplicação estivesse em um cenário diferente? Porque vimos que no “index.js” estamos definindo que a porta 3000 é efetivamente a porta da nossa aplicação.

[04:32] E se quiséssemos fazer isso no momento da criação da nossa imagem, de maneira mais parametrizada, através de uma variável de ambiente?

[04:43] Nós podemos simplesmente usar só uma sintaxe muito específica do Node, que seria colocar um process.env.PORT. PORT é o nome da variável que estamos definindo. Com isso basicamente estamos atribuindo que queremos ler uma variável de ambiente chamada PORT.

[05:07] A partir desse momento podemos definir na nossa imagem o seguinte: nós vamos querer agora receber esse parâmetro definido na nossa imagem.

[05:18] Então nós podemos simplesmente definir que nós vamos ter um argumento, que será usado para definir essa variável de ambiente dentro do nosso container posteriormente, e que será a porta que queremos utilizar. Para isso podemos fazer, por exemplo, ARG PORT=6000.

[05:39] E depois vamos colocar o EXPOSE com essa porta. E como eu pego o valor desse argumento, dessa variável que estamos utilizando dentro da criação da nossa imagem? É só colocar EXPOSE $PORT.

[05:52] Mas tem um pequeno detalhe: esse ARG só funciona em tempo de criação, de build da nossa imagem.

[06:00] E se eu quiser passar isso efetivamente para dentro do meu container que será gerado? Ou seja, se eu quero que em algum momento essa variável possa ser lida dentro do meu container, eu preciso explicitar também um outro tipo de variável de ambiente para dentro do container, que é uma ENV.

[06:19] O ARG só é usado em tempo de build da imagem, e o ENV será usado dentro do container posteriormente. Então podemos colocar também ENV PORT=$PORT.

[06:32] Essa variável ambiente PORT que nós estamos definindo para dentro do container terá um valor previamente definido por essa variável $PORT.

[06:40] Nós podemos até ser um pouco mais semânticos e trocar para ARG PORT_BUILD=6000 e ENV PORT=$PORT_BUILD, e também EXPOSE $PORT_BUILD.

[06:52] Agora vamos buildar essa imagem mais uma vez, agora na versão 1.2: docker build –t danielartine/app-node:1.2 ..

[07:05] Ele vai buildar todo o nosso processo. E agora eu vou fazer o docker run da nossa versão 1.2 sem definir nenhuma porta para ver se vai acontecer o que nós esperamos. E depois fazer um docker ps. Ele está mostrando a porta 6000.

[07:22] E agora nós já sabemos, olhando para nosso docker ps, que a porta que precisamos fazer algum mapeamento caso queiramos acessar esse container é a porta 6000.

[07:32] Então vamos fazer novamente nosso docker run -p da porta 9090 da nossa máquina, na porta 6000 do nosso container e em modo detached: docker run –p 9090:6000 –d danielartine/app-node:1.2. Vamos executar isso e voltar para nosso navegador, acessando o “localhost:9090”. Conseguimos acessar nossa aplicação mesmo assim.

[08:07] Nós conseguimos definir variáveis de ambiente para dentro do nosso container. Ou seja, conseguimos fazer a leitura dessas variáveis e colocá-las dentro do container.

[08:16] Temos também as variáveis que são explícitas, específicas para a parte de construção da nossa imagem, que é o caso do ARG. O ARG é usado para construção da imagem e o ENV é usado posteriormente dentro do container.

[08:29] E conseguimos também utilizar a instrução de EXPOSE, para ser mais semântico e deixar claro para as pessoas que vão utilizar nosso container posteriormente que a aplicação que estará ali dentro está exposta em determinada porta.

[08:42] Então conseguimos deixar a nossa imagem ainda mais fácil de ser manuseada posteriormente, além de tornar mais parametrizável através das variáveis de ambiente.

[08:53] Por esse vídeo é só. Deixamos nossa imagem agora um pouco mais robusta. E vamos entender a partir de agora como fazer o deploy dessa imagem, como colocá-la no Docker Hub. Veremos isso no próximo vídeo. Eu te vejo lá e até mais.
