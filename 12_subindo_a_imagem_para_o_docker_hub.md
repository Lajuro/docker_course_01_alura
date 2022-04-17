# **Subindo a imagem para o Docker Hub**

[00:00] Agora vamos fazer o push da nossa imagem para o Docker Hub. O primeiro passo é que você crie sua conta na parte direita da própria home do Docker Hub. Você define seu username, seu e-mail e sua senha, aceita os termos e marca o recaptcha. Depois é só clicar em “Sign Up” e confirmar sua conta por e-mail.

[00:20] Depois que você dizer isso, no canto superior direito tem a parte de “Sign In”. Você vai colocar o seu usuário, que no meu caso é “aluradocker”, mas você terá o seu. E também a senha que você usou no momento do cadastro.

[00:32] Quando você fizer o login ele vai carregar e na parte superior, na barra de navegação, tem a parte de repositórios. Se clicarmos, veremos que nós ainda não temos nada, porque nós simplesmente já criamos nossa imagem, mas ainda não a subimos para o Docker Hub.

[00:48] E como vamos fazer isso? Vamos voltar ao nosso terminal, e o primeiro passo que precisamos fazer é autenticar a nossa conta também no Command Line Interface do Docker, para que ele saiba que somos realmente quem nós somos.

[01:03] Então faço o comando docker login -u aluradocker. O aluradocker é o meu nome de usuário. Quando você der um “Enter” ele vai pedir a senha que você usou no momento do seu cadastro no Docker Hub. Ele não vai mostrar o número de caracteres por questão de segurança, mas ele vai digitar.

[01:22] Você vai dar um “Enter” e ele vai dar um warning de que sua senha foi armazenada de maneira não criptografada nesse caminho.

[01:30] Agora vou dar um “Ctrl + L” e um docker images. Agora nós queremos simplesmente colocar a imagem “danielartine/app-node” na versão 1.0 no Docker Hub.

[01:44] Nós precisamos usar um comando específico para isso. Ao invés de ser o docker pull, vai ser o docker push, seguido do nome da imagem e sua versão. Com isso ele vai saber que ele deve fazer esse push automaticamente para o Docker Hub.

[02:02] No momento em que dermos o “Enter”, ele vai preparar todas as camadas, mas repare que ele deu um acesso negado. Isso quer dizer que nós não temos permissão para colocar essa imagem “danielartine/app-node” na versão 1.0. Mas por quê?

[02:21] Vamos lembrar daquela questão, por exemplo, do “dockersamples/static-site”. Nós temos o nome do usuário ou da organização, barra e o nome da imagem.

[02:36] E qual é o meu nome de usuário efetivamente nessa conta? É “aluradocker”. Então não faz sentido eu ter permissão de fazer um push em nome de “danielartine/app-node”. Assim como não teria se eu tivesse uma imagem “dockersamples/alguma coisa”.

[02:51] Então eu vou voltar ao meu terminal e fazer docker images mais uma vez só para visualizar. Eu quero gerar uma cópia dessa imagem, mas com uma nova tag, um novo repositório na coluna que queremos gerar.

[03:07] Para fazer isso basta executarmos o comando docker tag. Então docker tag danielartine/app-node:1.0. E em seguida eu coloco a imagem que eu quero gerar, então fica: docker tag danielartine/app-node:1.0 aluradocker/app-node:1.0.

[03:25] No momento em que eu apertar o “Enter”, ele vai fazer sem nenhum output. E se eu der um docker images de novo, agora temos o “aluradocker/app-node” na versão 1.0. Inclusive com o mesmo ID, mas agora com um repositório diferente.

[03:41] Agora eu vou tentar efetuar mais uma vez o meu push, mas agora com a versão correta, que é o repositório de aluradocker: docker push aluradocker/app-node:1.0.

[03:52] Ele vai começar a fazer o push, só que agora efetivamente, sem dar nenhum problema de acesso, porque ele consegue, a partir desse momento, fazer o meu push de maneira bem mais segura, porque ele sabe que eu sou realmente a pessoa que deveria ter essa permissão, baseado no nome de repositório que definimos para a nossa imagem.

[04:16] Enquanto ele vai fazendo o push, eu vou dar uma breve pausa no vídeo. Assim que ele terminar eu volto para seguirmos.

[04:22] Repara que agora o push terminou. Isso quer dizer que se agora formos ao Docker Hub na nossa parte de repositórios, vai aparecer a nossa imagem que acabamos de subir. Se clicarmos sobre nossa imagem, vemos a versão 1.0.

[04:44] Só que agora veremos uma coisa mais legal ainda. No terminal vamos dar um “Ctrl + L” e fazer o docker images mais uma vez. Nós temos a “danielartines/app-node” também na versão 1.2.

[04:57] Então se eu fizer um docker tag dessa imagem na versão 1.2 para “aluradocker/app-node”, também na versão 1.2, eu vou fazer um push dessa nova versão.

[05:11] Só que qual vai ser a grande sacada? Ele vai fazer o processo de novo, só que agora ele sabe que diversas dessas camadas já existem no Docker Hub, e ele só faz o push das camadas necessárias.

[05:24] Então até o Docker Hub também consegue ser inteligente nessa parte. Ela já sabe que uma camada já está lá e ele consegue aproveitar para gerar uma imagem nova com as camadas já existentes. E isso é muito legal.

[05:36] Se voltarmos ao Docker Hub e atualizarmos a página da nossa imagem, além da nossa tag 1.0, nós também teremos a nossa 1.2, ambas com OS do Linux, e mostrando que o pull de uma foi feito há um minuto e ou outro há poucos segundos.

[05:54] Agora nós aprendemos a fazer o push das nossas imagens, gerando tags novas também localmente. E vimos que o Docker Hub é capaz de reutilizar as camadas já existentes também no nosso repositório remoto. E isso é muito legal.

[06:08] Então essa parte de criação de imagens nós finalizamos agora, e vamos começar um novo tópico. Só que isso nós veremos no próximo vídeo. Eu te vejo lá e até mais.
