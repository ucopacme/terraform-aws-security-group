# _Terraform Module: terraform-module-aws-security-group_
_Terraform module for_ **_AWS Security Group_**


## _General_

_This module may be used to create_ **_Security Group_**_

---


## _Usage_


_To use this module, add the following call to your code:_

```tf
module "sg" {
  source                 = "git::https://git@github.com/ahmadzaikk/terraform-module-aws-security-group.git//"
  enabled                = true
  name                   = "sg-name"
  vpc_id                 = "vpc-id"
  revoke_rules_on_delete = true
  ingress = [
    {
      from_port   = 0
      to_port     = 0
      protocol    = -1
      description = "Ingress rule that allows traffic from whitelisted ips"
      cidr_blocks = ["129.48.0.0/16", "10.0.0.0/16"]
    },
    {

      from_port       = 80
      to_port         = 80
      protocol        = "tcp"
      description     = "Ingress rule that allows traffic from whitelisted ips"
      security_groups = ["sg-id"]
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

  tags = {
    "ucop:application" = "app"
    "ucop:createdBy"   = "terraform"
    "ucop:environment" = "env"
    "ucop:group"       = "group"
    "ucop:source"      = join("/", ["https://github.com/ucopacme/ucop-terraform-deployments/terraform/chs-dev"])
    "Name"             = "Name"
  }

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
