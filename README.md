# Prestashop 1.7 docker configuration

Stack defines to run Prestashop 1.7.6.X/1.7.7.X, you have to download the latest stable version [here](https://www.prestashop.com/en/previous-versions) and extract it into the `www` folder or use the Prestashop repository on [Github](https://github.com/PrestaShop/PrestaShop/tags)

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

### Useful commands:

- run container : `docker-compose up -d`
- stop container : `docker-compose down`
- rebuild container : `docker-compose up -d --build`
- enter into web container : `docker exec -it presta_web bash`
- install npm dependencies : `docker exec -it presta_web npm i --prefix YOUR/FOLDER/PATH`
- build assets with npm : `docker exec -it presta_web run build --prefix YOUR/FOLDER/PATH`
- watch assets with npm : `docker exec -it presta_web run build --prefix YOUR/FOLDER/PATH`
- database dump : `docker exec -it presta_db mysqldump --single-transaction -u root --password=root YOUR_DB_NAME > YOUR_BACKUP.sql`


### Mailcatcher

You can see all the email send by Prestashop on the Mailcatcher web interface : http://localhost:1080.
Here is the Prestashop SMTP configuration for MailCatcher and Docker :

![MailCatcher configuration](https://upload.vaa.red/i/7pery.png)

### General information

- Php : 7.3 by default. Customizable in the `docker-compose.yml` file
- Mysql : 5.7
- Phpmyadmin : latest
- NodeJs : 10.x
- MailCatcher : 0.7.1

ℹ️ If your project is managed by VCS (Git), you can find your `composer.json` and `composer.json.lock` on the [official Prestashop Github Repository](https://github.com/PrestaShop/PrestaShop/tags)
