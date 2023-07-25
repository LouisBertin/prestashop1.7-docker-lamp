# Prestashop 1.7 docker configuration

Stack defines to run Prestashop 1.7.6.X/1.7.7.X, you have to download the latest stable version [here](https://prestashop.fr/versions/) and extract it into the `www` folder or use the Prestashop repository on [Github](https://github.com/PrestaShop/PrestaShop/tags)

Then, you can follow the Prestashop installer instructions.

Here is the result provided by the [Prestashop system requirements tool](https://devdocs.prestashop.com/1.7/basics/installation/system-requirements/) : 

![Prestashop system requirements](https://upload.vaa.red/i/JvmeY.png)

### ⚠️ Prestashop DB credentials during installation

- host: db
- database: the name entered in the `.env` file
- user: root
- pwd: root

Of course you can change everything in the `docker-compose.yml`

### ⚠️ Before anything else

- Duplicate `.env.dist` to `.env` and change credentials inside.
- Create a `www` folder

### ⚠️ macOS users - update 2023 - better overall performance

You can use OrbStack instead of NFS and Docker Desktop : https://orbstack.dev/

### ⚠️ macOS users - enable NFS

If you need to speed up your web container, I advice you to enable NFS on your mac and in the `docker-compose.yml`
```yml
services:
    web:
        container_name: ${PROJECT_NAME}_web
        build:
            context: ./conf
            args:
                PHP_VERSION: '7.3'
        ports:
            - "80:80"
        volumes:
            - nfsmount:/app/
        links:
            - db:db

volumes:
  nfsmount:
      driver: local
      driver_opts:
          type: nfs
          o: addr=host.docker.internal,rw,nolock,hard,nointr,nfsvers=3
          device: ":${PWD}/www"
```

If you need more informations about NFS, you can read the excellent article about this topic written by Jeff Geerling : https://www.jeffgeerling.com/blog/2020/revisiting-docker-macs-performance-nfs-volumes


### Useful commands:

- run container : `docker-compose up -d`
- stop container : `docker-compose down`
- rebuild container : `docker-compose up -d --build`
- enter into web container : `docker exec -it ${PROJECT_NAME}_web bash`
- install npm dependencies : `docker exec -it ${PROJECT_NAME}_web npm i --prefix YOUR/FOLDER/PATH`
- build assets with npm : `docker exec -it ${PROJECT_NAME}_web run build --prefix YOUR/FOLDER/PATH`
- watch assets with npm : `docker exec -it ${PROJECT_NAME}_web run build --prefix YOUR/FOLDER/PATH`
- database dump : `docker exec -it ${PROJECT_NAME}_db mysqldump --single-transaction -u root --password=root YOUR_DB_NAME > YOUR_BACKUP.sql`


### Mailcatcher

You can see all the email send by Prestashop on the Mailcatcher web interface : http://localhost:1080.
Here is the Prestashop SMTP configuration for MailCatcher and Docker :

<img width="1511" alt="mailcatcher" src="https://user-images.githubusercontent.com/22589554/189415670-9eb4e5df-d087-4db7-855c-85839f6379be.png">

### General information

- Php : 7.3 by default. Customizable in the `docker-compose.yml` file
- Mysql : 5.7
- Phpmyadmin : latest
- NodeJs : 10.x by default. Customizable in the `docker-compose.yml` file
- MailCatcher : 0.7.1

ℹ️ If your project is managed by VCS (Git), you can find your `composer.json` and `composer.json.lock` on the [official Prestashop Github Repository](https://github.com/PrestaShop/PrestaShop/tags)
