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
 > Plataforma de software que permite a criar, empacotar e executar aplicações de forma isolada em contêineres. 

D1.2 - O que são "Contêineres"?  
 > Ambientes isolados, leves e portáteis que garantem a funcionalidade em diferentes sistemas. 

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
  > Volumes no Docker representam a persistência de dados.
  > Caso o Contêiner não tenha um volume, ao ser parado, tudo será apagado.  
  > Existem 3 Tipos de Volumes:
  > | Tipo    | Local  | Persistência                                     | Objetivo                           |
  > |---------|--------|--------------------------------------------------|------------------------------------|
  > | Nomeado | Docker | Diretório do Docker no Host                      | Bancos de Dados, Logs e Arquivos   | 
  > | Bind    | Host   | Arquivo / Diretório a ser espelhado no Contêiner | Desenvolvimento                    |
  > | tmpfs   | RAM    | Rápido, mas apaga tudo quando para o Contêiner   | Caches, Sessões ou Dados Sensíveis |

D1.7 - Dockerfile
  
  > Arquivo de texto com as instruções de criação de imagem;  
  > Define o ambiente e o comportamento do contêiner.  
  > Normalmente usado para:   
  > - "Exportar" o ambiente para outros servidores / pessoas;  
  > - Automação e Versionamento de imagens;  
  > - Padronização de Contêiners;  
  > - Imagens Customizadas;  
  > - Testes e Deploys (CI/CD).  
  
D1.8 - Primeiros Comandos 
  
```
docker --version
docker run hello-world

docker run --name ubuntu_container -it ubuntu bash
docker run --name nginx_server -d -o 8080:80 nginx
docker run --name mysql_server -dp 93306:3306 -e MYSQL_ROOT_PASSWORD=mysqlpassword mysql

docker exec -it nginx_server bash
CTRL P + CTRL Q  # Sair do contêiner sem pará-lo

docker ps
docker ps -a

docker start (contêiner)
docker stop (contêiner)
docker rm (contêiner)
docker logs (contêiner) 

docker search (imagem)
docker pull (imagem) # Serve também para atualizar a imagem
docker pull (imagem):(tag) # As tags só podem ser vistas no navegador 
docker images
docker rmi (imagem) (imagem2)




```

D1.9 - URLs 

  > - Imagens Oficiais: https://hub.docker.com/search?badges=official&type=image

</div> 
</details>

----
