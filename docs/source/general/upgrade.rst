Upgrading Tedchain server
=========================

To upgrade an Tedchain deployment done `through Docker <docker-deployment>`, run the following commands:

    git reset --hard
    git pull
    cp templates/docker-compose-direct.yml docker-compose.yml
    docker-compose build
    docker-compose restart
    
Note: If the new version you are upgrading to includes a configuration file schema change, don't forget to update the configuration file before restarting Tedchain.