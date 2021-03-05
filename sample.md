# Get Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code, or IaC. In this guide, you will progress through a few short steps to show you how to create a Terraform configuration, initialize it, create resources, and complete the procedure by destroying the configuration.

## Prerequisites
- Install Terraform ([Terraform.io](https://www.terraform.io/downloads.html))

## Create infrastructure

It's easy to create a new directory on your local machine to create configuration code within it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into main.tf.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Use the `init' command to initialize Terraform and install an AWS provider. 

```shell
$ terraform init
```

If the configuration runs without errors, continue by using the `apply` command to provision the resources. 

```shell
$ terraform apply
```

Several minutes may pass before a message in the output indicates the resources were created.

Finally, you destroy the infrastructure with the `destroy` command.

```shell
$ terraform destroy
```

A message will appear at the bottom of the output asking for confirmation. Type `yes` and the Enter/Return key. Terraform then destroys all the resources it created earlier.
