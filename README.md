<div align="Center"> 
<br>

<h4>

██████╗░░█████╗░░█████╗░██╗░░██╗███████╗██████╗░
██╔══██╗██╔══██╗██╔══██╗██║░██╔╝██╔════╝██╔══██╗
██║░░██║██║░░██║██║░░╚═╝█████═╝░█████╗░░██████╔╝
██║░░██║██║░░██║██║░░██╗██╔═██╗░██╔══╝░░██╔══██╗
██████╔╝╚█████╔╝╚█████╔╝██║░╚██╗███████╗██║░░██║
╚═════╝░░╚════╝░░╚════╝░╚═╝░░╚═╝╚══════╝╚═╝░░╚═╝
</h4>
</div>

----

<details>
  <summary><b> 1. Fundamentos</b></summary>
<div align="Left"> 
<br>

D1.1 - O Que é o "Docker"?  
 > - Plataforma de software que permite a criar, empacotar e executar aplicações de forma isolada em contêineres. 

D1.2 - O que são "Contêineres"?  
 > - Ambientes isolados, leves e portáteis que garantem a funcionalidade em diferentes sistemas. 

D1.3 - Componentes do Docker  
 > - Docker Engine: Núcleo do Docker - cria e gerencia contêineres;  
 > - Docker CLI (docker): Interface de linha de comando;
 > - Docker API: Interface REST para controlar o Docker;
 > - Imagens Docker: Modelos para criar contêineres;
 > - Contêineres: Instâncias executáveis de imagens;
 > - Dockerfile: Script que define uma imagem;
 > - Redes Docker: Comunicação entre contêineres;
 > - Volumes Docker: Persistência de Dados;
 > - Docker Compose: Gerenciamento de Múltiplos Contêineres;
 > - Docker Desktop: Interface gráfica e ambiente completo para desenvolvimento;
 > - Docker Hub / Registry: Repositório de imagens Docker;
 > - containerd / runc: Execução de Contêineres em baixo nível. 

D1.4 - Diferença entre Docker Desktop e Docker Engine  
 > - Docker Desktop: Desenvolvimento Local em Windows /macOS - Possui GUI;
 > - Docker Engine: Núcleo do Docker, roda direto no Linux sem virtualizar - ambientes de produção, servidores e Linux -, apenas CLI.

D1.5 - Diferença entre VM e Contêiner  

 > | Virtual Machine                                | Contêiner                                              |
 > |------------------------------------------------|--------------------------------------------------------|
 > |Isolamento Total - Sistema Operacional Completo | Isolamento Parcial - Usa o Kernel do Host              |
 > | Ocupa mais memória e CPU                       | Usa menos recursos                                     |
 > | Inicialização lenta (Minutos)                  | Inicialização Rápida (segundos / milissegundos)        |
 > | Imagens são Grandes (GBs)                      | Imagens Pequenas (MBs ou poucos GBs)                   |
 > | Execução de múltiplos SOs                      | Execução rápida de aplicações isoladas / microserviços |
 > | Usa hypervisores (VirtualBox, VMware, Hyper-V) | Usa container engine (Docker, containerd)              |   

D1.6 - Volumes
  > - Volumes no Docker representam a persistência de dados.
  > - Caso o Contêiner não tenha um volume, ao ser parado, tudo será apagado.  
  > - Existem 3 Tipos de Volumes:
  >    
  > | Tipo    | Local  | Persistência                                     | Objetivo                           |
  > |---------|--------|--------------------------------------------------|------------------------------------|
  > | Nomeado | Docker | Diretório do Docker no Host                      | Bancos de Dados, Logs e Arquivos   | 
  > | Bind    | Host   | Arquivo / Diretório a ser espelhado no Contêiner | Desenvolvimento                    |
  > | tmpfs   | RAM    | Rápido, mas apaga tudo quando para o Contêiner   | Caches, Sessões ou Dados Sensíveis |

D1.7 - Dockerfile
  
  > - Arquivo de texto com as instruções de criação de imagem;  
  > - Define o ambiente e o comportamento do contêiner.  
  > - Normalmente usado para:   
  >   - "Exportar" o ambiente para outros servidores / pessoas;  
  >   - Automação e Versionamento de imagens;  
  >   - Padronização de Contêiners;  
  >   - Imagens Customizadas;  
  >   - Testes e Deploys (CI/CD).  
  
D1.8 - Primeiros Comandos 
  
```
docker --version
docker run hello-world

docker run --name ubuntu_container -it ubuntu bash
docker run --name nginx_server -d -o 8080:80 nginx
docker run --name mysql_server -dp 93306:3306 -e MYSQL_ROOT_PASSWORD=mysqlpassword mysql

docker exec -it nginx_server bash
CTRL P + CTRL Q                 # Sair do contêiner sem pará-lo

docker ps
docker ps -a

docker start (contêiner) (contêiner2) 
docker stop (contêiner) (contêiner2)
docker rm (contêiner) (contêiner2)
docker logs (contêiner) 

docker search (imagem)
docker pull (imagem)           # Serve também para atualizar a imagem
docker pull (imagem):(tag)     # As tags só podem ser vistas no hub 
docker images
docker rmi (imagem) (imagem2)

docker run -itd --name ubuntu_server -v ubuntu_server_vol:/tmp/ ubuntu
docker volume ls 
docker volume prune            # Apaga todos os volumes sem utilização
docker volume rm (volume)

docker -run -d --name sql_server_tmpfs -e MYSQL_ROOT_PASSWORD=admin --mount type=tmpfs,dst=/tmp,tmpfs-size=50M mysql  
docker -run -itd --name ubuntu_server_bind -v /tmp/Docker_Teste_Local_WSL:/tmp/ ubuntu  
```

D1.9 - URLs 

  > - Imagens Oficiais: https://hub.docker.com/search?badges=official&type=image

</div> 
</details>

----

<details>
  <summary><b> 2. Intermediário</b></summary>
<div align="Left"> 
<br>

D2.1 - Redes | Networks no Docker  
 > - As redes definem como será a comunicação do Contêiner com os demais Contêineres e Dispositivos.  
 > - Tipos de Rede:
 >    
 > | Rede          | Descrição                                                 |
 > |---------------|-----------------------------------------------------------|
 > | Bridge        | Rede Virtual Isolada entre Contêineres no mesmo Host      |
 > | Host          | Escuta Diretamente nas Portas do Host (Sem NAT)           |
 > | None          | Sem Acesso à Rede                                         |
 > | Overlay       | Ambientes Distribuídos (Swarm)                            |
 > | MacvLan       | Recebe IP como se fosse um Dispositivo Físico na Rede     |
 > | Custom Bridge | Ordem de Inicialização dos Contêineres                    |
 >
````
 docker network ls
 docker network create (rede)
 docker network inspect (rede)
 docker network rm (rede)

 docker network connect (rede) (contêiner)
 docker network disconnect (rede) (contêiner)

 docker network create -d bridge (rede bridge)
 docker network create -d overlay (rede overlay)
 docker network create -d macvlan (rede macvlan)

 docker run --network bridge nginx 
 docker run --network host nginx 
````
  
D2.2 - O Que é o "Docker Compose"?  
 > - Docker Compose permite definir e gerenciar múltiplos contêineres usando um YAML: docker-compose.yml;
 > - Se trata de uma orquestração de vários contêineres como um projeto;
 > - É possível rodar o comando e usar o parâmetro "-f" para usar outro arquivo (que possua outro nome);
 > - Ao rodar o "up", estar no diretório que contenha o arquivo .yml.
 >   
 > | Adições    | Descrição                                                 |
 > |------------|-----------------------------------------------------------|
 > | Services   | Define os Contêineres - Cada Serviço é um Contêiner       |
 > | Volumes    | Define Volumes Persistentes                               |
 > | Networks   | Define Redes Personalizadas                               |
 > | Depends_on | Ordem de Inicialização dos Contêineres                    |
 >   
 > - O Kubernetes seria um Docker Compose muito mais complexo e em larga escala;
 > - É possível conveter o docker-compose.yml em arquivos Kubernetes.
 >   
````
docker compose up
docker compose up -d
docker compose down

docker compose ps
docker compose logs

docker compose --project-name lgtm-stack up
docker compose --project-name lgtm-stack down

docker compose --project-name ps
docker compose --project-name logs

kompose convert
````
 > - Exemplo de Docker Compose com o Grafana Stack (LGTM):  
````  
  
services:
  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"

  loki:
    image: grafana/loki
    container_name: loki
    ports:
      - "3100:3100"

  tempo:
    image: grafana/tempo
    container_name: tempo
    ports:
      - "3200:3200"
      - "4317:4317"
    volumes:
      - ./tempo.yaml:/etc/tempo.yaml
      - ./tempo-data:/tmp/tempo
    command: [ "-config.file=/etc/tempo.yaml" ]

  mimir:
    image: grafana/mimir
    container_name: mimir
    ports:
      - "9009:9009"

Obs.: Para rodar com o Tempo, criar o arquivo "tempo.yaml":

server:
  http_listen_port: 3200
distributor:
  receivers:
    otlp:
      protocols:
        grpc: {}
ingester:
  trace_idle_period: 10s
  max_block_duration: 5m
compactor:
  compaction:
    block_retention: 1h
metrics_generator:
  processor:
    span_metrics:
      dimensions:
        - http.method
        - http.status_code
storage:
  trace:
    backend: local
    wal:
      path: /tmp/tempo/wal
    local:
      path: /tmp/tempo/traces
</details>      
````

</div> 
</details>

----
