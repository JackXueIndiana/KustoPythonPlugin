# Kusto Python Plugin - Setup & Use
This repo records the steps taken me to create a Kusto cluster and enable Python Plugin and finally run a user defined function from a whl file.

## Create a Kusto cluster
You can create a Kusto cluster for dev/test by following this article: 
https://docs.microsoft.com/en-us/azure/data-explorer/create-cluster-database-portal

For availability zone, you may pick "Local" to save money.

Once the cluster fully created (10-15 minutes), you need to create a database, say, TestKusto.

Now you can enable the Python plugin by following this article:
https://docs.microsoft.com/en-us/azure/data-explorer/language-extensions

This will take you another 5 minutes to finish the cluster enabling process.

Be aware that the currently Python v. 3.6 is supported. For details you may follow this article: 
https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/pythonplugin?pivots=azuredataexplorer

### Checking:
Run .show cluster you should see your cluster with only one node.

Run .show plugins you should see all plugins that have been enabled (including python).

## Install Python Package
Step 1: Create a blob container to host the packages, preferably in the same place as your cluster. For example, 
https://<blob account name>.blob.core.windows.net/<container name>.

Step 2: Grant yourself AllDatabasesAdmin permissions from this cluster's IAM.
  
Step 3: Alter the cluster's callout policy to allow access to that blob container.
This change requires AllDatabasesAdmin permissions. For example, to enable access to a blob located the container defined above, run the following command:
.alter-merge cluster policy callout @'[ { "CalloutType": "sandbox_artifacts", "CalloutUriRegex": "<blob account name>.blob.core.windows.net/<container name>","CanCall": true } ]'
  
Step 4. Wrap your Python function in a WHL file.
I have a say_hello function WHL file downloaded from https://pypi.org/project/helloworld3663/   
The gz file also downloaded so we can reproduce the WHL file by running 

pip wheel [-w download-dir] package-name
  
Step 5. Zip the WHL file.  
The zip file is also included in this repo.  
  
Step 6. Upload the zip file to the container

## Call the Python Function in KQL   
Call the say_hello function in your KQL

### Checking
If everything works fine, you should see this output:
  
| ID	| Value |
|-----|-----------------|  
|1|	Hello, Caller 0|
|2|	Hello, Caller 1|
|3|	Hello, Caller 2|
