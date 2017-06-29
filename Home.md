# Ignition Fuel Tools

A C++ library and a set of command line tools for interacting with a server containing simulation resources. Examples of these resources are SDF files or worlds, among others. The service provided by Ignition Fuel supports different server types for hosting the resources. The current Gazebo model database or [Girder](https://girder.readthedocs.io/en/latest/) are examples of two supported server types.


## [Features](https://bitbucket.org/ignitionrobotics/ign-fuel-tools/wiki/features)
The set of features supported by Ignition Fuel.

## [Architecture](https://bitbucket.org/ignitionrobotics/ign-fuel-tools/wiki/architecture)
The overall architecture of Ignition Fuel.

## [Model database](https://bitbucket.org/ignitionrobotics/ign-fuel-tools/wiki/model_database)
Details related with the usage of a model database as the server for hosting resources.

## [Girder](https://bitbucket.org/ignitionrobotics/ign-fuel-tools/wiki/girder)

### Resource organization

We need to define a way to organize resources in Girder such that:

- Can be easily discovered, both in the UI and by other tools (e.g. Gazebo).
- Can be queried by type (e.g. list all gazebo worlds).
- The owner of the resource can define access rights.

**Some possible options:**

- Similar to github, organizations / individuals have a collection assigned to them. Inside that collection there can be a folder per resource type (e.g. "worlds").
    - Pros: Familiar way of arranging resources, the owner of the resource is clear.
    - Cons: A resource can (and must) have a single type, not clear how to query, we may need to create the collection via script on registration, as creating a new collection requires admin rights
- Tag Resources with metadata. We could still adhere to the idea of having a collection per user / organization but using metadata to tag resources instead of a folder-based organization. 
    - Pros: Familiar way of arranging resources, the owner of the resource is clear, a resource may have multiple types 
    - Cons: Still not clear how efficient is to query by metadata, we may need to create the 

Based on what was discussed in Grider's mailing list:

- Metadata query is not supported out of the box, but shouldn't be a big deal to implement as a plugin.
- We should however be careful to add the proper indexes to the DB foe these to be perfomant.
- In the plugin we can add our custom REST endpoints, so it should play nice with existing REST infrastructure.
- A couple more of alternatives came up:
    - Use a single "assets" collection and give each user a folder (like the `/home` dir in linux).
    - Users can be treated as collections, so maybe storing the assets inside the user can be another option. This still needs some research, but an example can be seen in https://data.kitware.com/#user/55087c098d777f5ff55d5e3a


### Resource versioning

Based on what was discussed in Grider's mailing list, there is effectively no support for file / folder versioning out of the box. There is however a plugin (https://github.com/girder/data_revisions) that supports file versioning. We may use this as a baseline to further implement also folder versioning.