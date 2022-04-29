
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

Primeiramente vamos criar um arquivo chamado docker-compose.yml na raiz do projeto.
Este arquivo vai coordenar os containers e imagens, e possui algumas chaves muito utilizadas.
version: versão do compose
services: containers/serviços que vão rodar nessa aplicação
volumes: possível adição de volumes

**Rodando o compose**
Para rodar a estrutura em compose vamos utilizar o comando: docker-compose up
Isso fará com que as instruções no arquivo sejam executadas
Da mesma forma que é realizado o build e o run
Podemos parar o compose com o ctrl+c

**Compose em background**
O compose também pode ser executado em modo detached.
Para isso vamos utilizar a flag -d no comando (docker-compose up -d)
Podemos ver sua execução com o docker ps.

**Parando o compose**
Podemos parar o compose que roda em background com: docker-compose down
Desta maneira o serviço para e temos os containers adicionados no docker ps -a

**Variáveis de ambiente**
Podemos definir variáveis de ambiente para o docker compose.
Para isso vamos definir um arquivo base em .env
As variáveis podem ser chamadas pela sintaxe: ${VARIAVEL}
Esta técnica é útil quando o dado a ser inserido é sensível/não pode ser compartilhado como uma senha.
A variável que fica no YAML é a env_file

**Redes no compose**
O compose cria uma rede básica Bridge entre os containers da aplicação.
Porém podemos isolar as redes com a chave networks.
Desta maneira podemos conectar apenas os containers que optarmos e podemos definir drivers diferentes também.

**Verificando o que tem no compose**
Podemos fazer a verificação do compose com: docker-compose ps

**Docker Swarm**
Oque é orquestração de containers?
Orquestração e o ato de conseguir gerenciar e escalar os containers da nossa aplicação.
Temos um serviço que rege sobre os outros serviços, verificando se os mesmos estão funcionando como deveriam.
Desta forma conseguimos garantir uma aplicação saudável e também que esteja sempre disponível.
Alguns serviços: Docker Swarm, Kubernetes e Apache Mesos.
Uma ferramenta do Docker para orquestrar containers.
Podendo escalar horizontalmente nossos projetos de maneira simples.
O famoso cluster.
A facilidade do swarm para outros orquestradores é que todos os comandos são muito semelhantes ao do docker.
Toda a instalação do docker já vem com Swarm, porém desabilitado.

**Conceitos fundamentais**
Nodes: é uma instância (máquina) que participa do swarm.
Manager node: Node que gerencia os demais nodes.
Worker node: Nodes que trabalham em função do manager.
Service: Um conjunto de tasks que o manager node manda o work node executar.
Task: comandos que são executados nos Nodes.

**Iniciando o Swarm**
Isso fará com que a instância/maquina vire um node e também transforma em um node manager
1 - docker swarm init --advertise-addr 192.168.0.23
2 - docker swarm init

Para sair do swarm: docker swarm leave -f  **ou só** docker swarm leave

**Listando nodes ativos**
Podemos verificar quais nodes estão ativos com: docker node ls
Desta forma os serviços serão exibidos no terminal

**Adicionando novos nodes**
Podemos adicionar um novo serviço com o comando: docker swarm join --token {TOKEN} {IP}:{PORTA}
Esta nova máquina entra na hierarquia como Worker.
Todas as ações (TASKS) utilizadas na Manager, serão replicadas em nodes que foram adicionados com join.

**Subindo um novo serviço**
Podemos iniciar um serviço com o comando: docker service create --name {nome} {imagem}
Desta forma teremos um container novo sendo adicionado ao nosso manager.
E este serviço estará sendo gerenciado pelo Swarm.
Podemos testar com o nginx, liberando a porta 80 o container já pode ser acessado.

**Listando serviços**
Podemos listar os serviços que estão rodando com o: docker service ls
Desta maneira todos os serviços que iniciamos serão exibidos.

**Removendo serviços**
Podemos remover um serviço com: docker service rm {nome}
Desta maneira o serviço para de rodar.
Isso pode significar parar um container que está rodando.

**Aumentando o número de réplicas**
Podemos criar um serviço com um número maior de réplicas: docker service create --name {nome} --replicas {numero} {imagem}
Desta maneira uma task será emitida, replicando este serviço nos workers.
Agora de fato iniciamos a orquestração.
Pode checar os status com: docker service ls
**Verificando a orquestração**
1 - Remover um container do worker
Isso fará com que o swarm reinicie este container novamente.

**Chechando token do Swarm**
Para checar o token: docker swarm join-token manager

**Checando o Swarm**
Para checar o docker swarm: docker info

**Removendo instância do Swarm**
Podemos parar de executar o swarm em uma determinada instância também.
Comando: docker swarm leave

**Removendo um node**
Podemos também remover um node do nosso ecossistema do swarm.
Comando: docker node rm {ID} -f
Aqui pode ser que dê pau, aí teria que sair do swarm e entrar novamente.

**Inspecionando serviços**
Podemos ver em mais detalhes o que um serviç possui.
O comando é: docker service inspect {ID}

**Verificar containers ativados pelo service**
Podemos ver quais containers um serviço já rodou.
O comando é: docker service ps {ID}

**Rodando compose com Swarm**
Comando: docker stack deploy -c {arquivo.yaml} {nome}

**Aumentando réplicas do Stack**
Podemos criar réplicas nos worker nodes.
Vamos utilizar o comando: docker service scale {nome}={REPLICAS}
Desta forma as outras máquinas receberão as tasks a serem executadas.

**Fazer serviço não receber mais tasks**
podemos fazer com que um serviço n;ao receba mais ordens do manager.
Para isso vamos utilizar o comando: 
1 - docker node update --availability dain {ID}
2 - docker node active --availability dain {ID}

Obs. docker node ps

**Atualizar parâmetro**
Podemos atualizar as configurações dos nossos nodes.
Vamos utilizar o comando: docker service update --image {imagem} {servico}
Desta forma apenas os nodes que estão com o status active receberão atualizações.

**Criando rede para Swarm**
A conexão entre instância usa um driver diferente, o overlay.
Podemos criar primeiramente a rede com docker network create.
E depois ao criar um service adicionar a flag --network {rede} para inserir as instâncias na nova rede.

**Conectar serviço a uma rede**
Podemos também conectar serviços que já estão em execução a uma rede.
Vamos utilizar o comando de update: docker service update --network {REDE} {NOME}

**Oque é Kubernetes - K8S?**
Uma ferramenta de orquestração de containers.
Permite a criação de múltiplos containers em diferentes máquinas (nodes).
Escalando projetos, formando um cluster.
Gerencia serviços, garantindo que as aplicações sejam executadas, sempre da mesma forma.

**Instalando o K8s no Linux**
**Master**
1 - sudo apt update
2 - sudo apt -y full-upgrade
3 - [ -f /var/run/reboot-required ] && sudo reboot -f
4 - sudo apt -y install curl apt-transport-https
5 - curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
6 - echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
7 - sudo apt update
8 - sudo apt -y install vim git curl wget kubelet kubeadm kubectl
9 - sudo apt-mark hold kubelet kubeadm kubectl
10 - sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
11 - sudo swapoff -a
12 - sudo apt update
13 - sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
14 - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
15 - sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
16 - sudo apt update
--Revisar Início--
17 - sudo apt install -y containerd.io docker-ce docker-ce-cli
18 - sudo mkdir -p /etc/systemd/system/docker.service.d
19 - sudo tee /etc/docker/daemon.json <<EOF
20 - 
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
--Revisar Fim--
21 - sudo systemctl daemon-reload 
22 - sudo systemctl restart docker
23 - sudo systemctl enable docker
24 - kubeadm init
25 - mkdir -p $HOME/.kube
26 - sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
27 - sudo chown $(id -u):$(id -g) $HOME/.kube/config
28 - kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
29 - weave reset

**Dashboard**
1- kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
2 - kubectl proxy --address 0.0.0.0 --accept-hosts '.*'

**Referência instalação kubernetes no linux**
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt
https://computingforgeeks.com/deploy-kubernetes-cluster-on-ubuntu-with-kubeadm/
https://www.gremlin.com/community/tutorials/how-to-create-a-kubernetes-cluster-on-ubuntu-16-04-with-kubeadm-and-weave-net/
https://stackoverflow.com/questions/53354734/kubernetes-dashboard-in-aws-ec2-instance
https://www.replex.io/blog/how-to-install-access-and-add-heapster-metrics-to-the-kubernetes-dashboard
https://github.com/kubernetes/dashboard/blob/master/docs/user/certificate-management.md

**Conceitos fundamentais**
Control plane: Onde é gerenciado o controle dos processos dos nodes.
Nodes: Máquinas que são gerenciadaspelo control pane.
Deployment: A execução de uma imagem/projeto em um pod.
Pod: um ou mais containers que estão em um node.
Services: Serviços que expõe os pods ao mundo externo.
kubectl: Cliente de linha de comando para o kubernetes.

**Dependências necessárias**
O kubernetes pode ser executado de uma maneira simples em nossa máquina.
Vamos precisar do client, kubectl, que é a maneira de executar o kubernetes.
E também o minikube, uma espécie de simulador de kubernetes para não precisarmos de vários computadores.

**Minikube**
Start: minkube start --driver={DRIVER}
Stop: minikube stop

**Acessando a dashboard do Kubernetes**
O Minikube nos disponibiliza uma dashboard.
Nela podemos ver todo podemos ver todo o detalhamento de nosso projeto: serviços, pods e etc.
Vamos acessar com o comando: minikube dashboard
Ou para apenas obter a url: minikube dashboard --url

**Deployment**
O deployment é uma parte fundamental do Kubernetes.
Com ele criamos nosso serviço que vai rodar nos Pods.
Definimos uma imagem e um nome, para posteriormente ser replicado entre os servidores.
A partir dessa criação do deployment teremos containers rodando.
Vamos precisar de uma imagem no hub do docker, para gerar um deployment.

**Criando deployment**
O comando é: kubectl create deployment {nome} --imagem={imagem}

**Checando deployments**
Para verificar o Deployment vamos utilizar: kubectl get deployments
E para receber mais detalhes deles: kubectl describe deployments
Desta forma conseguimos saber se o projeto está de fato rodando e também oque está rodando nele.

**Checando pods**
Para verificar os pods: kubectl get pods
E para saber mais detalhes deles: kubectl describe pods

**Configurações do kubernetes**
O comando é: kubectl config view

**Services teoria**
As aplicações do Kubernetes não tem conexão com o mundo externo.
Por isso precisamos criar um Service, que é o que possibilita expor os pods.
Isso acontece pois os Pods são criados para serem destruídos e perderem tudo, ou seja, os dados gerados neles também são apagados.

**Criando nosso service**
Para criar um serviço e expor nossos Pods devemos utilizar o comando: kubectl expose deployment {nome} --type={tipo} --port={port}
Colocar o nome igual ao do deployment já criado
O tipo do service, há vários para utilizarmos, porem o LoadBalancer é o mais comum, onde todos os Pods são expostos.
E uma porta para o serviço ser consumido.

**Gerando um ip de acesso**
Podemos acessar o nosso serviço com o comando: minikube service {nome}

**Verificando os serviços**
O comando para verificar todos é: kubectl get services
Podemos obter informações de um serviço em específico: kubectl describe services/{nome}

**Replicando nossa aplicação**
Vamos aprender agora a como utilizar outros Pods, replicando assim a nossa aplicação.
O comando é: kubectl scale deployment/{nome} --replicas={numero}
Para retornar os pods: kubectl get pods

**Checar número de réplicas**
Além do get pods e da dashboard, temos mais um comando para checar réplicas.
Que é o: kubectl get rs

**Diminuindo a escala**
Scale down: kubectl scale deployment/{nome} --rerplicas={numero_menor}

**Atualização de imagem**
Para atualizar a imagem vamos precisar do nome do container.
E também a nova imagem deve ser uma outra versão da atual.
Depois utilizamos o comando: kubectl set image deployment/{nome} {nome_container}={nova_imagem}
O manager é sempre criado antes das replicas.

**Desfazer alteração**
Para desfazer uma alteração utilizamos uma ação conhecida como rollback.
O comando para verificar uma alteração é: kubectl rollout status deployment/{nome}
Com ele e com o kubectl get pods, podemos identificar problemas.
Para voltar a alteração utilizamos: kubectl rollout undo deployment/{nome}

**Deletar um service**
Para deletar um serviço do kubernetes vamos utilizar o comando: kubectl delete service {nome}

**Deletar um deployment**
Para deletar um deployment do kubernetes vamos utilizar o comando kubectl delete deployment {nome}

**Modo declarativo**
Modo imperativo: iniciamos a aplicação com comandos
Modo declarativo: É guiado por um arquivo semelhante ao docker compose.
Desta maneira tornamos nossas configurações mais simples e centralizadas.
A linguagem utilizada é o YAML.

**Chaves mais utilizadas**
apiVersion: versão utilizada da ferramenta.
kind: tipo do arquivo (deployment, service)
metadata: descrever algum objeto, inserindo chaves como name.
replicas: número de réplicas de nodes/pods.
containers: definir as especificações de containers como: nome e imagem.

**Executando arquivo de deployment**
Comando: kubectl apply -f {arquivo}

**Parando o deployment**
Comando: kubectl delete -f {arquivo}

**Executando o serviço**
Comando: kubectl apply -f {arquivo}
Gerar IP: minikube service {name}
Para gerar o ip externo: minikube tunnel

**Parando serviço**
Comando: kubectl delete -f {arquivo}

**Atualizando o projeto no declarativo**
É só rodar o comando kubectl apply -f {arquivo} com o arquivo apontando pra tag nova.

**Unindo arquivos do projeto**
A separação de objetos para o yaml é com: ---
Uma boa prática é colocar o service antes do deployment