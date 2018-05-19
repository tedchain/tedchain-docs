Running Tedchain
=================

Deploying Tedchain server can be done `through Docker <docker-deployment>`.

This document explains how to deploy Tedchain directly on a machine without using docker.

Prerequisites
-------------

Install the `.NET Command Line Interface <https://www.microsoft.com/net/core>`_ . This is cross-platform and runs on Windows, Linux and OS X.

Download the project files
--------------------------

Download the ``project.json``, ``Program.cs`` and ``config.json`` files from GitHub, then restore the NuGet dependencies. On Linux:

    $ wget https://github.com/tedchain/tedchain-technology/blob/master/src/Tedchain/project.json
    $ wget https://github.com/tedchain/tedchain-technology/blob/master/src/Tedchain/Program.cs
    $ wget https://github.com/tedchain/tedchain-technology/blob/master/src/Tedchain/data/config.json -P data
    $ dotnet restore

Note: On Windows, simply download the files manually using your browser, then run ``dotnet restore``.

Run Tedchain Server
--------------------

Run Tedchain server using the following command:

    $ dotnet run

Configuration
-------------

The dependencies section of the ``project.json`` file references the external providers pulled from NuGet:

    "dependencies": {
      "Microsoft.NETCore.App": {
        "version": "1.0.0",
        "type": "platform"
      },
      "Microsoft.AspNetCore.Server.IISIntegration": "1.0.0",
      "Tedchain.Server": "0.6.2",
    
      "Tedchain.Anchoring.Blockchain": "0.6.2",
      "Tedchain.Sqlite": "0.6.2",
      "Tedchain.SqlServer": "0.6.2",
      "Tedchain.Validation.PermissionBased": "0.6.2"
    },

By defaut, this imports the Sqlite storage engine (``Tedchain.Sqlite``), the SQL Server storage engine (``Tedchain.SqlServer``), the permission-based validation module (``Tedchain.Validation.PermissionBased``), and the Blockchain anchoring module (``Tedchain.Anchoring.Blockchain``). Update this list with the modules (and versions) you want to import.

You can then edit the ``data/config.json`` file to reference the `providers you want to use <configuration>`.

Tip: For example, if you want to use the ``SQLite`` provider as a storage engine, you will need to make sure the ``Tedchain.Sqlite`` module is listed in the dependencies.

Make sure you run ``dotnet restore`` again after modifying project.json.

Note: The Tedchain.Server dependency is the only one that is always required. The version of the ``Tedchain.Server`` package is the version of Tedchain you will be running.

Updating the target platform
----------------------------

The frameworks section of the project.json file lists the available target frameworks:

    "frameworks": {
      "netcoreapp1.0": {},
      "net451": {}
    }

By default .NET Core (cross-platform) and the .NET Framework (Windows only) are both targeted. Some providers run only on a subset of frameworks. In that case, remove the unsupported frameworks from the list to ensure the project runs.
