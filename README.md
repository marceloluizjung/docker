**Docker**
O que é Docker?
O *Docker* é um software que *reduz a complexidade de setup* de aplicações.
Onde *configuramos containers*, que são como servidores para rodar nossas aplicações. 
Com facilidade, podemos criar *ambientes independentes* e que funcionam em diversos SO's.
E ainda deixam os projetos performáticos. 
**Por quê Docker?**
- O *docker* proporciona mais velocidade na configuração do ambiente de um dev. 
- *Pouco tempo gasto em manutenção*, containers são executados como configurados.
- *Performance* para executar aplicação, mais performático que uma VM.
- Nos livra da *Matrix from Hell*, que é a montagem de ambiente.

**Instação do docker**
Pra verificar se o docker da instalado é só dar um "docker ps" ou "docker version".

**Oque são containers?**
Um pacote de código que pode executar uma ação, por exemplo: rodar uma aplicação de Node.js, PHP, Python e etc.
Ou seja, os nossos projetos serão executados dentro dos containers que criarmos/utilizarmos.
Containers utilizam imagens para poderem ser executados. Múltiplos containers podem rodar juntos, exemplo: um para PHP e outro para MySQL.

**Container X Imagens**
Imagem e container são recursos, fundamentais do docker. 
Imagem é o projeto que será executado pelo container, todas as instruções estarão declaradas nela.
Container é o Docker rodando alguma imagem, consequentemente executando algum código proposto por ela.
O fluxo é: programamos uma imagem e a executamos por meio de um container. 
A imagem é representada pelo Dockerfile (materialização da imagem), uma imagem pode ter outras imagens como base.
A imagem tem configurações como porta de exposição como o projeto vai rodar. 
Pode-se dizer também que uma imagem é um conjunto te instruções que define como é que o container vai ser executado.

**Verificar containers executados**
O comando docker ps ou docker container ls exibe quais containers estão sendo executados no momento;
Utilizando a flag -a, temos também todos os containers já executados na máquina;
Este comando é útil para entender oque está sendo executado e acontece no nosso ambiente.
- docker run -it ubuntu: O comando it significa terminal integrado
- Ficar ligado que existe uma sequência de execução.

**Container X Vm**
Container é mais específico e não possui sistema operacional. Vm possui sistema operacional, faz mais coisas mas gasta mais recursos.

**Executar container em background**
Quando iniciamos um container que persiste, ele fica ocupando o terminal. Podemos executar um container em background, para não precisar ficar com diversas abas de terminal aberto, utilizamos a flag -d (detached).
Verificamos containers em background com o docker ps também.
Podemos utilizar o nginx para este exemplo!

**Expor portas **
Os containers de docker não tem conexão com nada de fora deles. Por isso precisamos expor portas, a flag é "-p" e podemos fazer assim: -p 80:80.
Desta maneira o container é acessível na porta 80.
Estrutura>porta_de_acesso_na_máquina:porta_do_container
Pode ser entendido como uma reflexão, a porta que ta no container > reflete na minha máquina na porta tal.

**Parando containers**
Comando: docker stop {id ou nome}

**Iniciando containers**
Aprendemos já a parar um container com o stop, para voltar a rodar um container podemos usar o comando docker start {id}. Lembre-se que o run sempre cria um novo container. Então caso seja necessário aproveitar um antigo, opte pelo start.

**Definindo nome do container**
Podemos definir um nome do container com a flag --name.

**Verificando os logs**
Podemos verificar oque aconteceu em um container com o comando logs.
Utilizamos da seguinte maneira docker logs {id}.
As últimas ações realizadas no container serão exibidas no terminal.
Para ficar monitorando o tempo todo basta add o -f. docker logs -f {id}.

**Removendo containers**
Podemos remover um container da máquina que estamos executando o docker.
O comando é docker rm {id}.
Se o container estiver rodando ainda, podemos utilizar a flag -f (force).
O container removido não é mais listado em docker ps -a.

**O que são imagens?**
Imagens são originadas de arquivos que programamos para que o Docker crie uma estrutura que execute determinadas ações em containers. Elas contém informações como: Imagens base, diretório base, comandos a serem executados, porta da aplicação e etc.
Ao rodar um container baseado na imagem, as instruções serão executadas em camadas.
Uma imagem é representada pelo Dockerfile, que é usado para criar as imagens.

**Como escolher uma boa imagem**
Podemos fazer download das imagens no docker hub.
Porém qualquer um pode fazer upload de uma imagem, isso é um problema.
Devemos então nos atentar as imagens oficiais.
Outro parâmetro interessante é a quantidade de downloads e a a quantidade de starts.

**Criando uma imagem**
Para criar uma imagem camos precisar de um arquivo Dockerfile em uma pasta que ficará o projeto.
O Dockerfile é executado em camadas, tem cache pra cada linha.
Este arquivo vai precisar de algumas instruções para poder ser executado:
- FROM: imagem base
- WORKDIR: diretório em que vai ser utilizado para executar a aplicação dentro do container.
- EXPOSE: porta da aplicação
- COPY: quais arquivos precisam ser copiados
Exemplo:
#Imagem base
FROM  node
#Diretório de trabalho (aonde é que a imagem vai ser executada)
WORKDIR  /app
#Copia os .json e cola dentro da pasta app
COPY  *.json  /app
#Instala as dependências do projeto
RUN  npm  install
#Copia tudo e cola dentro da pasta app
COPY  .  /app
#Expõe a porta da aplicação
EXPOSE  3000
#Executa a aplicação
CMD  [  "node",  "app.js"  ]

**Executando uma imagem**
Para executar a imagem primeiramente vamos precisar fazer o build.
O comando é docker build {diretório da imagem}.
Depois vamos utilizar o docker run {imagem} para executá-la.

**Alterando uma imagem**
Sempre que for alterado algo no fonte, terá que refazer o build.
Para o docker é como se fosse uma imagem nova.
Após fazer o build vamos executa-la usando o docker run.

**Camadas das imagens**
As imagens do docker são divididas em camadas (layers).
Cada instrução no dockerfile representa uma layer.
Quando algo é atualizado apenas as layers depois da linha atualizada são refeitas.
O resto permanece em cache, tornando o build mais rápido.
A sequência de execução dependendo da organização o build pode demorar mais.

**Download de imagens**
Podemos fazer o download de alguma imagem de hub e deixá-la disponível em nosso ambiente.
Vamos utilizar o comando docker pull {IMAGEM}.
A imagem está disponível para ser usada quantas vezes for necessário.

**Aprender mais sobre os comandos**
Todo comando no docker tem acesso a uma flag --help.
Utilizando desta maneira, podemos ver todas as opções disponíveis nos comandos.
Para relembrar algo ou executar uma tarefa diferente com o mesmo.
Ex: docker run --help

**Múltiplas aplicações, mesmo container**
Podemos inicializar vários containers com uma mesma imagem.
As aplicações funcionarão em paralelo.
Para testar isso, podemos determinar uma porta diferente para cada uma, e rodar no modo detached.

**Alterando o nome da imagem e tag**
Podemos nomear a imagem que criamos.
Vamos utilizar o comando docker tag {nome} para isso.
Também podemos modificar a tag, que seria como uma versão da imagem, semelhante ao git.
Para inseir a tag utilizamos: docker tag {Id_Imagem} {nome}:{tag}
Para baixar uma imagem em uma versão é só dar docker pull nome:tag

**Iniciando imagem com um nome**
Podemos nomear a imagem já na sua criação.
Vamos utilizar a flag -t.
É possível inserir o nome e a tag na sintaxe: nome:tag.
Isso torna o processo de nomeação mais simples.
Exemplo: docker build -t meunode_diferente .

**Comando start interativo**
A flag -it pode ser utilizada com o comando start também.
Ou seja não precisamos criar um novo container para utilizá-lo no terminal.
O comando é: docker start -it {container}

**Removendo imagens**
Comando: docker rmi {imagem}
Se der proflema, usar o -f pra forçar.

**Removendo imagens e containers não utilizados**
Com o comando docker system prune.
Podemos reemover imagens, containers e networks não utilizados.
O sistema irá exigir uma confirmação para realizar a remoção.


**Removendo container após utilizar **
Um container pode ser automaticamente deletado após sua utilização.
Para isso vamos utilizar a flag --rm.
o comando seria docker run --rm {imagem}.

**Copiando arquivos entre containers**
Para cópia de arquivos entre containers utilizamos o comando: docker cp
Pode ser utilizado para copiar um arquivo de um diretório para um container. 
Ou de um container para um diretório determinado.
Exemplo: docker cp node_diferente2:/app/app.js ./copia/

**Veriricar informações de processaamento**
Para verificar dados de execução de um container utilizamos: docker top {container_id}
Desta maneira temos acesso a quando ele foi iniciado, id do processo, descrição do comando.

**Verificar dados de um container**
Para verificar diversas informações como: id, data de criação, imagem e muito mais.
Utilizamos o comando docker inspect {container_id}
Desta maneira conseguimos entender como o container está configurado.

**Verificar processamento**
Para verificar os processos que estão sendo executados em um container, utilizamos o comando: docker stats
Desta maneira temos acesso ao andamento do processamento e memória gasta pelo mesmo.

**Autenticação no docker hub**
Para autenticar pelo terminal vamos utilizar o comando docker login.

**Logout do docker hub**
Comando: docker logout

**Enviando imagem para o docker hub**
Para enviar uma imagem nossa ao docker hub utilizamos o comando docker push {imagem_id}
Mas antes deverá ser necessário criar um repositório.

**Enviando atualização de imagem**
Para enviar uma atualização vamos primeiramente fazer o build.
Trocando a tag da imagem para a versão atualizada.
Depois vamos fazer um push novamente para o repositório.
Assim todas as versões estarão disponíveis para serem utilizadas.
Comando: docker push matheusbattisti/nodeteste:novaversao

**Oque são volumes?**
Uma forma prática de persistir dados em aplicações e não depender de containers pra isso.
Todo dado criado por um container é salvo nele, quando o container é removido perdemos os dados.
Então precisamos dos volumes para gerenciar os dados e também conseguir fazer backups de forma mais simples.

**Tipos de volumes**
Anônimos (anonymous): Diretórios criados pela flag -v, porém com um nome aleatório, não permite reutilização.
Nomeados (named): São volumes com nomes, podemos nos referir a estes facilmente e saber para que são utilizados no nosso ambiente.
Bind mounts: Uma forma de salvar dados na nossa máquina, sem o gerenciamento do docker, informamos um diretório para este fim.

**O problema da persistência**
Se criarmos um container com alguma imagem, todos os arquivos que geramos dentro dele serão do container.
Quando o container for removido, perderemos estes arquivos.
Por isso precisamos dos volumes.

**Volumes anônimos**
Podemos criar um volume anônimo (anonymous) da seguinte maneira: docker run -v /data
Onde /data será o diretório que contém o volume anônimo.
E este container estará atrelado ao volume anônimo.
Com o comando docker volume ls, podemos ver todos os volumes do nosso ambimente.

**Volumes nomeados**
Podemos criar um volume nomeado (named) da seguinte maneira:
docker run -v nomedovolume:/data
*Obs.: O diretório principal do comando tem que ser igual ao do workdir. O fim pode ser trocado pra qualquer lugar*

**Bind mounts**
Bind mount também é um volume, porém ele fica em um diretório que nós especificamos.
Então criamos um volume em sim, apontamos um diretório.
O comando para criar um bind mount é: docker run -v C:/dir/data:/data
Desta maneira o diretório /dir/data no nosso computador, será o volume deste container.

**Atualização do projeto com bind mount**
Bind mount não serve apenas para volumes.
Podemos utilizar essa técnica para atualização em tempo real do projeto
Sem ter que refazer o build a cada atualização do mesmo.

**Listando todos os volumes**
Com o comando: docker volume ls, listamos todos os volumes.
Desta maneira temos acesso aos anonymous e os named volumes.
*Obs.: Não lista bind mount.*

**Checkar um volume**
Podemos verificar os detalhes de um volume em específico com o  comando: docker volume inspect nome.
Desta forma temos acesso ao local em que o volume guarda.

**Remover um volume**
Podemos também remover um volume existente de forma fácil.
Vamos utilizar o comando docker volume rm {nome}

**Removendo volumes não utilizados**
Podemos remover todos os volumes que não estão sendo utilizados com apenas um comando.
O comando é: docker volume prune

**Volume apenas de leitura**
Podemos criar um volume que tem apenas permissão de leitura, isso é útil em algumas aplicações.
Para realizar essa configuração devemos utilizar o comando docker run -v volume:/data:ro
Este :ro é a abreviação de read only.

**Oque são networks no docker?**
Uma forma de gerenciar a conexão do docker com outras plataformas ou até mesmo entre containers.
As redes ou networks são criadas separadas do containers, como os volumes.
Além disso existem alguns drivers de rede, que veremos em seguida.
Uma rede deixa muito mais simples a comunicação entre containers.

**Tipos de conexão**
Os containers costumam ter três principais tipos de comunicação.
Externa: conexão com uma API de um servidor remoto.
Com o host: comunicação com a máquina que está executando o Docker.
Entre containers: Comunicação que utiliza o driver bridge e permite a comunicação entre dois ou mais containers.

**Tipos de rede (drivers)**
Bridge: o mais comum e default do Docker, utilizado quando containers precisam se conectar (na maioria das vezes optamos por este driver).
Host: permite a conexão entre um container e a máquina que está hosteando o docker.
macvlan: permite a conexão a um container por um MAC address.
none: remove todas as conexões de rede de um container.
plugins: permite extensões de terceiros para criar outras redes.

**Listando redes**
Podemos verificar todas as redes do nosso ambiente com: docker network ls.
Algumsa redes já estão criadas, estas fazem parte da configuração inicial do docker.

**Criando rede**
Para criar uma rede vamos utilizar o comando docker network create {nome}
A rede do tipo bridge é a mais utilizada.
- Definindo um driver específico > docker network create -d macvlan meumacvlan

**Removendo redes**
Podemos remover redes de forma simples também: docker network rm {nome}

**Removendo redes em massa**
docker network prune

**Conexão com o host**
Podemos também conectar um container com o host do docker.
Host é a máquina que e está executando o docker;
Como ip de um host utilizamos: host.docker.internal

**Conexão entre containers**
Podemos também estabelecer uma conexão entre containers.
"-e" significa variável de ambiente.
O host quando os containers estão na mesma rede é o nome do container.

**Conectar container**
Podemos conectar um contaier a uma rede
Vamos utilizar o comando docker network connect {rede} {container}
Após o comando o container estará dentro da rede!

**Desconectar container**
Podemos desconectar um container a uma rede também.
Vamos utilizar o comando docker network disconect {rede} {container}

**Inspecionando redes**
Podemos analisar os detalhes de uma rede com o comando: docker network inspect  {nome}

**Oque é YAML?**
Uma linguagem de serialização, seu nome é YAML aint Markup Language (YAML não é uma linguagem de marcação).
Usada geralmente para arquivos de configuração, inclusive do docker, para configurar o Docker Compose.
O arquivo .yaml geralmente possui chaves e valores.
Que é de onde vamos retirar as configurações do nosso sistema.
Para definir uma chave apenas apenas inserimos o nome dela, em seguida colocamos dois pontos e depois o valor.

**Espaçamento e identação (YAML)**
O fim de de uma linha indica o fim de uma instrução, não há ponto e vírgula.
A identação deve conter um ou mais espaços, e não devemos utilizar tab.
E cada uma define um novo bloco.
O espaço é obrigatório após a declaração da chave
**Comentários (YAML)**
Para comentar é só usar a #.
**Dados Numéricos (YAML)**
Inteiro e Float
**String (YAML)**
Yaml entende string com aspas e com aspas
**Dados nulos (YAML)**
Ou null ou ~, os dois são válidos
**Booleanos (YAML)**
On ou True, Off ou False.
**Arrays (YAML)**
Primeira: [1, 2, 3]
Segunda:
items:
- 1
- 2
- 3
**Dicionários (YAML)**
Primeira: obj: {a: 1, b: 3}
Segunda:
objeto:
	chave: 1
	chave: 2

**Oque é o Docker Compose?**
O docker compose é uma ferramenta para rodar múltiplos containers.
Teremos apenas um arquivo de configuração que orquestra totalmente esta situação.
É uma forma de rodar múltiplos builds e runs com um comando.
Em projetos maiores é essencial o uso do Compose.