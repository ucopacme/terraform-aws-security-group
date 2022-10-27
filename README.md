# _Terraform Module: terraform-module-aws-security-group_
_Terraform module for_ **_AWS Security Group_**


## _General_

_This module may be used to create_ **_Security Group_** _resources in AWS Cloud provider......._

---


## _Prerequisites_

_This module needs **_Terraform 0.12.23_** or newer._

_You can download the latest Terraform version from_ [_here_](https://www.terraform.io/downloads.html).

_This module deploys aws services details are in respective feature branches._

---

## _Features_

_Below we are able to check the resources that are being created as part of this module call:_

- **_Security Group_**


---

## _Usage_

## _Using this repo_

_To use this module, add the following call to your code:_

```tf
module "security_group" {
  source = "git::https://github.com/nitinda/terraform-module-aws-security-group.git?ref=master"

  name_prefix            = "ec2-sg-"
  description            = "EC2 Security Group that allows traffic from whitelisted ips"
  vpc_id                 = var.vpc_id
  revoke_rules_on_delete = true
  ingress = [
    {
        from_port   = 0
        to_port     = 0
        protocol    = -1
        description = "Ingress rule that allows traffic from whitelisted ips"
        cidr_blocks = [ module.network.vpc_cidr ]
    }
  ]
  egress = [
    {
      from_port   = 0
      to_port     = 0
      protocol    = "-1"
      cidr_blocks = ["0.0.0.0/0"]
      description = "The egress rule allows all ports"
    }
  ]
}
```


```tf
module "security_group" {
  source = "git::https://github.com/nitinda/terraform-module-aws-security-group.git?ref=master"

  name                   = "ec2-sg-"
  description            = "EC2 Security Group that allows traffic from whitelisted ips"
  vpc_id                 = var.vpc_id
  revoke_rules_on_delete = true
  ingress = [
    {
        from_port   = 0
        to_port     = 0
        protocol    = -1
        description = "Ingress rule that allows traffic from whitelisted ips"
        cidr_blocks = [ module.network.vpc_cidr ]
    }
  ]
  egress = [
    {
      from_port   = 0
      to_port     = 0
      protocol    = "-1"
      cidr_blocks = ["0.0.0.0/0"]
      description = "The egress rule allows all ports"
    }
  ]
}
```


```tf
module "security_group" {
  source = "git::https://github.com/nitinda/terraform-module-aws-security-group.git?ref=master"

  name                   = "ec2-sg-"
  description            = "EC2 Security Group that allows traffic from whitelisted ips"
  vpc_id                 = var.vpc_id
  revoke_rules_on_delete = true
}
```
---

## _Inputs_

_The variables required in order for the module to be successfully called from the deployment repository are the following:_

|**_Variable_** | **_Description_** | **_Type_** | **_Argument Status_** |
|:----|:----|-----:|:---:|
| **_name\_prefix_** | _Creates a unique name beginning with the specified prefix_ | _string_ | **_Optional <br/> (Default - null)_** |
| **_name_** | _The name of the security group_ | _string_ | **_Optional <br/> (Default - null)_** |
| **_description_** | _The security group description_ | _string_ | **_Optional <br/> (Default - null)_** |
| **_ingress_** | _Ingress rules for security group_ | _any_ | **_Optional <br/> (Default - [])_** |
| **_egress_** | _Egress rules for security group_ | _any_ | **_Optional <br/> (Default - [])_** |
| **_revoke\_rules\_on\_delete_** | _Instruct Terraform to revoke all of <br/> the Security Groups attached ingress and <br/> egress rules before deleting the rule itself_ | _bool_ | **_Optional <br/> (Default - false)_** |
| **_vpc\_id_** | _The VPC ID_ | _any_ | **_Optional <br/> (Default - null)_** |
| **_tags_** | _A mapping of tags to assign to the resource_ | _map(string)_ | **_Optional <br/> (Default - {})_** |


---


# _Outputs_

### _General_

_This module has the following outputs:_

- **_id_**
- **_arn_**
- **_name_**

---

### _Usage_

_In order for the variables to be accessed at module level please use the syntax below:_

```tf
module.<module_name>.<output_variable_name>
```


_The output variable is able to be accessed through terraform state file using the syntax below:_

```tf
data.terraform_remote_state.<layer_name>.<output_variable_name>
```

---
