# 2 VM-Series Firewalls with public ip addresses and an internal load balancer with two webservers

NOTE---This deployment leverages the multiple public ip address feature that is currently in preview and is only available in
the West Central US region.  This template deploys to the West Central US region and requires the the public ip address preview 
is enabled on the subscription.

The intent of this ARM template is to deploy two firewalls with public IP address both the managemant and eth1 ports to allow
direct internet traffic to the eth1 interface from the internet.  It also deploys and internal load balancer and two web servers
with apache.  This template does not license the firewall or deploy a panos configuration.  Configs are included in this directory 
that can be used to provide basic functionality.

This deployment includes:
- Two Palo Alto Networks Firewalls
- One Internal Load Balancer
- Two Web Servers
- VNET 10.0.0.0/16
- Multiple Subnets and UDRs to support the traffic flow

This template is meant to let you do customized deployments of VM-Series instead of deploying from the Azure Marketplace. You can deploy using the "Deploy to Azure" button below or download the template and customize it to your needs. You can also fork the templates into your own GitHub repository.

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdjspears%2FPaloAlto%2Fmaster%2Fazure-public-ip%2Ftemplate.json)
[<img src="https://camo.githubusercontent.com/536ab4f9bc823c2e0ce72fb610aafda57d8c6c12/687474703a2f2f61726d76697a2e696f2f76697375616c697a65627574746f6e2e706e67" data-canonical-src="http://armviz.io/visualizebutton.png" style="max-width:100%;">](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fdjspears%2FPaloAlto%2Fmaster%2Fazure-public-ip%2template.json)


## Deploy ARM Template using Azure CLI in ARM mode

1. Download the two JSON files: template.json and parameters.json
1. Customize the azureDeploy.parameters.json file and then deploy it from your computer.
1. Install the latest <a href="https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/">Azure CLI</a> for your computer.</li>
1. Validate and deploy the ARM template:

``` azure
    azure login
    azure config mode arm
    azure  group  template  validate  -g YourResourceGroupName \
        -e  template.json   -f  parameters.json
    azure group create -v -n YourResourceGroupName -l YourAzureRegion  \
        -d  YourDeploymentLabel  -f template.json -e parameters.json
```

**Check the status of your deployment:**

- CLI: `azure vm show  -g YourResourceGroupName  -n YourDeploymentLabel`
- Azure Portal: Your Resource Group > Deployment or Alert Logs
