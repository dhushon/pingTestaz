# pingTestaz
running a ping Test for Azure instances to determine latencies...

# setup az[ure] cli
Assumed azure cli works on your platform today, test with az --version
```
DHushon-Mac:~/work/ping$ az --version
```
```
azure-cli                         2.0.75 *

command-modules-nspkg              2.0.3
core                              2.0.75 *
nspkg                              3.0.4
telemetry                          1.0.4

Python location '/usr/local/Cellar/azure-cli/2.0.75/libexec/bin/python'
Extensions directory '/Users/dhushon/.azure/cliextensions'

Python (Darwin) 3.7.4 (default, Oct 12 2019, 19:06:48) 
[Clang 11.0.0 (clang-1100.0.33.8)]

Legal docs and information: aka.ms/AzureCliLegal
```
 
# loging az[ure] cli
run az login, follow standard process to login - typically a platform based browser url mime launch of a target loging thry the cloud to the cli agent
```
DHushon-Mac:~$ az login
```
```
Note, we have launched a browser for you to login. For old experience with device code, use "az login --use-device-code"
You have logged in. Now let us find all the subscriptions to which you have access...
[
  {
    "cloudName": "AzureCloud",
    "id": "$myID",
    "isDefault": true,
    "name": "Pay-As-You-Go",
    "state": "Enabled",
    "tenantId": "myTenantID",
    "user": {
      "name": "somebody@example.com",
      "type": "user"
    }
  }
]
```

# setup the vm
create a resource group in eastus... note that this will want to become a variable sometime as we build and test multiple
```
az group create --name myResourceGroup --location eastus
```
```
{
  "id": "/subscriptions/83d88eb1-d24a-4302-9d28-b6ec4de5f205/resourceGroups/pingTest",
  "location": "eastus",
  "managedBy": null,
  "name": "pingTest",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

now create the vm
```
az vm create \
  --resource-group pingTest \
  --name myVM \
  --image UbuntuLTS \
  --admin-username $username \
  --generate-ssh-keys
{
  "fqdns": "",
  "id": "/subscriptions/$someSubscription/resourceGroups/pingTest/providers/Microsoft.Compute/virtualMachines/pingVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-99-xx-xx",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.xx.xx.xx",
  "resourceGroup": "pingTest",
  "zones": ""
}
```

