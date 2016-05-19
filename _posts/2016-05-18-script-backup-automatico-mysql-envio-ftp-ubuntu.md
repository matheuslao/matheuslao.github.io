---
layout: post
title: "Script de Backup Banco de Dados MySql + Envio FTP no Ubuntu"
date: 2016-05-18 23:50:53
categories: ubuntu, linux, mysql, backup, ftp, script, bash
tags: ubuntu, linux, mysql, backup, ftp, script, bash

---

Olá! Esse é um assunto cujo muitos blogs já postaram _scripts_ com soluções diversas e muito boas! Contudo, a necessidade sempre existe em usuários mais novos ou até mesmo naqueles que pretendem reescrever soluções ou procurar outras alternativas.

A ideia é simples: Utilizo uma máquina virtual na [Digital Ocean][digital-ocean] com _Linux Ubuntu_ instalado e farei o _backup_ de um banco de dados MySQL e posterior envio compactado para um FTP externo (outra máquina onde faço _backups_).

O _script_ utiliza:

* `mysqldump` para fazer uma cópia em _sql_ do banco de dados
* `gzip` para compactar o arquivo
* `ftp` para envio a um servidor externo
* `crontab` para agendar a execução do _script_


### O código

Segue abaixo o _script_. Deixei alguns comentários no código, mas acho que ele está bem intuitivo. Mesmo assim, se você tiver alguma dúvida ou sugestão, deixe seu comentário.

```bash
#!/bin/bash

MYSQL_DB="database"
MYSQL_USER="user"
MYSQL_PASSWORD="senha"
MYSQLDUMP_COMMAND="$(which mysqldump)"

BACKUP_FOLDER="/caminho/para/pasta/do/backup"

GZIP_COMMAND="$(which gzip)"

FTP_HOST="ftp.servidorbackup.com"
FTP_USER="user"
FTP_PASSWORD="senha"

TIMESTAMP=$(date +%Y%m%d-%H%M%S)

# Se a pasta já existir, limpa seu conteúdo. Caso contrário, cria
[ ! -d $BACKUP_FOLDER ] && mkdir -p $BACKUP_FOLDER || /bin/rm -f $BACKUP_FOLDER/*

FILE=$BACKUP_FOLDER/$MYSQL_DB.$TIMESTAMP.gz

$MYSQLDUMP_COMMAND -u $MYSQL_USER -p$MYSQL_PASSWORD $MYSQL_DB | $GZIP_COMMAND -9 > $FILE


ftp -inv $FTP_HOST << EOF
user $FTP_USER $FTP_PASSWORD
lcd $BACKUP_FOLDER
put *
bye

EOF
```

### Agendando execução automática

Salve o script em uma pasta `caminho/do/script/backup.sh` e adicione ao `crontab` para execução. No meu exemplo, configurarei para execução todo dia às 03:00am.

No terminal, digite o seguinte comando para editar seu _crontab_

    crontab -e

Adicione a seguinte linha:

    0 3 * * * /caminho/do/script/backup.sh >/dev/null 2>&1

Note que o trecho `>/dev/null 2>&1` serve para omitir a saída do script.

Agora, dê permissão de execução para seu script com:

    chmod +x caminho/do/script/backup.sh

Pronto! Salve e feche seu arquivo e seu banco de dados será feito _dump_ e encaminhado para seu servidor de backup via ftp!

[digital-ocean]:http://digitalocean.com
