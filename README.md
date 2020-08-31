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
- enter into web container : `docker exec presta_web bash`
- compile assets : `npm run build`
- watch assets changes : `npm run watch`


### General information

- Php 7.3
- Mysql 5.7
- Phpmyadmin : latest
- NodeJs : 12.x