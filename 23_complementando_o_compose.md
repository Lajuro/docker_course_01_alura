# **Complementando o compose**

[00:00] O que mais seria interessante saber sobre o Docker Compose? Uma coisa interessante é que no momento em que nós damos o docker-compose up, vimos que estamos subindo tudo de maneira meio indefinida.

[00:15] Mas existe uma instrução que podemos colocar, em conjunto com a documentação que eu vou deixar o link também para vocês. Nós podemos definir algumas instruções também.

[00:25] Além de todas que já colocamos, existe uma que se chama “depends_on”. Ela expressa dependência entre serviços. No momento em que colocamos uma dependência de um serviço para outro, ele vai iniciar o serviço nessa ordem específica.

[00:46] No momento em que fizermos a execução, ele vai esperar o serviço subir. Mas tem um pequeno detalhe: o depends_on não vai esperar necessariamente a aplicação dentro do container estar pronta para receber as requisições. O que ele vai fazer é esperar o container ficar pronto, o que não significa que a aplicação dentro do container já está pronta.

[01:12] No momento em que viermos no nosso VS Code falarmos que agora nossa aplicação do alurabooks depende do nosso banco de dados, nós conseguimos fazer essa definição. Então faço depends_on:, dou um “Enter”, um “Tab” e um - mongodb.

[01:31] Nós podemos agora colocar um docker-compose up no diretório mais uma vez. Antes vou salvar o arquivo no VS Code, vou dar um “Ctrl + L” no terminal e só então fazer docker-compose up.

[01:45] Ele vai fazer toda a definição. Meu mongo já está ok. E agora repara que apesar de no final ele ainda ter feito uma parte dividida entre as duas aplicações, teve uma redução em relação ao que tínhamos antes, de vários logs misturados. Nesse caso ele teve um isolamento um pouco maior.

[02:08] Como esperamos o container do mongo ficar pronto, só tivemos no final uma sobreposição de informações. Mas agora nós expressamos essa dependência entre as nossas aplicações.

[02:21] E tem um outro detalhe. Vamos dar um “Ctrl + C” mais uma vez. Nós podemos executar em modo detached, como tínhamos mencionado, então docker-compose –d up. No caso eu coloquei errado. Você tem que definir não só com o -d efetivamente, mas com up –d. Então vamos fazer docker-compose up –d. Ele vai inicializar e pronto, ele não travar o nosso terminal.

[02:49] Podemos fazer um docker-compose ps e ele vai mostrar os serviços que foram criados pelo Docker Compose de maneira mais organizada. Podemos fazer também um docker-compose down para ele remover. Ele vai fazer toda a etapa de remoção dos contêineres e da rede que foi criada.

[03:08] E só para finalizar essa definição toda de Docker Compose, o que é interessante sabermos e entendermos da documentação, para caso depois você for ler e não ficar perdido?

[03:22] Existem algumas coisas que seriam interessantes se conseguíssemos fazer, como a sessão de deploy, que permite fazer toda uma configuração de, por exemplo, número de réplicas: quantos containers de determinado serviço você quer; a parte de placement, como você vai ajustar isso a nível de paralelismo e tudo mais.

[03:43] Só que essa definição toda não funciona da maneira que estamos utilizando o Docker. Ele fala que essas configurações só tomam efeito no momento em que estamos fazendo isso com um swarm, que vai funcionar só com docker stack deploy.

[03:56] Isso significa que da maneira que estamos atualmente essas configurações, caso você tente testar na sua máquina e não funcionem, é porque você não está utilizando o Docker em modo swarm.

[04:06] Nós temos já um curso na Alura falando sobre isso, nós abordamos essas instruções com o Compose, e falamos sobre diversos detalhes também. Tem um curso da Alura só falando sobre Docker swarm.

[04:17] Sobre a parte da definição toda do Docker Compose e como ele funciona, é basicamente isso. Conseguimos subir e descer os serviços, fazer todas as nossas definições.

[04:27] Inclusive, conseguimos também fazer a utilização de volumes. Analogamente como fizemos com as redes, nós conseguiríamos definir, por exemplo, um volume para um container e fazer essa utilização também.

[04:40] Então caso você tenha alguma necessidade específica, a documentação é um lugar muito bom de se consultar. Eu falei para vocês de volumes, e podemos também fazer a utilização de volumes, com volumes -db para o que estamos definindo.

[04:55] Nós até poderíamos, por exemplo, subir uma imagem do Ubuntu e fazer sem nenhum problema como já fizemos anteriormente a definição de um serviço com um volume, com uma declaração bem parecida com a maneira que fizemos a nossa rede também.

[05:13] Essa parte toda de Docker Compose terminamos por aqui. Eu te vejo na próxima e até mais.
