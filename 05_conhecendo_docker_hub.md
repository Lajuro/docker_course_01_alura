# **Conhecendo o Docker Hub [Transcrição]**

[00:0] Agora vamos entender o que o Docker fez com o `docker run`, como ele funcionou. Nós vamos começar a aprofundar essas questões do `docker run` e como ele identificou aquele “hello world”, como ele sabia o que deveria fazer naquele momento.

[00:17] Vamos voltar ao nosso terminal e executar mais uma vez o `docker run hello-world` do zero, para vermos o que acontece.

[00:26] Nesse momento o Docker fala que não encontrou essa imagem na nossa máquina, depois ele faz o download. Por fim ele finaliza e faz uma validação sha256, que vamos entender mais à frente o que significa.

[00:42] O ponto é que ele executa a saída do container que pedimos para executar, baseado naquele `hello-world` que nós passamos.

[00:51] Vamos limpar o terminal e agora vamos executar outro `docker run`. Só que ao invés de simplesmente colocar `hello-world`, que queremos descobrir de onde veio, vamos colocar, por exemplo, um nome maluco nessa sequência, sem sentido de caracteres e dar um “Enter”.

[01:09] A primeira parte foi igual, ele fala que não foi possível encontrar esse cara localmente. E depois ele dá um erro falando que ou tivemos acesso negado ou esse repositório que contém essa imagem não existe.

[01:21] Mas voltou essa questão, o que é imagem? Nós vamos responder também isso aos poucos, mas vai chegar a hora que vamos dar a resposta final.

[01:29] Mas precisamos entender que para que o nosso `docker run` funcione, ele precisa encontrar essa tal de imagem para que o container funcione. Nesse caso, quando passamos um nome maluco ele não encontrou. Mas com o `hello-world` ele encontrou.

[01:43] Então como é que o Docker sabe onde ele deve procurar e encontrar esses nomes para resolver e executar o nosso container?

[01:52] Ele até está dando uma dica para nós, de que existe um grande repositório de imagens que são essas receitas que vão executar os nossos containers, que é o chamado Docker Hub.

[02:05] Dentro do Docker Hub podemos encontrar diversas dessas imagens, que são esses parâmetros que estamos passando. Se fizermos `docker run --help`, além de todas as flags, ele mostra que o uso do `docker run` é `docker run`, seguido de algumas opções, que vamos entender quais são em breve; e o nome da imagem que queremos executar.

[02:28] Então “hello-world” é o nome de uma imagem. Aquele nome maluco que passamos também foi uma tentativa de um nome de imagem.

[02:35] Isso significa que se viermos no Docker Hub pesquisarmos, por exemplo, por “hello-world”, ele vai achar nossa imagem. Temos como resultado o “hello-world”, que tem o selo de imagem oficial e na descrição fala que é só uma imagem para exemplificar uma “dockerização” mínima, ou seja, executar um container com Docker para testarmos se está funcionando.

[02:58] A imagem ser oficial significa que ela foi feita e é mantida por um grupo confiável de pessoas que desenvolveram e têm reconhecimento da comunidade. Então ela recebe esse selo de oficial.

[03:12] Abaixo ele mostra as descrições, o que é essa imagem efetivamente, conta uma breve história sobre ela.

[03:19] Mas a questão é: se tentarmos pesquisar no Docker Hub a imagem maluca que criamos anteriormente, ele não encontra nada. Então é por isso que quando executamos o `docker run` com aquele nome maluco ele não encontrou. Mas o `hello-world` já existe.

[03:44] Então o que mais podemos fazer agora para começar a levantar algumas perguntas? Quais outras imagens são interessantes de conhecermos para darmos esse pontapé agora na parte do `docker run` e entender como isso vai funcionar?

[03:56] Existem diversas imagens que podem replicar, por exemplo, o conteúdo de um sistema operacional. Então por mais que um container não tenha necessidade de ter um sistema operacional instalado, conforme estávamos falando anteriormente, nós podemos ter um container que contém um sistema operacional, por exemplo, o Ubuntu.

[04:15] Então se pesquisarmos por Ubuntu no Docker Hub, existe uma imagem, oficial inclusive. Então ela foi criada e é mantida por um grupo de pessoas confiáveis. Quando essa imagem for executada, ela vai gerar um container baseado no Ubuntu.

[04:34] Então como podemos fazer isso agora? Vamos voltar para o terminal e dar um “Ctrl + C” para fechar e um “Ctrl + L”.

[04:44] Se executarmos o comando `docker run` ubuntu, ele vai fazer exatamente isso: ele vai no Docker Hub, baixar essa imagem e executar esse container.

[04:56] Voltando no Docker Hub, se quisermos fazer em etapas, nós podemos primeiro baixar a imagem separadamente para executá-la depois.

[05:04] Então ao invés de `docker run ubuntu` podemos fazer `docker pull ubuntu`. Ele não vai dar o output de que não encontrou localmente, porque já estamos pedindo para fazer o download. Ele vai fazer o download, vai extrair e, por fim, vai fazer aquela verificação. Mas ele não vai executar, porque nós só pedimos para ele baixar a imagem.

[05:29] E agora se pedirmos para executar efetivamente, ele não vai fazer o download, porque nós já temos a imagem localmente. Então podemos simplesmente colocar agora `docker run ubuntu` para que o container execute.

[05:39] E o que vai acontecer agora? Nada. Por que nada aconteceu? Vamos na nossa apresentação mais uma vez para entender e levantar algumas dúvidas.

[05:52] No momento em que executamos o comando `docker run ubuntu`, nós esperávamos que subisse um container com o Ubuntu dentro dele e que alguma coisa executasse, como “Bem vindo ao Ubuntu”, ou alguma coisa do tipo.

[06:04] Mas no fim das contas temos duas perguntas: por que o container não rodou? Ou será que ele roubou e nós não sabemos? Por que ele não exibiu nada para nós? São perguntas que precisamos responder.

[06:16] E também, o que o `docker run` fez por baixo dos panos agora? Já sabemos agora que ele foi no Docker Hub, buscou aquela de imagem, que é a receita para gerar um container, e executou.

[06:27] Mas como isso funciona efetivamente, para entendermos todo o fluxo e conseguirmos compreender o que estamos fazendo? Vamos responder isso no próximo vídeo. Eu te vejo lá.

