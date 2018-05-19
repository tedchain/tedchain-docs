Tedchain Server Docker deployment
==================================

Tedchain Server is cross platform and can be deployed as a `DNX application <https://dotnet.readthedocs.org/en/latest/dnx/overview.html>`_ on Windows, OS X and Linux. However, to simplify dependency management and homogenize deployment of Tedchain, we are shipping it as a Docker image.

This document explains the few steps necessary to have the Tedchain server running.

Install Docker
--------------

Note: This assumes you are running Linux. Use `these instructions <http://docs.docker.com/installation/windows/>`_ if you are running Windows, and `these instructions <http://docs.docker.com/installation/mac/>`_ if you are running OS X.

First, install Docker if you don't have it:

    wget -qO- https://get.docker.com/ | sh

Then install Docker Compose:

    apt-get install python-pip
    pip install -U docker-compose

Install Tedchain Server
------------------------

Clone the tedchain/docker-deployment repository from GitHub, and copy the configuration files from the templates provided.

    git clone https://github.com/tedchain/docker-deployment.git tedchain
    cd tedchain
    cp templates/docker-compose-direct.yml docker-compose.yml
    mkdir data
    cp templates/config.json data/config.json

Now, edit the configuration file (``data/config.json``):

    nano data/config.json

Set the ``instance_seed`` setting to a random (non-empty) string.
   
    [...]
      // Define transaction validation parameters
      "validator_mode": {
        // Required: A random string used to generate the chain namespace
        "instance_seed": "",
        "validator": {
    [...]
    
Note: By default, the Tedchain server will run on port 8080. You can edit ``docker-compose.yml`` if you want to run on a non-default port.

You can now start the server:
    
    docker-compose up -d

This will start the Tedchain server in the background. To check that the server is running properly, check the docker logs:

    docker logs tedchain-server

You should not see any error:

    info: General[0]
        [2016-07-10 18:20:10Z] Starting Tedchain v0.7.0
    info: General[0]
        [2016-07-10 18:20:11Z]
    info: General[0]
        [2016-07-10 18:20:13Z] Stream subscriber disabled
    info: General[0]
        [2016-07-10 18:20:13Z] Anchoring disabled
    Hosting environment: Production
    Content root path: /tedchain
    Now listening on: http://0.0.0.0:8080
    Application started. Press Ctrl+C to shut down.

Tip: You can also run the Tedchain Docker container in the foreground by running ``docker-compose up`` and omitting the ``-d`` switch.

Now that you have a server running, you can connect to the server with a `client <tedchain-client>`.

Configuring admin keys
----------------------

Use the `client <tedchain-client>` to generate a seed, and derive it into an address. Once you have an address, you can use it as an admin address on your server instance. To do so, update ``data/config.json`` and add it to the ``admin_addresses`` list:
   
    // ...
    "admin_addresses": [
      "<your_address_here>"
    ],
    // ...

Tip: Follow `these steps <create-info-record>` to configure the ``info`` record on your new instance. The ``info`` record is used by clients connecting to the instance to receive additional information about the instance they are connecting to.

Controlling the server
----------------------

To restart the server, use:

    docker-compose restart
    
To stop it, use:

    docker-compose stop