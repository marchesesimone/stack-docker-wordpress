
# Stack Docker Wordpress

## Setup locale

Kill della porta 80 per far girare traefix

`sudo kill $(sudo netstat -anp | awk '/ LISTEN / {if($4 ~ ":80$") { gsub("/.*","",$7); print $7; exit } }')`

#### Dipendenze

* [Docker](https://www.docker.com)
* [Docker compose](https://docs.docker.com/compose)
* [Træfik](https://traefik.io)

## Installazione locale

1. copiare il file `.env.example` in un nuovo file `.env` e personalizzare le voci nella sezione `LOCAL SETTINGS`
2. scaricare l'ultima versione di wordpress e scaricarla all'interno della cartella `docroot`
3. aggiungere al file hosts il puntamento al `PROJECT_BASE_URL` definito nel `.env`

```bash
127.0.0.1 web.stackwp.docker.loclahost
127.0.0.1 mailhog.stackwp.docker.loclahost
```

4. avviare lo stack Docker con il comando `make up`

## Utilizzo di Traefik

Scommentare in `docker-compose.yml` il container ```traefik```

## Importazione del DB
Nel container php è possibile utilizzare le wp-cli|https://wp-cli.org/it/ 

Eseguire il download del file e salvarlo nella root del progetto ed eseguire il seguente commando
```bash
make db
wp db import NomeFile.sql --allow-root 
```

o inserire il file sql nella cartella dump prensete nella root del progetto

#### Informazioni sullo sviluppo

**Installazione plugin**
```
wp plugin install PLUGIN_NAME --allow-root --activate
```

**Aggiornamento plugin**
```
wp plugin update PLUGIN_NAME --allow-root
```
Se vogliamo indicare una versione precisa del plugin dobbiamo aggiungere
```
--version=<versione>
```

**Aggiornamento del core**
```
wp core update
```
Per i possibili parametri vedi questa pagina [ https://developer.wordpress.org/cl