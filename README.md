# Docker
> Comandos básicos.

Rodar comandos:

```sh
lucas@LucasOliveira:~$ docker run
```

## Rodando Imagens do Site Docker
No site https://hub.docker.com/, existem muitos modelos de imagens para replicar, para realizar um primeiro teste vamos criar um docker com o sistema operacional Linux.
No site (https://hub.docker.com/_/ubuntu), é possível achar a imagem e rodar este container na linha de comando, através do comando abaixo:
```sh
lucas@LucasOliveira:~$ docker run ubuntu
```
Este comando irá buscar no docker hub, baixar a imagem, e executar o container.<br><br>
Caso queira somante baixar a imagem o comando é: 
```sh
lucas@LucasOliveira:~$ docker pull ubuntu
```
Para saber os containers que estão em execução é possível realizar o comando:
```sh
lucas@LucasOliveira:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
Apesar de ter executado o comando para executar o container com o ubuntu, não existia nenhuma atividade sendo executada dentro deste container, desta maneira o container executou e já fechou.<br><br>
Agora para saber os containers que estão em execução e os que já foram executados, é possível rodar o comando:
```sh
lucas@LucasOliveira:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                      PORTS     NAMES
192ebedcac7d   ubuntu        "/bin/bash"   18 seconds ago   Exited (0) 16 seconds ago             charming_visvesvaraya
53aed12504af   hello-world   "/hello"      20 hours ago     Exited (0) 20 hours ago               friendly_brattain
```
Caso queira executar o comando e o container não encerre mesmo sem nenhuma atividade rodando, podemos usar o comando:
```sh
lucas@LucasOliveira:~$ docker run ubunto sleep 1d
```
desta maneira o container vai ficar aguardando 1 dia para encerrar, mesmo sem atividades em aberto.<br><br>
Caso queria encerrar a execução de um container, podemos executar o comando stop passando o ID do container ou o nome do container como mostra o comando:
```sh
lucas@LucasOliveira:~$ docker stop 192ebedcac7d
```
Para retomar a execução do comando é start como mostra o comando abaixo:
```sh
lucas@LucasOliveira:~$ docker start 192ebedcac7d
```
Existe um comando, também dentro desse universo todo do Docker, que é o docker exec. Eu posso simplesmente falar que eu posso executar algum comando dentro do meu container em modo interativo.
```sh
lucas@LucasOliveira:~$ docker exec -t 192ebedcac7d bash
root@192ebedcac7d:/#
```
## Mapeando Portas

Para fazer este teste vamos utilizar uma imagem chamada static-site (https://hub.docker.com/r/dockersamples/static-site), onde simula uma aplicação web cuja saída é possível visualizar através do navegador. <br><br>
Para executar vamos executar o static-site com a flag " -d " para que o terminal não trave e execute o container em segundo plano, como mostra o comando:
```sh
lucas@LucasOliveira:~$ docker run -d dockersamples/static-site
```
Desta maneira, verificando os containers que estão em execução, podemos verificar em qual porta esta disponível a aplicação:
```sh
lucas@LucasOliveira:~$ docker ps
CONTAINER ID IMAGE                     COMMAND                CREATED        STATUS        PORTS           NAMES
45493a7b660d dockersamples/static-site "/bin/sh -c 'cd /usr…" 40 seconds ago Up 39 seconds 80/tcp, 443/tcp ecstatic_mclaren
```
Agora quando adicionamos o " -P " (Maiúsculo), este sinalizador mapeia automaticamente as portas dentro do contêiner para portas disponíveis no host, ou seja, ele faz um mapeamento automático das portas entre o host e o contêiner. como mostra no comando abaixo:
```sh
lucas@LucasOliveira:~$ docker run -d -P dockersamples/static-site
0b205c3fc75c9733be385f4e2130f05ae45910168e19321d7866730bdc18f48d
```
desta forma conseguimos ver em qual porta está rodando a aplicação web, que neste caso é na porta 32769, onde consultamos utilizando o comando "docker port" como podemos ver no comando abaixo:
```sh
lucas@LucasOliveira:~$ docker ps
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                           NAMES
0b205c3fc75c   dockersamples/static-site   "/bin/sh -c 'cd /usr…"   16 seconds ago   Up 15 seconds   0.0.0.0:32769->80/tcp, 0.0.0.0:32768->443/tcp   fervent_kalam
lucas@LucasOliveira:~$ docker port 0b205c3fc75c
80/tcp -> 0.0.0.0:32769
443/tcp -> 0.0.0.0:32768
```
Caso queria deixar uma porta expecifica, podemos utilizar o comando com o " -p " (Minúsculo), informando que o host 8080 vai refletir na porta 80 do container, como mostra o comando abaixo:
```sh
lucas@LucasOliveira:~$ docker run -d -p 8080:80 dockersamples/static-site
d55f4ee8451c671e608d1416f91bebb22810d64eac4f31c30d9face4f87a9021
```