# terraform-kubernetes

A terraform module for provisioning AWS resources (VMs, VPC, route table etc) for running a Kubernetes cluster.  Builds a multi-master, multi-AZ cluster for Kubernetes.

You can parameterise the number of masters, minions and availability zones to use.  Masters and minions will be round-robined across the availability zones.  For more information see [vars.tf](vars.tf).

To use:

```shell
$ echo >cluster.tf <<EOF
provider "aws" {
    access_key = "..."
    secret_key = "..."
    region = "..."
}

module "infra" {
    source = "github.com/weaveworks/terraform-kubernetes"

    cluster_name = "kubernetes_cluster"

    num_azs = 1
    num_minions = 1
	num_masters = 1

    key_pair_name = "test"
    elb_name = "test"
}
EOF
$ terraform get
$ terraform up
```
