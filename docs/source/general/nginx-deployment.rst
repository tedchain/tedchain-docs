Deploying Tedchain in a production environment
===============================================

In production, it is recommended to proxy the Tedchain server behind a reverse proxy server such as Nginx. This architecture enables a number of possibilities:

- Expose Tedchain through SSL/TLS
- Host multiple Tedchain server instances on the same port
- Change the URL path under which the Tedchain server is being exposed
- Route requests to different Tedchain instances depending on the host name used

This document explain the few steps necessary to expose Tedchain through Nginx.

Install Docker
--------------

Refer to the `base Docker deployment documentation <docker-deployment>` to find out how to install Docker and Docker Compose.

Pull the Docker images through Docker Compose
---------------------------------------------

Clone the tedchain/docker-deployment repository from GitHub, and copy the configuration files from the templates provided.

    git clone https://github.com/tedchain/docker-deployment.git tedchain
    cd tedchain
    cp templates/docker-compose-proxy.yml docker-compose.yml
    cp templates/nginx.conf nginx/nginx.conf
    mkdir data
    cp templates/config.json data/config.json

Edit the configuration file (``data/config.json``) as described in the `base Docker deployment documentation <docker-deployment>`.

You can now start the server:
    
    docker-compose up -d

Note: By default, Nginx will run on port 80.
