Zing+Serge Docker Container
=======================

Fork of https://github.com/1drop/zing with an updated version of Zing and integrated Serge based on https://github.com/evernote/serge-dockerfiles.

- [Zing](https://github.com/evernote/zing/) is a Community localization server - Get your community translating your software into their languages.  
- [Serge](https://serge.io/) is a Free, Open-Source Solution for Continuous Localization

## Environment Variables:

    ZING_CANONICAL_URL=http://zing.docker
    ZING_TITLE=TYPO3 Translation Server
    ZING_ADMIN_NAME=John Doe
    ZING_ADMIN_MAIL=john.doe@mail.com
    ZING_SENDER_MAIL=no-reply@zing.docker
    SECRET_KEY=4JY+9C9kEWASJk5MVkYH8ynd5ka9aRq56jssTwa2key8CZrSipNi1vD/1lPfzcqx/UY=
    
    MYSQL_HOST=mysql
    MYSQL_USER=zing
    MYSQL_PASSWORD=ChangeMe
    MYSQL_DATABASE=zing
    MYSQL_PORT=3306
    
    REDIS_HOST=redis
    REDIS_PORT=6379
    
## Volumes (for serge, optional):

    -v /var/serge:/var/serge
    -v /var/serge/lib:/usr/lib/serge/vendor/lib:ro

## Initialize MySQL DB on first Start

    docker run -it --rm -e MYSQL_HOST "mysql" -e MYSQL_DATABASE "zing" -e MYSQL_USER "zing" -e MYSQL_PASSWORD "ChangeMe" arturh85/zing-serge bash
    
then inside the bash:

    zing migrate
    zing initdb
    zing createsuperuser
    zing verify_user --all

## Example Usage:

    docker run -d --name zing-serge -p 5394:8000 -e REDIS_HOST "redis" -e MYSQL_HOST "mysql" -e MYSQL_DATABASE "zing" -e MYSQL_USER "zing" -e MYSQL_PASSWORD "ChangeMe" -e SECRET_KEY "changeMe" -e ZING_TITLE "My Zing Translation Server" -v /var/serge:/var/serge -v /var/serge/lib:/usr/lib/serge/vendor/lib:ro --restart=always arturh85/zing-serge
