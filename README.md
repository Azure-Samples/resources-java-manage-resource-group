---
services: compute
platforms: java
author: alvadb
---

# Manage Azure resource group with  Java

**On this page**

- [Run the sample](#run)
- [What is ManageResourceGroups.java doing?](#example)
   - [Create a resource group](#create)
   - [Update a resource group](#update)
   - [List resource groups](#list)
   - [Delete a resource group](#delete)
 
<a id="run"></a>
## Running the sample ##

1. Set the environment variable `AZURE_AUTH_LOCATION` with the full path for an [auth file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md).

2. Clone the repository.

```
git clone https://github.com/Azure-Samples/resources-java-manage-resource-group.git
```

3. Run the sample

```
cd resources-java-manage-resource-group
mvn clean compile exec:java
```

<a id="example"></a>
## What is ManageResourceGroup.java doing?

The sample starts by creating some name and tag variables that it uses in the various tasks.

```
final String rgName = ResourceNamer.randomResourceName("rgRSMA", 24);
final String rgName2 = ResourceNamer.randomResourceName("rgRSMA", 24);
final String resourceTagName = ResourceNamer.randomResourceName("rgRSTN", 24);
final String resourceTagValue = ResourceNamer.randomResourceName("rgRSTV", 24);
```

Then is signs in to the account using the authentication file.

```
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure.configure()
        .withLogLevel(HttpLoggingInterceptor.Level.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<a id="create"></a>
### Create a resource group

```
ResourceGroup resourceGroup = azure.resourceGroups()
        .define(rgName)
        .withRegion(Region.US_WEST)
        .create();
```

<a id="update"></a>
### Update a resource group

```
resourceGroup.update()
    .withTag(resourceTagName, resourceTagValue)
    .apply();
```

<a id="list"></a>
### List resource groups

```
azure.resourceGroups().list();
```

<a id="delete"></a>
### Delete a resource group

```
azure.resourceGroups().delete(rgName2);
```

## More information ##

[http://azure.com/java] (http://azure.com/java)

If you don't have a Microsoft Azure subscription you can get a FREE trial account [here](http://go.microsoft.com/fwlink/?LinkId=330212)

---

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.