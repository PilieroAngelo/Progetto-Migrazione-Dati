# Progetto-Migrazione-Dati

PASSI PER L'INSTALLAZIONE E L'ESECUZIONE DEL PROGETTO:

FASE 1- INSTALLAZIONE:
1) Scaricare tutti i file (.zip e docker-compose)
2) Scaricare Mysql da questo link: https://www.mysql.com/products/workbench/
3) Scaricare il batabase (sakila database) da questo link: https://dev.mysql.com/doc/index-other.html
4) Scaricare MongoDB Compass e fare l'accesso https://www.mongodb.com/try/download/compass
5) Scaricare Docker Desktop https://www.docker.com/products/docker-desktop/
6) Installare l'immagine MinIO su Docker > docker run -d -p 9000:9000 -p 9090:9090 --name minio -v C:\minio\data:/data \ -e "MINIO_ROOT_USER=[user]" -e "MINIO_ROOT_PASSWORD=[password]" \ quay.io/minio/minio server /data --console-address ":9090"
7) Installare l'immagine Redis > docker run --name redis -p 6379:6379 -d redis
8) Installare tramite l'uso di docker-compose kafka e zookeeper
9) Aprire la cartella scaricata e aprire il file config.py
    -Modifica 'access_key' e 'secret_key' con i dati che avete inserito nel punto 6 durante l'installazione di MinIO, modificare user e password per quanto riguarda       l'accesso di MySQL e la configurazione del localhost di MongoDB
10)Caricare il database Sakila su MySQL
11) Scarica il backup con l'uso di CMD (mysqldump -u user -p Sakila > nome_backup.sql)
12) Caricarlo nel nuovo database (si consiglia di nominarlo Sakila2) sempre tramite l'uso di CMD (mysql -u user -p Sakila2 [o un altro nome] < nome_backup.sql

FASE 2- AVVIO:
1) Avviare i container Redis, Zookeeper, Kafka e MinIO su Docker
2) Accedi su MinIO e crea il bucket
3) Andare su config.py e cambiare il nome del bucket con quello dato in questa sezione 'bucket': '[nome bucket]'
4) Avviare main.py e seguire i comandi della console

(FACOLTATIVO FASE 3-RIAVVIO:)
--Nel caso vogliate riprovare il progetto dopo aver già fatto tutti gli step precendenti:
1) Andare su Docker e eseguire questo comando: docker exec -it nome_redis redis-cli
2) Controllare questo flag: GET initial_migration_done
  -Se da "true" signfiica che la migrazione è già stata effettuata quindi il programma salterà la prima fase di aggiornamento e controllo dei dati, in questo caso seguire il punto successivo
  -Se da "nil" basta solo andare nel main.py e rieseguire l'applicazione 
4) Eseguire questo comando per eliminare la flag "true": DEL initial_migration_done
-----

BUON DIVERTIMENTO
