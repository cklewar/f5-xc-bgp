# F5-XC-BGP

This repository consists of Terraform templates to bring create a F5XC BGP object.

## Usage

- Clone this repo with: `git clone --recurse-submodules https://github.com/cklewar/f5-xc-bgp`
- Enter repository directory with: `cd f5-xc-bgp`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
- Initialize with: `terraform init`
- Apply with: `terraform apply -auto-approve` or destroy with: `terraform destroy -auto-approve`

### Example Output

```bash

```

## Create F5XC Namespace

```hcl
variable "project_prefix" {
  type        = string
  description = "prefix string put in front of string"
  default     = "aws"
}

variable "project_suffix" {
  type        = string
  description = "prefix string put at the end of string"
  default     = "01"
}

variable "f5xc_api_p12_file" {
  type = string
}

variable "f5xc_api_url" {
  type = string
}

variable "f5xc_tenant" {
  type = string
}

module "bgp" {
  source                = "./modules/f5xc/bgp"
  f5xc_namespace        = "system"
  f5xc_tenant           = var.f5xc_tenant
  f5xc_api_url          = var.f5xc_api_url
  f5xc_api_p12_file     = var.f5xc_api_p12_file
  f5xc_bgp_asn          = 65200
  f5xc_bgp_description  = "Neighbor Xyz"
  f5xc_bgp_name         = format("%s-bgp-%s", var.project_prefix, var.project_suffix)
  f5xc_bgp_peer_asn     = 65000
  f5xc_bgp_peer_name    = format("%s-peer-%s", var.project_prefix, var.project_suffix)
  f5xc_bgp_peer_address = "169.254.186.2"
  f5xc_site_name        = format("%s-%s", var.project_prefix, var.project_suffix)
}
```