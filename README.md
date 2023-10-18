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