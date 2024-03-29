## Summary
This module creates simple setup for a private gke cluster with its network setup and management vm that will have cluster access.

## How to use it
first configure your backend and provider check provider.tf and backend.tf in the root module, check the inputs table below for more configuration, also check submodules READMEs for full resource list.

Then:
```
terraform init
terraform apply
```
after you have the gke cluster and management vm up and ready execute the following command from your management vm that will initiate cluster connection: 

```
sh /gke_connection_init.sh
```
you will have output like that:
```
Fetching cluster endpoint and auth data.
kubeconfig entry generated for test-gke.
```
to test your connection:
```
kubectl get nodes
```
if your prompt similar to the following you are good to go.
```
NAME                                            STATUS   ROLES    AGE     VERSION
gke-test-gke-test-gke-node-pool-3e301953-fjt1   Ready    <none>   3m31s   v1.25.7-gke.1000
gke-test-gke-test-gke-node-pool-3e301953-qnc3   Ready    <none>   3m31s   v1.25.7-gke.1000
gke-test-gke-test-gke-node-pool-3e301953-xsl3   Ready    <none>   3m33s   v1.25.7-gke.1000
```

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.1 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >= 4.0.0 |

## Providers

No providers.

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_gke"></a> [gke](#module\_gke) | ./gke | n/a |
| <a name="module_vpc"></a> [vpc](#module\_vpc) | ./network | n/a |

## Resources

No resources.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_gke_cluster_name"></a> [gke\_cluster\_name](#input\_gke\_cluster\_name) | name for gke cluster | `string` | n/a | yes |
| <a name="input_gke_node_count"></a> [gke\_node\_count](#input\_gke\_node\_count) | gke cluster node count | `number` | `3` | no |
| <a name="input_gke_node_disk_size"></a> [gke\_node\_disk\_size](#input\_gke\_node\_disk\_size) | gke node disk size | `number` | `20` | no |
| <a name="input_gke_node_type"></a> [gke\_node\_type](#input\_gke\_node\_type) | gke node pool instance type | `string` | `"e2-small"` | no |
| <a name="input_management_subnet_cidr"></a> [management\_subnet\_cidr](#input\_management\_subnet\_cidr) | cidr for management subnet that contains the management vm instance | `string` | `"10.0.1.0/24"` | no |
| <a name="input_project_id"></a> [project\_id](#input\_project\_id) | gcp project id | `string` | n/a | yes |
| <a name="input_region"></a> [region](#input\_region) | gcp region | `string` | n/a | yes |
| <a name="input_restricted_subnet_cidr"></a> [restricted\_subnet\_cidr](#input\_restricted\_subnet\_cidr) | cidr for restricted subnet that contains the gke cluster | `string` | `"10.0.2.0/24"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_gke_cluster_name"></a> [gke\_cluster\_name](#output\_gke\_cluster\_name) | n/a |
| <a name="output_gke_management_vm_name"></a> [gke\_management\_vm\_name](#output\_gke\_management\_vm\_name) | n/a |
