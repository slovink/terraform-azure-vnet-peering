<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AZURE VNET PEERING
</h1>

<p align="center" style="font-size: 1.2rem;"> 
    Terraform module to create VNET PEERING resource on AZURE.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v1.1.7-green" alt="Terraform">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-APACHE-blue.svg" alt="Licence">
</a>






## Prerequisites

This module has a few dependencies:

- [Terraform 1.x.x](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/slovink/terraform-azure-vnet-peering/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
  ```hcl


module "vnet_peering" {
  source     = "../"
  depends_on = [module.resource_group_1, module.resource_group_2]

  enabled_peering       = true
  resource_group_1_name = module.resource_group_1.resource_group_name
  resource_group_2_name = module.resource_group_2.resource_group_name

  allow_gateway_transit_vnet1   = false
  use_remote_gateways_vnet1     = false
  allow_gateway_transit_vnet2   = false
  use_remote_gateways_vnet2     = false
  allow_forwarded_traffic_vnet1 = false
  allow_forwarded_traffic_vnet2 = false
  different_rg                  = true
  vnet_1_name                   = module.vnet.vnet_name[0]
  vnet_1_id                     = module.vnet.vnet_id[0]
  vnet_2_name                   = module.vnet_remote.vnet_name[0]
  vnet_2_id                     = module.vnet_remote.vnet_id[0]

}

  ```



## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/slovink/terraform-azure-vnet-peering/issues), or feel free to drop us an email at [devops@slovink.com](mailto:devops@slovink.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/slovink/terraform-azure-vnet-peering)!
