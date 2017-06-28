# Architecture of Ignition Fuel Tools

The Ignition Fuel service operates using a client/server architecture. One or multiple servers store the resources. Clients requests actions (search, download, upload, list) that will query or modify the resources contained within the servers.

The Ignition Fuel server supports multiple server types. As of today, a Gazebo model database and Girder are under consideration as server types. The functionality provided by Ignition Fuel can be exercised from a client using either a CLI tool or a C++ function. Humans are the target audience for using the CLI tools and other programs (e.g.: a simulator) are the expected consumers of the C++ API.

## Where does my client store the resources downloaded?

By default, Ignition Fuel stores all resources under `~/.ignition/fuel/`, although this path might be modified using a configuration file. Within `~/.ignition/fuel/` we can find one subdirectory containing the name of the server containing the resources (e.g.: `~/.ignition/fuel/my_server). If we go one directory deeper we should find the resource types already downloaded from that server (e.g.: sdf, worlds). If we go one directory lower, we'll find the name of the resource. Within this last directory we'll observe all the files related with the given resource. E.g.:


```
#!python

~/.ignition/fuel/my_server/sdf/coke_can/model.sdf
~/.ignition/fuel/my_server/sdf/coke_can/model.conf
~/.ignition/fuel/my_server/sdf/coke_can/materials/...
~/.ignition/fuel/my_server/sdf/coke_can/meshes/...
```

## Configuration files

Ignition Fuel uses a configuration file for specifying the servers, its location, type and credentials. The credentials are needed when accessing private directories or for uploading resources.
Alternatively, we could provide multiple configuration files, one per server.

## How does the interaction between the client and server occurs?

This interaction varies depending on the server type. When an operation is requested, the type of the server should be read using the configuration file[s]. Once the type is known, the client should use the implementation of the operation available for that server type. Under the hood, each implementation will use the interface that the server requires, e.g. a REST API for Girder.