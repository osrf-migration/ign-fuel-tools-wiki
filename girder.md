# Details about the Girder implementation of the Ignition Fuel API

### Search a resource by name

Girder REST API offers the ability to search resources. Apparently, the Girder search only matches resources with the exact same name of the text used in the search or resources that contain a prefix of the text used in the search.

**ToDo: Research if there are additional ways to perform more generic searches**
**ToDo: Verify that the resources hosted under private directories are found when including the right access credentials**

### Download

All Ignition Fuel operations use names or paths for selecting the right resource[s]. However, most of the Girder API uses IDs to identify resources. In most of the Girder operations, a two-step communication is required. In the first step, the ID of the resource is located. The second step uses the ID to fetch and download the resource.

### Upload

In a similar way, a first step is required to acquire the Id of the destination directory. Then, the upload operation can be requested.

### List

Girder does not categorize or label any of the resources so we need a way to add semantics to the resources. Here are several ideas to implement this functionality:

* Add some metadata to the resource that helps with its categorization.
* Require a specific agreement in the way the resources are stored in the server. E.g.: 


```
#!python

/collections/<organization_name>/<resource_type>/<resource_name>/<resource_content>
```

We may have to filter by the name of the second directory name to identify the type of the resource.