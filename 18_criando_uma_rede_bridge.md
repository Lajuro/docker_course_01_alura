# **Criando uma rede bridge**

[00:00] Como podemos fazer para ter uma comunicação mais estável entre containers? Porque vimos que o IP é uma coisa que não podemos garantir.

[00:10] Mas vamos ver um pouco a nossa coluna de informações sobre o container. Eu removi todos os containers com nosso comando clássico que já vimos anteriormente de docker container rm $(docker ps -aq) --force.

[00:25] Agora eu vou mais uma vez fazer docker run –it ubuntu bash e vou abrir um novo terminal. Se eu der um docker ps, que informação eu poderia ter que seria mais estável do que um IP?

[00:44] Eu poderia utilizar, por exemplo, o nome. Talvez você esteja se perguntando, e com total razão: esse nome não é gerado de maneira aleatória? Por exemplo, agora é o “angry_keller”. Como teremos isso de maneira estável, como conseguiremos identificar isso?

[01:02] Nós podemos simplesmente definir os nossos próprios nomes para os containers, porque até então nós não fizemos isso. Quem fez essa criação de nome para nós foi o próprio Docker.

[01:12] Então se eu voltar em algum dos outros terminais e der mais uma vez um docker rm com o nosso comando de remover todos os containers, o que eu posso fazer é, no momento da execução de um container, definir um nome para ele com a flag --name.

[01:31] Por exemplo, vou dar o nome de “ubuntu1” para o container: docker run -it --name ubuntu1. E eu quero executá-lo com a imagem do Ubuntu e o comando bash, então docker run -it --name ubuntu1 ubuntu bash.

[01:40] Mas isso será o suficiente para conseguirmos comunicar dois containers via host name? Não. Nós ainda precisamos dar um passo além.

[01:47] Qual vai ser esse passo? Se olharmos o nosso docker network ls, nós temos as redes que já são padrão do Docker: a bridge, a host e a none. Mas para que consigamos fazer a comunicação entre containers via host name nós precisamos criar nossa própria rede.

[02:05] E como criamos nossa própria rede? Deve ser muito difícil. Na verdade é bem fácil. Basta executarmos o comando docker network create.

[02:15] Queremos criar uma rede que faça o papel de bridge, que é a rede padrão, mas será uma própria nossa para fazer a ponte entre os containers utilizando esse driver de bridge. Então docker network create --driver bridge minha-bridge. O nome dela é o último parâmetro que é passado.

[02:35] E agora nesse momento em que vamos criar o nosso container, além de definir o nome dele, vamos definir também a rede através do --network minha-bridge.

[02:49] E repara que se voltarmos ao outro terminal, fizemos docker ps e agora inspecionarmos esse container com docker inspect, ele vai mostrar que dentro da parte de network não está mais simplesmente aquela bridge. Está a “minha-bridge”, que eu criei. Tem as outras informações dele, o IP está como 172.19.0.2 e com esse nome de “ubuntu1”.

[03:16] Vamos agora tentar criar um outro container. Vou dar um “Ctrl + L” e vamos criar um container dentro dessa mesma rede.

[03:25] Eu vou colocar um docker run -d porque não vamos nos preocupar com o terminal dele. E vou colocar o nome de --name pong, só por uma piada que vai ser engraçada e que você já vai entender, docker run -d --name pong --network minha-bridge ubuntu sleep 1d.

[03:44] Coloquei o sleep de um dia só para manter o container em execução, não vamos nos preocupar com o terminal dele. Vou dar um “Enter”. Ele criou. E agora se eu vier no terminal do meu ubuntu1, vamos fazer apt-get update de início. Ele vai fazer toda a atualização de repositórios e afins do sistema do meu container.

[04:13] Mas enquanto ele vai fazendo isso, se simplesmente fizermos um docker inspect no container que acabou de ser criado, que é o nosso pong, repara que assim como o nosso ubuntu1, ele está na rede “minha-bridge”, com um IP diferente. Mas não estamos mais nos preocupado com o IP.

[04:30] Se fizermos um docker ps agora, temos o nosso ubuntu1 e o pong. Então conseguimos definir os nomes agora, conseguimos ter um controle sobre isso. E no momento em que eu tentar agora comunicar esse meu ubuntu1 com o pong, a ideia vai ser que se eu fizer simplesmente o comando de comunicação diretamente ele deve funcionar.

[04:56] Vamos ver como está o processo de atualização e vamos ver se isso vai funcionar 100%. Quando ele terminar de fazer a atualização dos pacotes nós faremos aquele mesmo processo de antes de instalar o ping com apt-get install iputils-ping.

[05:16] O processo de instalação do ping é bem rápido também. Quando ele terminar nós faremos nosso experimento para ver se tudo vai funcionar da maneira esperada.

[05:26] Ele terminou agora, vou dar um “Ctrl + L” para limpar. E vou fazer apt-get install iputils-ping –y. O -y é para ele não pedir a confirmação.

[05:35] E agora vamos fazer o nosso teste final. Vou dar um “Ctrl + L” mais uma vez e vou fazer um ping pong. Era essa a grande piada que eu queria fazer com vocês, por isso que eu coloquei o nome de pong no container.

[05:48] E repara que ele está fazendo a comunicação para o IP inclusive do container. Ele está mostrando que é a 172.19.0.3. Se fizermos um docker ps e um docker inspect pong, veremos que é o 172.19.0.3.

[06:07] Conseguimos agora comunicar dois containers via host name com a user-defined bridge, a rede que nós definimos através de criação.

[06:17] Mas como nós saberíamos disso? Isso é um tópico muito importante que está listado na documentação, em use bridge networks. Ele fala de todos os processos, eu não tirei isso do além.

[06:28] Ele mostra que nas redes user-defined bridges, ou seja, as redes que são criadas por usuários de bridge, a diferença é que elas provém essa resolução automática de DNS entre containers, que é basicamente o que nós estamos fazendo agora.

[06:42] Então conseguimos agora comunicar diferentes containers via host name. É um pouco mais fácil manter essa comunicação agora. E vamos entender outras questões sobre, por exemplo, o que é a rede host e a rede null para complementar nosso conhecimento, e depois vamos seguindo. Por esse vídeo é só. Eu te vejo na próxima e até mais.
