1.  The correct Terraform command to remove the lock on the state for the current configuration is terraform force-unlock. This command is specifically designed to force unlock the state file and allow modifications to be made.
    The terraform force-unlock command can be used to remove the lock on the Terraform state for the current configuration. Another option is to use the "terraform state rm" command followed by the "terraform state push" command to forcibly overwrite the state on the remote backend, effectively removing the lock. It's important to note that these commands should be used with caution, as they can potentially cause conflicts and data loss if not used properly.

Be very careful forcing an unlock, as it could cause data corruption and problems with your state file.

[Terraform force-unlock documentation](https://developer.hashicorp.com/terraform/cli/commands/force-unlock)

2.  WHY MIGHT A USER OPT TO INCLUDE THE FOLLOWING SNIPPET IN THEIR CONFIGURATION FILE?

    terraform {
    required_version = ">= 1.9.2"
    }

The snippet specifies the minimum version of Terraform required to run the configuration, ensuring compatibility and preventing potential issues that may arise from using older versions
The required_version parameter in a terraform block is used to specify the minimum version of Terraform that is required to run the configuration. This parameter is optional, but it can be useful for ensuring that a Terraform configuration is only run with a version of Terraform that is known to be compatible.

For example, if your Terraform configuration uses features that were introduced in Terraform 1.9.2, you could include the following terraform block in your configuration to ensure that Terraform 1.9.2 or later is used

https://developer.hashicorp.com/terraform/language/settings#specifying-a-required-terraform-version

3.  Each Terraform workspace uses its own state file to manage the infrastructure associated with that workspace. This allows Terraform to manage multiple sets of infrastructure independently and avoid conflicts. Each Terraform workspace has its own Terraform state file that keeps track of the resources and their attributes, so changes made in one workspace will not affect the infrastructure managed by other workspaces.

In fact, having different state files provides the benefits of workspaces, where you can separate the management of infrastructure resources so you can make changes to specific resources without impacting resources in others....

https://developer.hashicorp.com/terraform/language/state/workspaces#workspace-internals

4.  Understanding how indexes work is essential when working with different variable types and resource blocks that use count or for_each. Therefore, what is the output value of the following code snippet?

variable "candy_list" {
type = list(string)
default = ["snickers", "kitkat", "reeces", "m&ms"]
}

output "give_me_candy" {
value = element(var.candy_list, 2)
}

The output value of the code snippet is "reeces" because the element function is used to access the element at index 2 in the candy_list variable, which is "reeces".
In this example, the candy_list variable is a list of strings, and the output block retrieves the third element in the list (at index 2) and outputs it as the value of give_me_candy.

Remember that an index starts at [0], and then counts up. Therefore, the following represents the index value as shown in the variable above:

[0] = snickers

[1] = kitkat

[2] = reeces

[3] = m&ms

https://developer.hashicorp.com/terraform/language/functions/index_function

https://developer.hashicorp.com/terraform/language/functions/element

5.  When using constraint expressions to signify a version of a provider, which of the following are valid provider versions that satisfy the expression found in the following code snippet: (select two)

terraform {
required_providers {
aws = {
source = "hashicorp/aws"
version ~> "5.36.0"
}
}
}

The version "5.36.9" satisfies the constraint expression "~> 5.36.0" as it falls within the same minor version range (5.36.x).
In Terraform, required_providers act as traffic controllers for your infrastructure tools. They ensure all modules use the right versions of providers like AWS or Azure, avoiding compatibility issues and guaranteeing everyone plays by the same rules. Think of them as a clear roadmap for your infrastructure setup, leading to consistent, predictable, and secure deployments.

A version constraint is a string literal containing one or more conditions, which are separated by commas.

Each condition consists of an operator and a version number.

Version numbers should be a series of numbers separated by periods (like 1.2.0), optionally with a suffix to indicate a beta release:

~>: Allows only the rightmost version component to increment. This format is referred to as the pessimistic constraint operator. For example, to allow new patch releases within a specific minor release, use the full version number:

~> 1.0.4: Allows Terraform to install 1.0.5 and 1.0.10 but not 1.1.0.

~> 1.1: Allows Terraform to install 1.2 and 1.10 but not 2.0.

https://developer.hashicorp.com/terraform/language/modules/syntax#version

https://developer.hashicorp.com/terraform/language/expressions/version-constraints#version-constraint-syntax
