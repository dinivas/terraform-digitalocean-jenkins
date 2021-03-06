# Terraform Openstack Jenkins

Terraform module that install Jenkins in Openstack using provided infos

## Examples

```
module "jenkins" {
  source = "../../"

  enable_jenkins_master              = "1"
  jenkins_master_name                = "jenkins-test"
  jenkins_master_instance_count      = 1
  jenkins_master_image_name          = "Jenkins Master"
  jenkins_master_compute_flavor_name = "dinivas.large"
  jenkins_master_keypair_name        = "my-keypair"
  jenkins_master_network             = "my-network"
  jenkins_master_subnet              = "my-subnet"
  jenkins_master_floating_ip_pool    = ""
}
```

## Inputs

```

variable "enable_jenkins_master" {
  type    = "string"
  default = "1"
}

variable "jenkins_master_name" {
  description = "The name of the master instance"
  type        = "string"
}

variable "jenkins_master_instance_count" {
  description = "Number of master instances"
  default     = 1
}

variable "jenkins_master_image_name" {
  description = "The Image name of the master instance"
  type        = "string"
}

variable "jenkins_master_compute_flavor_name" {
  description = "The Flavor name of the master instance"
  type        = "string"
}


variable "jenkins_master_keypair_name" {
  description = "The Keypair name of the master instance"
  type        = "string"
}

variable "jenkins_master_floating_ip_pool" {
  description = "The floating Ip pool of the master instance"
  type        = "string"
  default     = ""
}


variable "jenkins_master_network" {
  description = "The Network name of the master instance"
  type        = "string"
}

variable "jenkins_master_subnet" {
  description = "The Network subnet name of the master instance"
  type        = "string"
}

variable "jenkins_master_security_group_rules" {
  type        = list(map(any))
  default     = []
  description = "The definition os security groups to associate to instance. Only one is allowed"
}

variable "jenkins_master_security_groups_to_associate" {
  type        = "string"
  default     = ""
  description = "List of existing security groups to associate to Jenkins masters."
}

variable "jenkins_master_metadata" {
  default = {}
}



```

## Outputs

```
output "jenkins_master_instance_ids" {
  value = "${module.jenkins_master_instance.ids}"
}

output "jenkins_master_floating_ip" {
  value       = "${openstack_networking_floatingip_v2.jenkins_master_floatingip}"
  description = "The floating ips bind to Jenkins master"
}
```