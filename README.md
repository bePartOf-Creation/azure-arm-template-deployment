# AZURE ARM TEMPLATES DEPLOYEMENT TO A TARGET RESOURCE GROUP WITHIN A TENANT.

# Getting Started

The purpose of this deployment is to demonstrate the possibility of deploying to AZURE with an ARM TEMPLATE.

### Use Case.
A Saving Application(In Requirement Gathering) called `KoloBox Savings App` was used as my use case, where i have created a single resource in resource group`(kolobox-rgp)`
to host my application in the  `dev` environment, redirects the creation of the resource to a re-usable template `(simpledevtemplate.json)` which was used as template for deployment 
to another resource group `(kolobox-prod-rgp)` i choose to be my `prod` environment. The next sections will be command used and  challenegs faced in carrying out this slick deployment.

### Commands Used.
First of all, the prequisite here is to have the dynamics of linux commands.

* `az login`
* `az group create -n kolobox-rgp -l eastus`
* `az group list -o table` OR
* `az group exists -g  kolobox-rgp`
* `az vm create -g kolobox-rgp -n testVm --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys  --size Standard_B1s`.
After creation, test the ssh authentication to your vurtual machine with `ssh azureuser@20.163.192.37`.

Yaay!!!!! It Works 😁

* `az group export -g kolobox-rgp >> simplateTemplate.json`
* `az group create -n kolobox-prod-rgp -l eastus`
* `az group deployment create --template-file simpledevtemplate.json --parameters networkInterfaces_testVmVMNic_name=KoloboxProdNic networkSecurityGroups_testVmNSG_name=KoloboxProdNSG publicIPAddresses_testVmPublicIP_name=KoloboxProdPublicIP virtualMachines_testVm_name=KoloboxProdVm virtualNetworks_testVmVNET_name=KoloboxProdVNET -g kolobox-prod-rgp`.


Yaay!!!!! It DEPLOYED 😁 


### Challenges Faced
Errors Like:
`'simpledevtemplate.json' is misspelled or not recognized by the system.'` - This was caused by a missing command `(create)` while trying to deploy with my arm template to the target rg.

`"code":"InvalidParameter",
"target":"requireGuestProvisionSignal",
"message":"The property 'requireGuestProvisionSignal' is not valid because the 'Microsoft.Compute/Agentless' feature is not enabled for this subscription."}` - This property `'requireGuestProvisionSignal'` was not enable for subscription, also this was was taken out of the template in resolving it.

### Deployemt Images
`Dev Deployment(kolobox-rgp)`
![KoloBox Dev Environment](https://github.com/bePartOf-Creation/azure-arm-template-deployment/assets/76472595/46b9eba2-de8a-42c3-8b68-54d2f310d0b6)

`Prod Deployment(kolobox-rpod-rgp)`
![KoloBox Prod Environment](https://github.com/bePartOf-Creation/azure-arm-template-deployment/assets/76472595/8974925c-605d-421b-a19a-6b567ae9360c)
 
## Stay in touch

- Author - [Olasunkanmi Olayinka .O](https://kamilmysliwiec.com)
- LinkedIn - [Olasunkanmi Olayinka](https://www.linkedin.com/in/olayinka-olasunkanmi/)
- Twitter - [@AgbaKhoder](https://twitter.com/AgbaKhoder)

## License





