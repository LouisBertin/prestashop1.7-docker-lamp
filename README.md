# Prestashop 1.7 docker configuration

Stack defines to run Prestashop 1.7.6.X, you have to download the latest stable version [here](https://www.prestashop.com/en/previous-versions) and extract it into the `www` folder.

Then, you can follow the Prestashop installer instructions.

Here is the result provided by the [Prestashop system requirements tool](https://devdocs.prestashop.com/1.7/basics/installation/system-requirements/) : 

![Prestashop system requirements](https://upload.vaa.red/i/JvmeY.png)

### ⚠️ Prestashop DB credentials during installation

- host: db
- user: root
- pwd: root

Of course you can change everything in the `docker-compose.yml`


### Useful commands:

- run container : `docker-compose up -d`
- stop container : `docker-compose down`
- rebuild container : `docker-compose up -d --build`
- enter into web container : `docker exec -it presta_web bash`
- install npm dependencies : `docker exec -it presta_web npm i --prefix YOUR/FOLDER/PATH`
- build assets with npm : `docker exec -it presta_web run build --prefix YOUR/FOLDER/PATH`
- watch assets with npm : `docker exec -it presta_web run build --prefix YOUR/FOLDER/PATH`
- database dump : `docker exec -it presta_db mysqldump -u root --password=root YOUR_DB_NAME --compact > YOUR_BACKUP.sql`


### General information

- Php 7.2
- Mysql 5.7
- Phpmyadmin : latest
- NodeJs : 10.x