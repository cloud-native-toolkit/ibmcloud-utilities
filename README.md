# IBMCloud-Utilies

Remove all resources from an IBM Cloud account such as 

- Kubernetes and OpenShift clusters
- Container Registry namespaces (Only List)
- Applications 
- Services (like Cloudant, Watson services, Object Storage etc)
- Classic Baremetal servers
- Classic Virtual servers
- Code Engine projects 
- Cloud Functions Namespaces (and their underlying actions)
- API keys (excluding ones requires for managing Kubernetes clusters)
- Satellite locations
- Gen2 VPCs
- Gen2 VPC Subnet
- Gen2 VPC Loadbalancer

## Install the IBM Cloud CLI & plugins

In order to use this script you must have installed the IBM Cloud CLI. If you need to do that run the following:

- ***For MacOS***, run the following command:

```
curl -fsSL https://clis.cloud.ibm.com/install/osx | sh
```

- ***For Linux***, run the following command:

```
curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
```

- ***For Windows 10 Pro***, run the following command in PowerShell as an administrator:

```
curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
```

***Once IBM Cloud CLI installed***,  install several plugins for the script to execute successfully.
install them run the following commands:

```
ibmcloud plugin install -f code-engine
```

```
ibmcloud plugin install -f container-registry
```

```
ibmcloud plugin install -f container-service
```

```
ibmcloud plugin install -f cloud-functions
```

```
ibmcloud plugin install -f infrastructure-service
```

```
ibmcloud plugin install -f schematics
```

```
ibmcloud plugin install cloud-object-storage
```

```
ibmcloud plugin install vpc-infrastructure
```

## CLI options

| Category | Name                                                                       | Description          | Run Time |
|--------|----------------------------------------------------------------------------|----------------------|----------|
| Delete   | [Delete IBM Cloud resource(s)](./ibmcloud-delete.sh) |⚠️⚠️⚠️⚠️ Delete Resource Group, Cluster, Applications, Services, VPC (Subnet/ Loadbalancer), Classic VM, Code Engine, Cloud Functions or Satellite location, APIKeys almost anything you deal with in IBM Cloud | 10-30 Mins (Depends on total number of resources)  |

***Note:***

1. By default *IBM Cloud Utilies* only lists all resources which exist in the account/resourcegroup/region. You need to add `-n` flag to actually delete resources.
2. A config file can be used to specify names and IDs of resources to skip over.

```bash
ibmcloud-delete.sh [-n] [-c <path-to-config-file>]
```

* `-n`: Specify "no dry run". Resources will be deleted.
* `-c`: Specify a config file for IDs/names of resources to be saved from deletion. The tool will automatically look for a file called `ibmcloud-skip` in the local directory.

## Using the CLI

1. Clone the repo.

   ```bash
   git clone
   ```

2. Log into IBM Cloud.

   ```bash
   ibmcloud login --sso
   ```
3. Switch to Resource Group where you want to list and delete resources

   ```bash
   ibmcloud target -g <resource-group>
   ```
4. Switch to region where you want to list and delete resources

   ```bash
   ibmcloud target -r <region us-south,eu-gb>
   ```

4. Run the CLI.

   (A) Perform a dry run:

   ```bash
   ./ibmcloud-delete.sh
   ```

   (B) Delete all resources (will skip over any resorces found in `.ibmcloud-skip`):

   ```bash
   ./ibmcloud-delete.sh -n
   ```

   (C) Delete all resources but skip resources list in `ibmcloudconfig.txt`:

   ```bash
   ./ibmcloud-delete.sh -c ibmcloudconfig.txt
   ```

## TODO

1. The project needs support for deleting the following types of resources:

   * Storage(s) - File, Block & COS
  
## Resources

1. [IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started)