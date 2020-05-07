# ArgoCD terraform module

Installs ArgoCD in the cluster via the operator. On OpenShift the module will also set up a route and
enable OpenShift Auth. On Kubernetes, an ingress will be created.

## Software dependencies

The module depends on the following software components:

- terraform v12
- kubectl
- helm terraform provider >= 1.1.1 (provided by terraform provider)

## Module dependencies

- Cluster
- OLM

## Example usage

```hcl-terraform
module "dev_tools_argocd" {
  source = "github.com/ibm-garage-cloud/terraform-tools-argocd.git?ref=v1.0.0"

  cluster_config_file = module.dev_cluster.config_file_path
  cluster_type        = module.dev_cluster.type
  app_namespace       = module.dev_cluster_namespaces.tools_namespace_name
  ingress_subdomain   = module.dev_cluster.ingress_hostname
  olm_namespace       = module.dev_software_olm.olm_namespace
  operator_namespace  = module.dev_software_olm.target_namespace
  name                = "argocd"
}
```
