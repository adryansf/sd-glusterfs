# SD GLUSTERFS

Projeto desenvolvido para a matéria de Sistemas Distribuídos.

## Etapas

### 1º Passo

Crie um arquivo docker-compose.yml no diretório de trabalho com o seguinte conteúdo:

```
docker-compose up -d
```

### 2º Passo

Acesse um dos contêineres, por exemplo, no gs1, execute:

```
docker exec -it gluster-server-1 bash
```

### 3º Passo

Dentro do contêiner, adicione o gluster-server-2 como um par e configure o volume (como fizemos anteriormente):

```
gluster peer probe gluster-server-2
gluster volume create gv0 replica 2 gluster-server-1:/data gluster-server-2:/data force
gluster volume start gv0
```

### 4º Passo

Monte o volume GlusterFS no diretório /mnt dentro do contêiner:

```
mount -t glusterfs localhost:/gv0 /mnt
```

### 5º Passo

Observe o funcionamento criando um arquivo dentro da pasta /mnt no container

```
cd /mnt
date > text.txt
```
