<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AZURE VNET PEERING
</h1>

<p align="center" style="font-size: 1.2rem;">
    Terraform module to create VNET PEERING resource on AZURE.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v1.7.4-green" alt="Terraform">
</a>
<a href="https://github.com/slovink/terraform-azure-vnet-peering/blob/dev/LICENSE">
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
  source                        = "https://github.com/slovink/terraform-azure-vnet-peering.git?ref=1.0.0"
  depends_on                    = [module.resource_group_1, module.resource_group_2]

  enabled_peering               = true
  resource_group_1_name         = module.resource_group_1.resource_group_name
  resource_group_2_name         = module.resource_group_2.resource_group_name

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
## Peering in diff subscription
Here is an example of how you can use this module in your inventory structure:
   ```hcl
module "vnet_peering" {
  source                        = "https://github.com/slovink/terraform-azure-vnet-peering.git?ref=1.0.0"
  enabled_diff_subs_peering     = true
  resource_group_1_name         = module.resource_group.resource_group_name
  diff_subs_resource_group_name = data.azurerm_resource_group.resource_group_1.name
  alias_subs_id                 = "0a7be846-xxxxxxxxxxxxxx98787h"
  vnet_1_name                   = module.vnet.name
  vnet_1_id                     = module.vnet.id
  vnet_diff_subs_name           = data.azurerm_virtual_network.mgmt-staging-vnet.name
  vnet_diff_subs_id             = data.azurerm_virtual_network.mgmt-staging-vnet.id
}
  ```
## Peering in same subscription
Here is an example of how you can use this module in your inventory structure:
   ```hcl

module "vnet_peering" {
  source                = "https://github.com/slovink/terraform-azure-vnet-peering.git?ref=1.0.0"
  enabled_peering       = true
  resource_group_1_name = module.resource_group_1.resource_group_name
  resource_group_2_name = module.resource_group_2.resource_group_name
  different_rg          = true
  vnet_1_name           = module.vnet.name
  vnet_1_id             = module.vnet.id
  vnet_2_name           = module.vnet_remote.name
  vnet_2_id             = module.vnet_remote.id
}
  ```

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/slovink/terraform-azure-vnet-peering/blob/dev/LICENSE) file for details.


## Examples
For detailed examples on how to use this module, please refer to the [Examples](https://github.com/slovink/terraform-azure-vnet-peering/tree/dev/_example) directory within this repository.


## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/slovink/terraform-azure-vnet-peering/issues), or feel free to drop us an email at [contact@slovink.com](contact@slovink.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/slovink/terraform-azure-vnet-peering)!

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.7.4 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | >=3.87.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | >=3.87.0 |
| <a name="provider_azurerm.peer"></a> [azurerm.peer](#provider\_azurerm.peer) | >=3.87.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [azurerm_virtual_network_peering.peering](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network_peering) | resource |
| [azurerm_virtual_network_peering.peering_back](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network_peering) | resource |
| [azurerm_virtual_network_peering.peering_back_diff_subs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network_peering) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_alias_subs_id"></a> [alias\_subs\_id](#input\_alias\_subs\_id) | Alias for remote provider in module. | `string` | `""` | no |
| <a name="input_allow_forwarded_traffic_vnet1"></a> [allow\_forwarded\_traffic\_vnet1](#input\_allow\_forwarded\_traffic\_vnet1) | Controls if forwarded traffic from VMs in the remote virtual network is allowed | `bool` | `false` | no |
| <a name="input_allow_forwarded_traffic_vnet2"></a> [allow\_forwarded\_traffic\_vnet2](#input\_allow\_forwarded\_traffic\_vnet2) | Controls if forwarded traffic from VMs in the remote virtual network is allowed | `bool` | `false` | no |
| <a name="input_allow_forwarded_traffic_vnet_diff_subs"></a> [allow\_forwarded\_traffic\_vnet\_diff\_subs](#input\_allow\_forwarded\_traffic\_vnet\_diff\_subs) | Controls if forwarded traffic from VMs in the remote virtual network is allowed | `bool` | `false` | no |
| <a name="input_allow_gateway_transit_vnet1"></a> [allow\_gateway\_transit\_vnet1](#input\_allow\_gateway\_transit\_vnet1) | Controls gatewayLinks can be used in the remote virtual network’s link to the local virtual network. | `bool` | `false` | no |
| <a name="input_allow_gateway_transit_vnet2"></a> [allow\_gateway\_transit\_vnet2](#input\_allow\_gateway\_transit\_vnet2) | Controls gatewayLinks can be used in the remote virtual network’s link to the local virtual network. | `bool` | `false` | no |
| <a name="input_allow_gateway_transit_vnet_diff_subs"></a> [allow\_gateway\_transit\_vnet\_diff\_subs](#input\_allow\_gateway\_transit\_vnet\_diff\_subs) | Controls gatewayLinks can be used in the different subscription virtual network’s link to the local virtual network. | `bool` | `false` | no |
| <a name="input_allow_virtual_network_access"></a> [allow\_virtual\_network\_access](#input\_allow\_virtual\_network\_access) | Controls if the VMs in the remote virtual network can access VMs in the local virtual network. | `bool` | `true` | no |
| <a name="input_diff_subs_resource_group_name"></a> [diff\_subs\_resource\_group\_name](#input\_diff\_subs\_resource\_group\_name) | The name of remote resource group to be imported. | `string` | `""` | no |
| <a name="input_different_rg"></a> [different\_rg](#input\_different\_rg) | Flag to tell whether peering is to be done in same in resource group or different resource group | `bool` | `false` | no |
| <a name="input_enabled_diff_subs_peering"></a> [enabled\_diff\_subs\_peering](#input\_enabled\_diff\_subs\_peering) | n/a | `bool` | `false` | no |
| <a name="input_enabled_peering"></a> [enabled\_peering](#input\_enabled\_peering) | Set to false to prevent the module from creating any resources. | `bool` | `false` | no |
| <a name="input_resource_group_1_name"></a> [resource\_group\_1\_name](#input\_resource\_group\_1\_name) | The name of 1st existing resource group to be imported. | `string` | `""` | no |
| <a name="input_resource_group_2_name"></a> [resource\_group\_2\_name](#input\_resource\_group\_2\_name) | The name of 2nd existing resource group to be imported. | `string` | `""` | no |
| <a name="input_use_remote_gateways_vnet1"></a> [use\_remote\_gateways\_vnet1](#input\_use\_remote\_gateways\_vnet1) | Controls if remote gateways can be used on the local virtual network | `bool` | `false` | no |
| <a name="input_use_remote_gateways_vnet2"></a> [use\_remote\_gateways\_vnet2](#input\_use\_remote\_gateways\_vnet2) | Controls if remote gateways can be used on the local virtual network | `bool` | `false` | no |
| <a name="input_use_remote_gateways_vnet_diff_subs"></a> [use\_remote\_gateways\_vnet\_diff\_subs](#input\_use\_remote\_gateways\_vnet\_diff\_subs) | Controls if remote gateways can be used on the different subscription virtual network | `bool` | `false` | no |
| <a name="input_vnet_1_id"></a> [vnet\_1\_id](#input\_vnet\_1\_id) | The full Azure resource ID of the remote virtual network. Changing this forces a new resource to be created. | `string` | `""` | no |
| <a name="input_vnet_1_name"></a> [vnet\_1\_name](#input\_vnet\_1\_name) | The name of the virtual network. Changing this forces a new resource to be created. | `string` | `""` | no |
| <a name="input_vnet_2_id"></a> [vnet\_2\_id](#input\_vnet\_2\_id) | The full Azure resource ID of the remote virtual network. Changing this forces a new resource to be created. | `string` | `""` | no |
| <a name="input_vnet_2_name"></a> [vnet\_2\_name](#input\_vnet\_2\_name) | The name of the remote virtual network. | `string` | `""` | no |
| <a name="input_vnet_diff_subs_id"></a> [vnet\_diff\_subs\_id](#input\_vnet\_diff\_subs\_id) | The id of the remote virtual network. | `string` | `""` | no |
| <a name="input_vnet_diff_subs_name"></a> [vnet\_diff\_subs\_name](#input\_vnet\_diff\_subs\_name) | The name of the remote virtual network. | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_vnet_peer_1_id"></a> [vnet\_peer\_1\_id](#output\_vnet\_peer\_1\_id) | The id of the newly created virtual network peering in on first virtual netowork. |
| <a name="output_vnet_peer_1_name"></a> [vnet\_peer\_1\_name](#output\_vnet\_peer\_1\_name) | The name of the newly created virtual network peering in on first virtual netowork. |
| <a name="output_vnet_peer_2_id"></a> [vnet\_peer\_2\_id](#output\_vnet\_peer\_2\_id) | The id of the newly created virtual network peering in on second virtual netowork. |
| <a name="output_vnet_peer_2_name"></a> [vnet\_peer\_2\_name](#output\_vnet\_peer\_2\_name) | The name of the newly created virtual network peering in on second virtual netowork. |
| <a name="output_vnet_peer_diff_subs_id"></a> [vnet\_peer\_diff\_subs\_id](#output\_vnet\_peer\_diff\_subs\_id) | The id of the newly created virtual network peering in on different subscription virtual netowork. |
| <a name="output_vnet_peer_diff_subs_name"></a> [vnet\_peer\_diff\_subs\_name](#output\_vnet\_peer\_diff\_subs\_name) | The name of the newly created virtual network peering in on different subscription virtual netowork. |
<!-- END_TF_DOCS -->