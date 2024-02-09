# Terraform-google-gke
# Terraform Google Cloud Gke Module
## Table of Contents

- [Introduction](#introduction)
- [Usage](#usage)
- [Examples](#examples)
- [License](#license)
- [Author](#author)
- [Inputs](#inputs)
- [Outputs](#outputs)

## Introduction
This project deploys a Google Cloud infrastructure using Terraform to create Gke .
## Usage
To use this module, you should have Terraform installed and configured for GCP. This module provides the necessary Terraform configuration for creating GCP resources, and you can customize the inputs as needed. Below is an example of how to use this module:
# Example: gke
```hcl
module "gke" {
  source             = "cypik/gke/google"
  version            = "1.0.0"
  name               = "app"
  environment        = "test"
  region             = "asia-northeast1"
  image_type         = "UBUNTU_CONTAINERD"
  location           = "asia-northeast1"
  min_master_version = "1.27.8-gke.1067004"
  network            = module.vpc.vpc_id
  subnetwork         = module.subnet.subnet_id
  service_account    = module.service-account.account_email
  initial_node_count = 1
  min_node_count     = 1
  max_node_count     = 1
  disk_size_gb       = 20
  cluster_enabled    = true
}
```
This example demonstrates how to create various GCP resources using the provided modules. Adjust the input values to suit your specific requirements.

## Examples
For detailed examples on how to use this module, please refer to the [Examples](https://github.com/cypik/terraform-google-gke/tree/master/example) directory within this repository.

## Author
Your Name Replace **MIT** and **Cypik** with the appropriate license and your information. Feel free to expand this README with additional details or usage instructions as needed for your specific use case.

## License
This project is licensed under the **MIT** License - see the [LICENSE](https://github.com/cypik/terraform-google-gke/blob/master/LICENSE) file for details.

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.6.6 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >= 3.50, < 5.11.0 |
| <a name="requirement_null"></a> [null](#requirement\_null) | 3.2.2 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_google"></a> [google](#provider\_google) | >= 3.50, < 5.11.0 |
| <a name="provider_null"></a> [null](#provider\_null) | 3.2.2 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_labels"></a> [labels](#module\_labels) | cypik/labels/google | 1.0.1 |

## Resources

| Name | Type |
|------|------|
| [google_container_cluster.primary](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster) | resource |
| [google_container_node_pool.node_pool](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_node_pool) | resource |
| [null_resource.configure_kubectl](https://registry.terraform.io/providers/hashicorp/null/3.2.2/docs/resources/resource) | resource |
| [google_client_config.current](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/client_config) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_auto_repair"></a> [auto\_repair](#input\_auto\_repair) | Enables or disables automatic repair of nodes in the cluster. | `bool` | `true` | no |
| <a name="input_auto_upgrade"></a> [auto\_upgrade](#input\_auto\_upgrade) | Enables or disables automatic upgrades of nodes in the cluster. | `bool` | `true` | no |
| <a name="input_cluster_create_timeouts"></a> [cluster\_create\_timeouts](#input\_cluster\_create\_timeouts) | Timeout for creating the cluster. | `string` | `"30m"` | no |
| <a name="input_cluster_delete_timeouts"></a> [cluster\_delete\_timeouts](#input\_cluster\_delete\_timeouts) | Timeout for deleting the cluster. | `string` | `"30m"` | no |
| <a name="input_cluster_enabled"></a> [cluster\_enabled](#input\_cluster\_enabled) | Flag to control the cluster\_enabled creation. | `bool` | `true` | no |
| <a name="input_cluster_update_timeouts"></a> [cluster\_update\_timeouts](#input\_cluster\_update\_timeouts) | Timeout for updating the cluster. | `string` | `"30m"` | no |
| <a name="input_disk_size_gb"></a> [disk\_size\_gb](#input\_disk\_size\_gb) | Size of the disk in gigabytes for each node in the cluster. | `number` | `10` | no |
| <a name="input_disk_type"></a> [disk\_type](#input\_disk\_type) | Type of disk to use for the nodes in the cluster. | `string` | `""` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| <a name="input_image_type"></a> [image\_type](#input\_image\_type) | Type of image to use for the nodes in the cluster. | `string` | `""` | no |
| <a name="input_initial_node_count"></a> [initial\_node\_count](#input\_initial\_node\_count) | The number of nodes to create in this cluster's default node pool. | `number` | `1` | no |
| <a name="input_kubectl_config_path"></a> [kubectl\_config\_path](#input\_kubectl\_config\_path) | Path to the kubectl config file. Defaults to $HOME/.kube/config | `string` | `""` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | Label order, e.g. sequence of application name and environment `name`,`environment`,'attribute' [`webserver`,`qa`,`devops`,`public`,] . | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| <a name="input_location"></a> [location](#input\_location) | The location (region or zone) in which the cluster master will be created, as well as the default node location. | `string` | `""` | no |
| <a name="input_location_policy"></a> [location\_policy](#input\_location\_policy) | Specifies the policy for distributing nodes across locations, with the default being BALANCED | `string` | `"BALANCED"` | no |
| <a name="input_machine_type"></a> [machine\_type](#input\_machine\_type) | Specifies the machine type for the nodes in the cluster. | `string` | `""` | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy, eg 'cypik'. | `string` | `"cypik"` | no |
| <a name="input_max_node_count"></a> [max\_node\_count](#input\_max\_node\_count) | Maximum number of nodes in the cluster. | `number` | `1` | no |
| <a name="input_min_master_version"></a> [min\_master\_version](#input\_min\_master\_version) | The minimum version of the master. | `string` | `""` | no |
| <a name="input_min_node_count"></a> [min\_node\_count](#input\_min\_node\_count) | Minimum number of nodes in the cluster. | `number` | `1` | no |
| <a name="input_module_enabled"></a> [module\_enabled](#input\_module\_enabled) | Flag to control the service\_account\_enabled creation. | `bool` | `true` | no |
| <a name="input_name"></a> [name](#input\_name) | Name of the resource. Provided by the client when the resource is created. | `string` | `"test"` | no |
| <a name="input_network"></a> [network](#input\_network) | A reference (self link) to the VPC network to host the cluster in | `string` | `""` | no |
| <a name="input_preemptible"></a> [preemptible](#input\_preemptible) | Specifies whether the nodes in the cluster should be preemptible. | `bool` | `false` | no |
| <a name="input_region"></a> [region](#input\_region) | Google Cloud region | `string` | `"asia-northeast1"` | no |
| <a name="input_remove_default_node_pool"></a> [remove\_default\_node\_pool](#input\_remove\_default\_node\_pool) | deletes the default node pool upon cluster creation. | `bool` | `true` | no |
| <a name="input_repository"></a> [repository](#input\_repository) | Terraform current module repo | `string` | `"https://github.com/cypik/terraform-google-gke"` | no |
| <a name="input_service_account"></a> [service\_account](#input\_service\_account) | The Google Cloud Platform Service Account to be used by the node VMs created by GKE Autopilot or NAP. | `string` | `""` | no |
| <a name="input_subnetwork"></a> [subnetwork](#input\_subnetwork) | A reference (self link) to the subnetwork to host the cluster in | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_client_certificate"></a> [client\_certificate](#output\_client\_certificate) | Base64 encoded public certificate used by clients to authenticate to the cluster endpoint. |
| <a name="output_client_key"></a> [client\_key](#output\_client\_key) | Base64 encoded private key used by clients to authenticate to the cluster endpoint. |
| <a name="output_cluster_autoscaling"></a> [cluster\_autoscaling](#output\_cluster\_autoscaling) | Specifies the Auto Upgrade knobs for the node pool. |
| <a name="output_cluster_ca_certificate"></a> [cluster\_ca\_certificate](#output\_cluster\_ca\_certificate) | Base64 encoded public certificate that is the root certificate of the cluster. |
| <a name="output_cluster_location"></a> [cluster\_location](#output\_cluster\_location) | Location of the GKE cluster that GitLab is deployed in. |
| <a name="output_cluster_name"></a> [cluster\_name](#output\_cluster\_name) | an identifier for the resource with format |
| <a name="output_endpoint"></a> [endpoint](#output\_endpoint) | The IP address of this cluster's Kubernetes master. |
| <a name="output_id"></a> [id](#output\_id) | an identifier for the resource with format |
| <a name="output_instance_group_urls"></a> [instance\_group\_urls](#output\_instance\_group\_urls) | The resource URLs of the managed instance groups associated with this node pool. |
| <a name="output_label_fingerprint"></a> [label\_fingerprint](#output\_label\_fingerprint) | an identifier for the resource with format |
| <a name="output_maintenance_policy"></a> [maintenance\_policy](#output\_maintenance\_policy) | Duration of the time window, automatically chosen to be smallest possible in the given scenario. |
| <a name="output_master_version"></a> [master\_version](#output\_master\_version) | The current version of the master in the cluster. |
| <a name="output_node_id"></a> [node\_id](#output\_node\_id) | An identifier for the resource with format. |
| <a name="output_self_link"></a> [self\_link](#output\_self\_link) | The server-defined URL for the resource. |
| <a name="output_services_ipv4_cidr"></a> [services\_ipv4\_cidr](#output\_services\_ipv4\_cidr) | The IP address range of the Kubernetes services in this cluster |
| <a name="output_tpu_ipv4_cidr_block"></a> [tpu\_ipv4\_cidr\_block](#output\_tpu\_ipv4\_cidr\_block) | The IP address range of the Cloud TPUs in this cluster, |
<!-- END_TF_DOCS -->