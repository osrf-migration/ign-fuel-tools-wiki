# Ignition Fuel features

Next you can find the set of features supported by Ignition Fuel tools. The same functionality should be available via a CLI tool or a c++ API:

### Search for a given resource by name

E.g.: ign fuel --search coke_can

The result of the search request should tell you whether a model was found or not, the path of each model found and the server containing the resource. It's possible to configure Ignition Fuel to use multiple servers (e.g.: one public well known service and a company server containing proprietary and private models).

### Download a resource by name

E.g.: ign fuel --download coke_can

Downloads the resource from all the servers that contain the given resource. Optionally, we could specify the server and path for downloading just a single copy of the resource.

### Upload a resource

E.g.: ign fuel --upload coke_can --remote my_public_server --dst /collections/caguero/sdf

Uploads a resource from the local filesystem to a destination folder in a given server.

### Show the list of resources of a given type

E.g.: ign fuel --list sdf

Displays all resources, path and server of a given type (sdf, worlds, ...). Optionally, we could filter by server.