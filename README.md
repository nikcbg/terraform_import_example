# terraform_import_example

### Purpose of the repository

The `terraform import` command is used to import existing infrastructure, in this case EC2 instance (Ubuntu 16.04 server) in AWS. The command currently can only import one resource at a time. This means you can't yet point Terraform import to an entire collection of resources.

---------------------------------------------------------------------------------------------------------------------

### How to use this repository

- install `terraform` from [here](https://www.terraform.io/downloads.html).
- setup Amazon Web Services (AWS) account [here](https://aws.amazon.com/).
- configure your AWS access keys [here](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).
- configure your AWS access keys as environment variables so you can authenticate to your AWS account:

```
export AWS_ACCESS_KEY_ID="your access key id here"
export AWS_SECRET_ACCESS_KEY="your secret access key here"
```
- make sure you have running instance in AWS. 
- clone the repo on your computer by executing `git clone git@github.com:nikcbg/terraform_import_example.git`.
- go to the folder where you clone the repo `cd terraform_import_example.git`.
- execute `terraform init` to download the necessary plugins.
- execute `terraform import aws_instance.example i-abcd1234`
  - i-abcd1234 is the existing instance ID in AWS.
  - you will be asked to enter the region where the instance is running.
- the output of the `import` command should display the following:

```
provider.aws.region
  The region where AWS operations will take place. Examples
  are us-east-1, us-west-2, etc.

  Default: us-east-1
  Enter a value: us-east-1

aws_instance.example: Importing from ID "i-abcd1234"...
aws_instance.example: Import complete!
  Imported aws_instance (ID: i-abcd1234)
aws_instance.example: Refreshing state... (ID: i-abcd1234)

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.

```
- now you can manage the existing EC2 instance in AWS.

----------------------------------------------------------------------------------------------------------------------------

### Managing the existing resource and adding more resources

- this is very basic modification of the existing terraform code that will add more EC2 instances.
- add the below code to the existing code in the `main.tf` file:
  ```
  provider "aws" {
    region = "us-east-1"
  }
  resource "aws_instance" "example" {
    ami = "ami-0f9cf087c1f27d9b1"
    instance_type = "t2.micro"
    count = "5"
  }

  ```
  
- the code will create 5 EC2 instances in US east region that have baseline level of CPU (t2.micro)
- execute `terraform plan` after modifying the code, the output should display the following:

```
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  + aws_instance.example[1]
      id:                           <computed>
      ami:                          "ami-0f9cf087c1f27d9b1"
      arn:                          <computed>
      associate_public_ip_address:  <computed>
      availability_zone:            <computed>
      cpu_core_count:               <computed>
      cpu_threads_per_core:         <computed>
      ebs_block_device.#:           <computed>
      ephemeral_block_device.#:     <computed>
      get_password_data:            "false"
      host_id:                      <computed>
      instance_state:               <computed>
      instance_type:                "t2.micro"
      ipv6_address_count:           <computed>
      ipv6_addresses.#:             <computed>
      key_name:                     <computed>
      network_interface.#:          <computed>
      network_interface_id:         <computed>
      password_data:                <computed>
      placement_group:              <computed>
      primary_network_interface_id: <computed>
      private_dns:                  <computed>
      private_ip:                   <computed>
      public_dns:                   <computed>
      public_ip:                    <computed>
      root_block_device.#:          <computed>
      security_groups.#:            <computed>
      source_dest_check:            "true"
      subnet_id:                    <computed>
      tenancy:                      <computed>
      volume_tags.%:                <computed>
      vpc_security_group_ids.#:     <computed>

  + aws_instance.example[2]
      id:                           <computed>
      ami:                          "ami-0f9cf087c1f27d9b1"
      arn:                          <computed>
      associate_public_ip_address:  <computed>
      availability_zone:            <computed>
      cpu_core_count:               <computed>
      cpu_threads_per_core:         <computed>
      ebs_block_device.#:           <computed>
      ephemeral_block_device.#:     <computed>
      get_password_data:            "false"
      host_id:                      <computed>
      instance_state:               <computed>
      instance_type:                "t2.micro"
      ipv6_address_count:           <computed>
      ipv6_addresses.#:             <computed>
      key_name:                     <computed>
      network_interface.#:          <computed>
      network_interface_id:         <computed>
      password_data:                <computed>
      placement_group:              <computed>
      primary_network_interface_id: <computed>
      private_dns:                  <computed>
      private_ip:                   <computed>
      public_dns:                   <computed>
      public_ip:                    <computed>
      root_block_device.#:          <computed>
      security_groups.#:            <computed>
      source_dest_check:            "true"
      subnet_id:                    <computed>
      tenancy:                      <computed>
      volume_tags.%:                <computed>
      vpc_security_group_ids.#:     <computed>

  + aws_instance.example[3]
      id:                           <computed>
      ami:                          "ami-0f9cf087c1f27d9b1"
      arn:                          <computed>
      associate_public_ip_address:  <computed>
      availability_zone:            <computed>
      cpu_core_count:               <computed>
      cpu_threads_per_core:         <computed>
      ebs_block_device.#:           <computed>
      ephemeral_block_device.#:     <computed>
      get_password_data:            "false"
      host_id:                      <computed>
      instance_state:               <computed>
      instance_type:                "t2.micro"
      ipv6_address_count:           <computed>
      ipv6_addresses.#:             <computed>
      key_name:                     <computed>
      network_interface.#:          <computed>
      network_interface_id:         <computed>
      password_data:                <computed>
      placement_group:              <computed>
      primary_network_interface_id: <computed>
      private_dns:                  <computed>
      private_ip:                   <computed>
      public_dns:                   <computed>
      public_ip:                    <computed>
      root_block_device.#:          <computed>
      security_groups.#:            <computed>
      source_dest_check:            "true"
      subnet_id:                    <computed>
      tenancy:                      <computed>
      volume_tags.%:                <computed>
      vpc_security_group_ids.#:     <computed>

  + aws_instance.example[4]
      id:                           <computed>
      ami:                          "ami-0f9cf087c1f27d9b1"
      arn:                          <computed>
      associate_public_ip_address:  <computed>
      availability_zone:            <computed>
      cpu_core_count:               <computed>
      cpu_threads_per_core:         <computed>
      ebs_block_device.#:           <computed>
      ephemeral_block_device.#:     <computed>
      get_password_data:            "false"
      host_id:                      <computed>
      instance_state:               <computed>
      instance_type:                "t2.micro"
      ipv6_address_count:           <computed>
      ipv6_addresses.#:             <computed>
      key_name:                     <computed>
      network_interface.#:          <computed>
      network_interface_id:         <computed>
      password_data:                <computed>
      placement_group:              <computed>
      primary_network_interface_id: <computed>
      private_dns:                  <computed>
      private_ip:                   <computed>
      public_dns:                   <computed>
      public_ip:                    <computed>
      root_block_device.#:          <computed>
      security_groups.#:            <computed>
      source_dest_check:            "true"
      subnet_id:                    <computed>
      tenancy:                      <computed>
      volume_tags.%:                <computed>
      vpc_security_group_ids.#:     <computed>


Plan: 4 to add, 0 to change, 0 to destroy.

```
- as you can see terraform will create only 4 resources (EC2 instances) in this case, this is because the fifth resource was imported initially and terraform will not recreate it.
- next execute `terraform apply` to apply the changes, the output should display the following:

```
aws_instance.example[4]: Creation complete after 27s (ID: i-0e29c8f37a83e6e27)
aws_instance.example[1]: Creation complete after 38s (ID: i-0ff0f40bb02d23806)
aws_instance.example[3]: Creation complete after 38s (ID: i-0ee0e01f751fb9d2d)
aws_instance.example[2]: Creation complete after 48s (ID: i-07569e6e68f6f44af)

Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
```
- next you can destroy all resources by executing `terraform destroy`, the output should display the following:

```
Terraform will perform the following actions:

  - aws_instance.example[0]
  - aws_instance.example[1]
  - aws_instance.example[2]
  - aws_instance.example[3]
  - aws_instance.example[4]

Plan: 0 to add, 0 to change, 5 to destroy.

aws_instance.example[4]: Destruction complete after 54s
aws_instance.example[3]: Destruction complete after 54s
aws_instance.example[1]: Destruction complete after 1m15s
aws_instance.example[0]: Destruction complete after 1m15s
aws_instance.example[2]: Destruction complete after 2m51s

Destroy complete! Resources: 5 destroyed.
```
