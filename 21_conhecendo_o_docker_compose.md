# **Conhecendo o Docker Compose**

[00:00] Agora vamos voltar a um problema que já tivemos anteriormente, mas vamos ver o que aconteceu.

[00:06] O que nós fizemos ainda há pouco? Nós executamos aquele nosso container do aluradocker da imagem alura-books na versão 1.0 em conjunto com o mongo na versão 4.4.6.

[00:17] Para fazer isso nós precisamos de início executar o banco. O comando que executamos foi o docker run –d --network minha-bridge --name meu-mongo mongo:4.4.6. E para executar nosso container do alura-books foi através do comando: docker run –d --network minha-bridge --name alurabooks –p 3000:3000 aluradocker/alura-books:1.0.

[00:43] E nós precisamos fazer tudo isso manualmente. Nós precisamos ter definido qual era o comando que iríamos executar e definido a ordem que queríamos.

[00:54] Então vamos parar para pensar: qual foi a motivação inicial que tivemos no curso? Uma das questões é que podemos ter diversas aplicações se comunicando entre si para construir um sistema ainda mais complexo.

[01:05] Mas o que está acontecendo agora é que se nós crescermos muito a nossa aplicação, o que vai acabar acontecendo, em algum momento teremos que subir diversos containers manualmente.

[01:16] Sempre que quisermos parar um container teremos que fazer docker stop ou um docker rm para remover um a um. Então para cada container vai ser um comando que precisaremos executar, além de nos preocuparmos com toda a questão da pilha de execução que teremos com todos esses containers.

[01:32] Existe uma solução já desenvolvida pela empresa do próprio Docker que vai nos ajudar a resolver esse tipo de situação, que no caso é o Docker Compose.

[01:46] O Docker Compose nada mais é do que uma ferramenta de coordenação de containers. Não confunda com orquestração, são coisas diferentes.

[01:53] Então o Docker Compose vai nos auxiliar a executar, a compor, como o nome diz, diversos containers em um mesmo ambiente, através de um único arquivo. Então vamos conseguir compor uma aplicação maior através dos nossos containers com o Docker Compose.

[02:08] E faremos isso através da definição de um arquivo yml, aquela extensão yml, ou yaml, caso você já tenha ouvido falar. E nada mais é do que um tipo de estrutura que vamos seguir baseado em indentação do nosso arquivo.

[02:32] Nós vamos seguir mais ou menos essa receita de definir uma versão, quais serão os nossos serviços, e também como fazer toda a parte de rede e comunicação dos nossos containers, só que agora através de um único arquivo. E conseguiremos coordenar isso diretamente dos comandos de como o Docker Compose faz isso.

[02:50] Um pequeno adendo é que caso você esteja no Windows nesse momento, quando você instala o Docker você já tem nesse momento o Docker Compose.

[03:00] Então caso você execute docker-compose no seu terminal, a princípio ele vai dar o “erro”, mostrando todos os comandos que você pode executar. Ele já fala que você poderá definir e executar aplicações de múltiplos containers com o Docker Compose.

[03:22] Mas caso você esteja no Linux, como temos feito o curso desde o início, você precisará instalar o Docker Composer. Se viermos no terminal, não vamos conseguir executar nada com o Docker Compose. Ele não reconhece o comando docker-compose.

[03:45] E ele vai sugerir também a instalação através do snap ou do apt, mas nós não faremos isso. Nós vamos seguir a documentação nesse caso.

[03:51] Então eu vou abrir uma nova aba e vamos fazer o processo de instalação. Se eu digitar na barra de pesquisa “docker compose install Linux”, ele vai ter a documentação oficial que eu vou deixar para vocês também.

[04:03] E caso você esteja no Windows e a instalação não tenha acontecido por algum motivo, é só marcar na página da documentação que você está utilizando o Windows. No nosso caso, estamos utilizando o Linux.

[04:15] Para instalar é bem simples, basta copiar o comando que ele fornece e voltar ao terminal. Vou fazer “Ctrl + L” para limpar e “Shift + Insert” para colar. Vou colocar minha senha, você vai colocar a sua, claramente, e vou dar um “Enter”.

[04:30] Ele vai fazer todo o processo de baixar. E logo depois precisamos tornar o nosso Docker Compose executável, dar a permissão para ele com o comando do chmod.

[04:43] Nesse momento vou abrir um terminal novo. Se executarmos um docker-compose para executar, agora temos o mesmo output que tínhamos no Windows. Ele vai definir múltiplos containers para executar uma aplicação com o Docker.

[05:04] Agora que entendemos o que é o Docker Compose, que será essa ferramenta de composição e de coordenação de containers, precisamos transformar o que fizemos anteriormente num ambiente agora distribuído dessa maneira com o Docker Compose. Por esse vídeo nós terminamos. Eu te vejo no próximo e até mais.
