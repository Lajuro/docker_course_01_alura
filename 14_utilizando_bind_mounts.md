# **Utilizando bind mounts**

[00:00] Agora nós vamos entender como utilizar a primeira solução que o Docker disponibiliza para persistência de dados, que se dermos uma olhada na documentação, são os bind mounts.

[00:14] Ele vai fazer basicamente o bind, uma ligação entre um ponto de montagem do nosso sistema operacional e algum diretório dentro do container. Vamos entender agora como isso vai funcionar.

[00:27] Eu vou parar mais uma vez os containers com o comando de docker rm $(docker container os -aq) --force. E agora vamos executar mais uma vez aquele docker run –it ubuntu. E a questão agora é a seguinte: o que podemos definir no momento em que vamos executar um container?

[00:53] Eu posso informar que quando esse container for criado e executado eu quero que as informações persistidas em determinado diretório dentro dele sejam persistidas em algum diretório na minha máquina local mesmo, no meu host.

[01:06] Então além de definir os comandos básicos que já definimos e a flag de -it também, eu posso colocar uma flag de -v.

[01:16] Vamos ver o que essa flag faz. Eu vou criar uma nova pasta para esse caso específico. Já estou na minha home, vou criar um pasta com o comando mkdir, chamada volume-docker. Pode ser o nome que você quiser criar para essa pasta.

[01:40] E agora, voltando à nossa execução, eu quero que esse diretório que esteja na minha pasta “/home/daniel/volume-docker” corresponda a um determinado caminho dentro do meu container.

[01:59] Então eu coloco dois pontos e informo que, por exemplo, dentro do container eu terei um diretório chamado “/app”, e tudo que for gravado dentro desse diretório será persistido nesse diretório no meu host, docker run –it –v /home/daniel/volume-docker:/app Ubuntu bash.

[02:13] Vamos ver como isso vai funcionar. Eu vou colocar ainda um bash no final e dar um “Enter”. Estou dentro. Se eu der um ls agora, repara que ele tem esse diretório “/app”. Agora vou acessar com cd app/. E vou criar um arquivo com touch arquivo-qualquer.txt. Vamos ver o que vai acontecer.

[02:43] Se eu simplesmente abrir o gerenciador de arquivos e entrar na pasta “volume-docker”, está ali o meu “arquivo-qualquer.txt”.

[02:52] Então eu consegui fazer essa definição de colocar um caminho dentro do meu diretório da minha máquina local para um diretório dentro do container e salvar esse arquivo.

[03:03] Mas como isso vai funcionar agora? Eu quero parar esse container. Vou dar um “Ctrl + D” e vou criar um novo container, definindo o mesmo bind mount, o mesmo caminho na minha máquina para esse diretório “/app”.

[03:17] E vai ser um novo container, porque estamos dando um novo run, então sabemos que será uma nova camada de read-write para esse container: docker run –it –v /home/daniel/volume-docker:/app ubuntu bash. E vou dar um “Enter”.

[03:27] Se agora eu der um ls, repare que eu vou continuar tendo minha pasta “/app”. E se eu der um cd app e um ls em seguida, o meu “arquivo-qualquer.txt” ainda aparece.

[03:38] Então conseguimos agora persistir informações entre containers. Caso um container pare de funcionar de alguma maneira e queiramos persistir os dados que estejam lá, já conseguimos fazer isso agora, e de maneira a princípio prática.

[03:50] Nós só definimos um diretório dentro do nosso host para um diretório do nosso container e está tudo feito, 100% funcionando. É muito fácil e prático nesse sentido.

[03:59] Mas qual é a outra maneira que podemos fazer e que inclusive vem sendo mais recomendada pelo Docker para criação de volume?

[04:07] Mais uma vez, em conjunto com a documentação, repara que a maneira que estamos utilizando é com a flag -v.

[04:14] Mas vem sendo recomendado, por ser mais semântico, a utilização além da flag –v, a flag --mount. Vamos pegar um exemplo para ver o que ela faz.

[04:26] No terminal vou dar um “Ctrl + D” de novo e vou criar um terceiro container agora, só para vocês verem que eu não estou roubando, não estou com nenhum container execução.

[04:34] Vamos criar o terceiro container agora utilizando essa flag --mount. Como é que ela funciona? No nosso caso vamos fazer um mount do tipo bind, porque é um bind mount. E a nossa source, o diretório da nossa máquina, vai ser mais uma vez, no meu caso, docker run –it --mount type=bind,source=/home/daniel/volume-docker,target=/app ubuntu bash. E o meu target será um “/app” também dentro desse container.

[05:07] Vou dar um “Enter”. Deu um erro, vou ver o que eu errei. Ficou o –v sobrando, nós não precisamos mais dele. Então vou tirar e dar um “Enter”.

[05:28] Está dando erro de novo, foi porque eu escrevi meu nome errado, acontece. Vou arrumar, e agora sim.

[05:39] Isso é até uma coisa interessante: se o diretório que você estiver tentando utilizar não existir no seu host, a flag --mount vai falar que esse caminho não existe. Não foi ensaiado, mas é bom pegarmos esses erros, porque vamos pegando esses possíveis cenários.

[05:53] Agora dando um “Enter” tudo funcionou. Se eu der um ls tenho o meu app. E seu eu der cd app/ e em seguida um ls, aparece o meu arquivo.

[06:03] Então tudo continua funcionando, utilizando tanto da maneira com a flag --mount quanto com a flag –v. Conseguimos agora persistir os dados entre os containers e também entre os próprios containers nas execuções seguintes para que os dados sejam persistidos caso seja necessário.

[06:20] Se tiver algum arquivo de configuração, que a sua aplicação precisa executar e coisas afins, nós conseguimos ter isso agora.

[06:26] Nós veremos alguns exemplos mais robustos posteriormente, mas até então vamos entender os conceitos primordiais que baseiam toda a utilização de volumes, bind mount e tmpfs.

[06:41] Mas vamos ficar com a pulga atrás da orelha no final dessa aula com o seguinte questionamento: será que é interessante o nosso container depender de um caminho dentro do nosso host?

[06:52] Pode ser que nós escrevamos como aconteceu agora, de um caminho não existir e dê algum problema; ou não tenhamos permissão para acessar; ou alguém simplesmente delete esse caminho localmente, porque ele estará no host.

[07:06] Então são N cenários que podem acontecer e que devemos nos preocupar. E para isso vamos conseguir utilizar uma solução ainda mais robusta e que é mais recomendada pelo Docker, que são os volumes em si, que serão gerenciados pelo próprio Daemon do Docker. Mas isso veremos no próximo vídeo. Eu te vejo lá e até mais.

## Comando executado para persistência de dados

Foi executado o comando abaixo:

```powershell
docker run -it -v C:\Users\rober\Desktop\Programming\Alura\Docker\14_utilizando_bind_mounts\:/app ubuntu bash
```

Além disso, utilizando a forma mais recomendada, ficou da seguinte forma:

```powershell
docker run -it --mount type=bind,source=C:\Users\rober\Desktop\Programming\Alura\Docker\14_utilizando_bind_mounts\,target=/app ubuntu bash
```