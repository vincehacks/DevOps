# DevOps

Created by Vince Chang </br>

- Need tools to **_configure_** and tools to **_provision_**
  I used AWS to host a Virtual Machine and configured Chef. I created an
  organization on Chef.io where I created and pushed cookbooks.

#### Chef

- **_Node_**: Virtual Machine
- **_Resource_**: Represents a element on a machine I want to do something to
- **_Recipe_**: A collection of resources; command to do to a node
- **_Cookbook_**: A list/collection of recipes
- **_Knife_**: Mainly for working with the `Chef Server`
  - **_Configuration for Knife_**: `.pem` and `knife.rb` that lives in `.chef`
- Use Chef to do a `chef generate` to start up
- `chef-client -z -r "recipe[workstation::setup]"` : use this to apply a
  cookbook to a node
- Use this to configure a VM that already exists
- Before pushing a cookbook to the server, you need to update the version number
  in `metadata.rb`
- `berks install`: cookbook management
- `berks upload`: upload the cookbook to the server

#### Kitchen

- This is a testing utility
- `.kitchen.yml` is a testing file
- `inspect` and `serverspec` are not a part of `chef`, but are commonly used

1. `Create`: creates the instance, brings out the testing environment
2. `Converge`: applies the cookbooks to the testing environment
3. `Verify`: based upon the config file, it will use a verifier that is
   specified, if any, and look for the verifier framework we are using (serverspec)
4. `Destroy`: destroys the entire testing environment
5. `Test`: Does the entire life cycle of 1-4 (quick command)

- Can run tests on multiple OS systems
- Need to install the connection between Chef and Docker

#### Ohai

- How `Chef` produces an inventory of a node
- `ohai`: this is a .json of the inventory of the os
  - `ohai` is run at the startup
  - it is a chef utility that complies all the system information
  - can access the information using the node object in recipes
- `knife` : manipulating the chef server remotely
  `knife bootstrap ip-172-31-16-158.us-west-2.compute.internal -i ~/vccentos.pem -u vincechang -N node1`
  - : gets the chef node up and running on the new VM

#### Terraform

- Terraform is a provisioner, this creates the infrastructure, Chef on the other
  hand will configure what has been provisioned
- Command line tool
  1. `terraform init`: sets up
  2. `terraform plan`: shows what Terraform is going to do when you execute,
     doesn't do it, just validates what I want to do
  3. `terraform apply`: executes the script itself
