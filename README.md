# KustoPythonPlugin
This repo records the steps taken me to create a Kusto cluster and enable Python Plugin and finally run a user defined function from a whl file.

## Create a Kusto cluster
You can create a Kusto cluster for dev/test by following this article: 
https://docs.microsoft.com/en-us/azure/data-explorer/create-cluster-database-portal

For availability zone, you may pick "Local" to save money.

Once the cluster fully created (10-15 minutes), you need to create a databse, say, TestKusto.

Now you can enable the Python plugin by following this article:
https://docs.microsoft.com/en-us/azure/data-explorer/language-extensions

This will take you another 5 minutes to finish the cluster enabling process.

Be aware that the currently Python v. 3.6 is supported. For details you may follow this article: 
https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/pythonplugin?pivots=azuredataexplorer

## Install Python Package
