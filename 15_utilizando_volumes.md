# **Utilizando volumes**

[00:00] A segunda solução, que inclusive é a mais recomendada para se usar em ambientes produtivos e afins pelo Docker, é a utilização de volumes.

[00:08] Se olharmos a imagem que está presente na documentação, ele mostra que a utilização de volumes é uma área gerenciada pelo Docker dentro do seu file system.

[00:17] Então por mais que no fim das contas as nossas informações continuem dentro do nosso host original para ser persistidas, nós teremos uma área que o Docker vai gerenciar e é muito mais segura a nível de alguém mexer e fazer alguma loucura ali dentro, porque será gerenciada pelo próprio Docker.

[00:33] E como criamos um volume inicialmente? Vamos voltar no nosso terminal. Não estou com nenhum container em execução.

[00:41] Existe, dentre os diversos comandos que temos no Docker, um comando chamado docker volume. Podemos até dar um docker volume ls, para vermos que não temos nenhum criado. Nós podemos simplesmente criar. Eu posso dar um docker volume create e colocar em seguida nosso meu-volume.

[01:02] Quando eu der esse comando, ele vai criar, e se dermos um docker volume ls, ele mostra nosso volume, usando nosso driver local do nosso host, com o nome que demos.

[01:13] Mas onde é que ele está na nossa máquina? Como é que eu sei que ele vai gravar essas informações? Nós vamos chegar lá.

[01:19] Mas antes vamos fazer o mesmo experimento que fizemos anteriormente. Eu vou executar o docker run com a flag -v, como fizemos da maneira original. Só que ao invés de colocarmos o mesmo caminho de antes, eu não quero mais definir nenhum diretório dentro da minha máquina manualmente.

[01:40] Então eu vou simplesmente explicitar que eu quero utilizar o “meu-volume”, que é o nome do meu volume, e ele será mapeado nesse meu diretório “/app” dentro do meu container, docker run –it –v meu-volume:/app ubuntu bash. Vou dar um “Enter” e um ls. Vou entrar no meu /app mais uma vez.

[02:00] Ele está vazio, porque repara que por mais que o /app seja igual, agora nós estamos utilizando um ponto dentro do nosso host diferente. Antes estávamos utilizando o diretório na nossa home, mas agora estamos usando um novo volume, que é esse “meu-volume” gerenciado pelo Docker.

[02:15] Mas se seguirmos a mesma receita, vamos criar um arquivo qualquer com touch arquivo-qualquer.txt. Vamos criar um novo container, seguindo o mesmo comando: docker run –it –v meu-volume:/app ubuntu bash. Se eu fizer agora um cd app/ e um ls, temos agora o nosso arquivo qualquer.

[02:32] Então tudo continua funcionando. Mas a pergunta que precisamos responder agora é: onde está esse arquivo? Porque antes nós sabíamos que se viéssemos na nossa home e acessássemos a pasta “volume-docker” ele estaria dentro dela.

[02:47] Mas esse meu volume está aonde? Vamos descobrir esbanjando conhecimento para conseguirmos distribuir para outras pessoas também e mostrar o que sabemos, porque é importante sabermos disso.

[03:00] Eu vou entrar com o super usuário, fazendo sudo su e colocar minha senha. Agora existe um diretório onde o Docker está realmente na nossa máquina. Não o Docker em si, mas diversas informações que ele armazena na nossa máquina. Ele grava em “/var/lib/docker/”.

[03:23] Se dermos um ls, nós temos diversas informações, como plug-ins, buildkit, imagens, overlay, e inclusive volumes. Se fizermos cd volumes/, nós encontramos o “meu-volume”.

[03:37] Então se eu fizer um cd meu-volume/, ele vai ter um hash doido, dentro dessa pasta de data, e dentro dele estará o nosso arquivo qualquer.

[03:46] Então nós sabemos agora onde os nossos arquivos estão, porque agora por mais que eles estejam ainda dentro desse caminho, eles estão num lugar completamente gerenciado pelo Docker. Então conseguimos utilizar os comandos do Docker para gerenciar esse volume.

[04:02] Se sairmos do modo de super usuário e fizermos docker volume simplesmente sem passar nada, ele vai mostrar que conseguimos criar volumes, inspecioná-los, listá-los, remover os que não estão sendo usados, remover independentemente se estiver sendo usado ou não.

[04:18] Então conseguimos gerenciar esses volumes agora através da interface do Docker. Não ficamos 100% dependentes do nosso sistema de arquivos do nosso sistema operacional. E sim o Docker vai gerenciar isso para nós agora.

[04:31] Isso é muito interessante, porque agora não dependemos diretamente de uma estrutura de pastas específicas do nosso sistema operacional. Ele estará sempre nesse diretório de volumes.

[04:43] E por fim, para finalizar essa parte da criação de volumes, mais uma vez vamos olhar na documentação. Também temos a possibilidade de criar um volume com a flag --mount.

[04:54] E é até mais fácil nesse caso, porque por padrão ele já assume que o tipo que vamos criar é um volume. Então não precisamos colocar o tipo, como fizemos com o bind.

[05:04] Então vamos voltar ao terminal e executar o comando de criação de um container. Vamos colocar o --mount, sem o type=bound, porque não é mais necessário. E a source será o meu-volume, e o target continua para “/app”, docker run -it --mount source=meu-volume, target=/app ubuntu bash. Se fizermos o ls dentro de /app, temos o nosso arquivo qualquer.

[05:31] E ainda tem uma graça dos volumes também que é o seguinte: vamos criar mais um container, mas agora vou colocar, por exemplo um meu-novo-volume em source, que é um volume que eu não tenho criado até então. Ele vai fazer isso automaticamente para nós.

[05:45] Se eu der um ls app/ vai estar vazio, porque eu estou usando um volume novo. Mas se eu sair desse container agora e der um docker volume ls, vemos que ele criou já esse volume automaticamente.

[05:59] Então conseguimos ter esse controle também e o Docker vai nos ajudar nesse sentido. Então não precisamos se preocupar necessariamente em criar, porque como é gerenciado pelo Docker ele pode fazer isso por nós. E isso é muito interessante.

[06:13] Agora já vimos as duas principais formas de criar maneiras de persistir dados, tanto bind mount como com os volumes em si gerenciados pelo Docker. Mas ainda falta uma terceira forma, que eu vou colocar direto na URL da documentação, que são os tmpfs.

[06:35] Basicamente o nome já indica uma coisa bem peculiar, mas veremos isso no próximo vídeo. Eu te vejo lá e até mais.

## Comando do volume

Segue o comando abaixo da primeira maneira com a flag `-v`:

```powershell
docker run -it -v meu-volume:/app ubuntu bash
```

E o comando abaixo da segunda maneira com a flag `--mount`:

```powershell
docker run -it --mount source=meu-volume,target=/app ubuntu bash
```

Por padrão, o comando `--mount` assume que o tipo é volume. Então não precisamos colocar o tipo, como fizemos com o bind.