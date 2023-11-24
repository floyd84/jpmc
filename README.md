```

terraorm exam reference links :

https://www.examtopics.com/exams/hashicorp/terraform-associate/view/

https://developer.hashicorp.com/terraform/language/providers


```

cicd pipeline :


https://github.com/ramannkhanna2/Ddevops-terraform-ansiblee.git


```



https://github.com/ramannkhanna2/tteraform-aws-moduless.git

# jpmc

https://github.com/ramannkhanna2/TF-advanced.git

```

https://cloud2.rpsconsulting.in/console/#/

Rps@12345

```

```

--------------

Ubuntu Server 20.04 LTS (HVM), SSD Volume Type

t2.medium

ramanvirg1 (.pem)

storage : 20 gb

```

```

https://developer.hashicorp.com/terraform/install?product_intent=terraform

```


```
https://developer.hashicorp.com/terraform/install?product_intent=terraform



https://registry.terraform.io/

providers block
resource blocks


-- https://registry.terraform.io/providers/hashicorp/aws/latest/docs


--authentication : authenticating our ,main server to our aws account
aws configure


sudo -i
apt update -y
apt install -y unzip
apt install -y wget
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#cliv2-linux-install (copy the three commands)
ln -s  /usr/local/bin/aws  /usr/bin/
aws --version --To get the version of aws

```

```

--authentication : authenticating our ,main server to our aws account
aws configure

root@ip-172-31-10-175:~# aws s3 ls

Unable to locate credentials. You can configure credentials by running "aws configure".
root@ip-172-31-10-175:~# aws configure
AWS Access Key ID [None]: AKIAT2EFG
AWS Secret Access Key [None]: yT3K2CPNm3e9pZJXw
Default region name [None]: ap-south-1
Default output format [None]: 
root@ip-172-31-10-175:~# aws s3 ls

```


```

root@ip-172-31-10-175:~# cat ec2.tf 

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-02a2af70a66af6dfb"
  instance_type = "t2.micro"

  tags = {
    Name = "HelloWorld"
  }
}

```

```
terraform validate
   95  ls
   96  terraform plan
   97  terraform apply
   98  vi ec2.tf 
   99  terraform apply
  100  cat ec2.tf 
  101  terraform apply
  102  vi ec2.tf 
  103  terraform apply
  104  clear
  105  ls
  106  cat terraform.tfstate
  107  clear
  108  ls
  109  vi ec2.tf 
  110  cat terraform.tfstate
  111  clear
  112  vi ec2.tf 
  113  terraform validate
  114  vi ec2.tf 
  115  terraform validate
  116  terraform plan
  117  cat ec2.tf 
  118  terraform apply
  119  clear
  120  cat terraform.tfstate
  121  clear
  122  cat ec2.tf 
  123  clear
  124  terraform validate
  125  terraform plan
  126  cat ec2.tf 
  127  terraform apply -auto-approve
  128  terraform apply
  129  clear
  130  vi ec2.tf 
  131  ls
  132  rm -rf terraform.tfstate terraform.tfstate.backup 
  133  clear
  134  terraform plan
  135  terraform apply
  136  clear
  137  ls
  138  terraform plan
  139  terraform apply
  140  clear
  141  cat ec2.tf 
  142  vi ec2.tf 
  143  terraform apply
  144  terraform state list
  145  clear
  146  vi ec2.tf 
  147  terraform apply -auto-approve
  148  clear
  149  terraform destroy
```


```
root@ip-172-31-10-175:~# cat ec2.tf 
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0a7cf821b91bcccbc"
  instance_type = "t2.micro"

  tags = {
    Name = "HelloWorld"
  }
}

resource "aws_instance" "web2" {
  ami           = "ami-0a7cf821b91bcccbc"
  availability_zone= "ap-south-1a"
  instance_type = "t2.micro"

  tags = {
    Name = "HelloWorld22"
  }
```



```

provider "github" {
  token="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"
}



resource "github_repository" "example" {
  name        = "raman-jpmc-test-repo"
  description = "My awesome codebase"

  visibility = "public"

}

```

```
root@ip-172-31-11-146:~# cat azure.tf 
provider "azurerm" {
features{}
}



resource "azurerm_resource_group" "rg" {
  name     = "raman-tf-resources"
  location = "Australia East"
}

resource "azurerm_public_ip" "example" {
  name                = "acceptanceTestPublicIp1"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  allocation_method   = "Static"

  tags = {
    environment = "Production"
  }
}




resource "azurerm_virtual_network" "network" {
  name                = "raman-network"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}

resource "azurerm_subnet" "subnet" {
  name                 = "raman-subnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.network.name
  address_prefixes     = ["10.0.2.0/24"]
}

resource "azurerm_network_interface" "nic" {
  name                = "raman-nic"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    public_ip_address_id= azurerm_public_ip.example.id
    private_ip_address_allocation = "Dynamic"
  }
}


resource "azurerm_linux_virtual_machine" "vm" {
  name                = "raman-machine"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  size                = "Standard_F2"
  disable_password_authentication="false"
  admin_username      = "adminuser"
  admin_password      = "Rmankhn@2023"
  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "16.04-LTS"
    version   = "latest"

#az vm image list --offer CentOS --all
  }
}


```


```

root@ip-172-31-11-146:~# cat ec2.tf 
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0a7cf821b91bcccbc"
  instance_type = var.type
  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
  tags = {
    Name = var.name
  }
}

resource "aws_instance" "web2" {
  ami           = "ami-0a7cf821b91bcccbc"
  instance_type = var.type
#  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
   vpc_security_group_ids= [aws_security_group.sg.id]
  tags = {
    Name = var.name
  }
}

resource "aws_security_group" "sg" {
  name        = "training-sg"
  description = "training-sg"
  vpc_id      = "vpc-027b7a70751225ee4"

  ingress {
    description      = "TLS from VPC"
    from_port        = 443
    to_port          = 443
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 80
    to_port          = 80
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 3389
    to_port          = 3389
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 636
    to_port          = 636
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }





  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = [var.cidr]
  }

  tags = {
    Name = "training-sg"
  }
}



```

```

variable type {
default="t3.micro"
}

variable name {
default="ramanserver-jpmc"
}

variable cidr {
default="0.0.0.0/0"
}                                                                                                                                                                            
```


```
LIST AND MAPS :


root@ip-172-31-11-146:~# cat ec2.tf 
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0a7cf821b91bcccbc"
#  instance_type = var.type[0]
  instance_type=var.types["dev"]
  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
  tags = {
    Name = var.name[0]
  }
}

resource "aws_instance" "web2" {
  ami           = "ami-0a7cf821b91bcccbc"
#  instance_type = var.type[2]
   instance_type=var.types["prod"]
#  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
   vpc_security_group_ids= [aws_security_group.sg.id]
  tags = {
    Name = var.name[1]
  }
}

resource "aws_security_group" "sg" {
  name        = "training-sg"
  description = "training-sg"
  vpc_id      = "vpc-027b7a70751225ee4"

  ingress {
    description      = "TLS from VPC"
    from_port        = 443
    to_port          = 443
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 80
    to_port          = 80
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 3389
    to_port          = 3389
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 636
    to_port          = 636
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }





  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = [var.cidr]
  }

  tags = {
    Name = "training-sg"
  }
}




```

LIST AND MAPS

```
root@ip-172-31-11-146:~# cat variable.tf 
/*
variable type {
type=list
default= ["t2.micro","t3.micro","t2.medium"]
}

*/

variable name {
type= list
default=["ramanserver-1","raman-server-2"]
}

variable cidr {
default="10.0.0.0/24"
}

variable types {
type=map
default= {
dev="t2.micro"
uat="t3.micro"
prod="t2.medium"
}
}
```


```
Variable usage and heirarchy :


root@ip-172-31-11-146:~# cat ec2.tf 
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0a7cf821b91bcccbc"
#  instance_type = var.type[0]
  instance_type=var.types
  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
  tags = {
    Name = var.name[0]
  }
}

resource "aws_instance" "web2" {
  ami           = "ami-0a7cf821b91bcccbc"
#  instance_type = var.type[2]
   instance_type=var.types
#  vpc_security_group_ids=  ["sg-091098ee7a282d63f"]
   vpc_security_group_ids= [aws_security_group.sg.id]
  tags = {
    Name = var.name[1]
  }
}

resource "aws_security_group" "sg" {
  name        = "training-sg"
  description = "training-sg"
  vpc_id      = "vpc-027b7a70751225ee4"

  ingress {
    description      = "TLS from VPC"
    from_port        = 443
    to_port          = 443
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 80
    to_port          = 80
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 3389
    to_port          = 3389
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }

  ingress {
    description      = "TLS from VPC"
    from_port        = 636
    to_port          = 636
    protocol         = "tcp"
    cidr_blocks      = [var.cidr]
  }





  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = [var.cidr]
  }

  tags = {
    Name = "training-sg"
  }
}


```

```

root@ip-172-31-11-146:~# cat custom.tfvars 
types="t2.medium"
```

```
root@ip-172-31-11-146:~# cat custom.tfvars 
types="t2.medium"
root@ip-172-31-11-146:~# cat custom.tfvars cat variable.tf 
types="t2.medium"
cat: cat: No such file or directory
/*
variable type {
type=list
default= ["t2.micro","t3.micro","t2.medium"]
}

*/

variable name {
type= list
default=["ramanserver-1","raman-server-2"]
}

variable cidr {
default="10.0.0.0/24"
}

variable types {
default="t2.micro"
}

```


```
terraform plan -var-file "custom.tfvars"

terraform plan -var-file "custom.tfvars" -var cidr="10.0.0.0/24" -var types="t3.micro"
```



```

PROVISONER -REMOTE :


root@ip-172-31-11-146:~/provisioner# terraform state list
aws_instance.myec2
aws_security_group.allow_ssh
root@ip-172-31-11-146:~/provisioner# cat remote.tf 
provider "aws" {
region="ap-south-1"
}




resource "aws_instance" "myec2" {
   ami = "ami-0d92749d46e71c34c"                               #amazon linux ami
   instance_type = "t2.micro"
   key_name = "raman-virg1"                                 # Create a keypair in the region #
   vpc_security_group_ids  = [aws_security_group.allow_ssh.id]
   tags= {
   Name= "web-server"
   }

   provisioner "remote-exec" {
     inline = [
       "sudo amazon-linux-extras install -y nginx1.12",
       "sudo systemctl start nginx"
     ]

   connection {
     type = "ssh"
     user = "ec2-user"
     private_key = file("./raman.pem")    #copy the content of the private keyfile ; create a file in /root/app1 named nvirginia.pem and then paste the content into this file #
     host = self.public_ip
 #   host=aws_instance.myec2.public_ip
   }
   }
}

### NOTE - Adding a new security group resource to allow the terraform provisioner from laptop to connect to EC2 Instance via SSH.


resource "aws_security_group" "allow_ssh" {
  name        = "allow_ssh"
  description = "Allow SSH inbound traffic"
  vpc_id      = "vpc-027b7a70751225ee4"

  ingress {
    description = "SSH into VPC"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  
 ingress {
    description = "SSH into VPC"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    description = "Outbound Allowed"
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

```



FUNCATIONS :

```

oot@ip-172-31-11-146:~/func# cat func.tf 
provider "aws" {
  region     = var.region
}

locals {
  time = formatdate("DD MMM YYYY hh:mm ZZZ", timestamp())
}




resource "aws_instance" "app-dev" {
   ami = lookup(var.ami,var.region)  #in terraform console: lookup({us-east-1="ami1",us-east-2="ami2",ap-south-1="ami3"},"ap-south-1","NA") #
   instance_type = "t2.micro"
   count = 2

   tags = {
     Name = element(var.tags,count.index)    # element(["firstec2","secondec2"],1) #
   }
}

output "timestamp" {
  value = local.time
}

/*
output "prvateip" {
  value = aws_instance.app-dev[count.index].private_ip
}
*/


```

```

root@ip-172-31-11-146:~/func# cat variable.tf 
variable "region" {
default="ap-south-1"
}

variable "tags" {
  type = list
  default = ["firstec2","secondec2"]
}

variable "ami" {
  type = map
  default = {
    "us-east-1" = "ami-0323c3dd2da7fb37d"
    "us-west-2" = "ami-0d6621c01e8c2de2c"
    "ap-south-1" = "ami-0470e33cd681b2476"
  }
}

```

```

root@ip-172-31-11-146:~# cat iam.tf 
provider "aws" {
region ="us-east-1"
}

resource "aws_iam_user" "lb" {
 count=4  
 name = var.users[count.index]

  tags = {
    env = "prod"
  }
}


variable users {
type=list
default=["jpmc1","jpmc2","jpmc3","jpmc4"]
}

```

```
WORKSPACE :

root@ip-172-31-11-146:~/work# cat work.tf 
provider "aws" {
  region     = "ap-south-1"

}


resource "aws_instance" "myec2" {
   ami = "ami-064ff912f78e3e561"
   instance_type = lookup(var.instance_type,terraform.workspace)
tags = {
    Name = lookup(var.name,terraform.workspace)
  }
}



variable "instance_type" {
  type = map

  default = {
    default = "t2.nano"
    dev     = "t2.micro"
    prod     = "t2.large"
  }
}

variable "name"{
type=map
default= {
default="IT server"
dev="dev-server"
prod="prod-server"
}
}

```


```

LOCAL MODULES :

root@ip-172-31-11-146:~/app# tree
.
├── modules
│   ├── ec2
│   │   ├── ec2.tf
│   │   └── variable.tf
│   └── s3
│       └── s3.tf
└── projects
    ├── projectA
    │   ├── dev
    │   │   ├── main.tf
    │   │   ├── terraform.tfstate
    │   │   └── terraform.tfstate.backup
    │   └── prod
    │       ├── main.tf
    │       ├── terraform.tfstate
    │       └── terraform.tfstate.backup
    └── projectB


```

```

root@ip-172-31-11-146:~/app# ls
modules  projects
root@ip-172-31-11-146:~/app# cd modules/
root@ip-172-31-11-146:~/app/modules# ls
ec2  s3
root@ip-172-31-11-146:~/app/modules# cd ec2/
root@ip-172-31-11-146:~/app/modules/ec2# ls
ec2.tf  variable.tf
root@ip-172-31-11-146:~/app/modules/ec2# cat ec2.tf 
resource "aws_instance" "ec2" {
instance_type= var.type
ami="ami-0d92749d46e71c34c"
tags = {
    Name = var.name
  }
}
root@ip-172-31-11-146:~/app/modules/ec2# cat variable.tf 
variable "type" {
default="t2.micro"
}

variable "name" {
default="dev-server"
}
```

```
root@ip-172-31-11-146:~/app/modules/s3# cat s3.tf 
resource "aws_s3_bucket" "example" {
  bucket = "my-tf-test-bucketttttttttttttttttttttttttttttttt"

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}
```


```

root@ip-172-31-11-146:~/app/projects/projectA/dev# cat main.tf 
provider "aws" {
region="ap-south-1"
}

module "ec2module" {
#source="../../modules/ec2"
source="/root/app/modules/ec2"
}

```


```
 root@ip-172-31-11-146:~/app/projects/projectA/prod# cat main.tf 
module "ec2module" {
#source="../../modules/ec2"
source="/root/app/modules/ec2"
type="t2.medium"
name="prod-server"
}
module "s3module" {
source="/root/app/modules/s3"
}

```


```
BACKEND AND STATE LOCKING :

root@ip-172-31-11-146:~/remote# cat backend.tf 
terraform {
  backend "s3" {
    bucket = "jpmc-statefille"
    key    = "terraform/state"
    region = "us-east-1"
    dynamodb_table = "tflock"
  }
}

root@ip-172-31-11-146:~/remote# cat ec2.tf 
provider "aws" {
region="us-east-1"
}

resource "aws_instance" "ec2" {
instance_type= "t2.medium"
ami="ami-0fa1ca9559f1892ec"
tags = {
    Name = "raman-server"
  }
}


** dynamodb_table = "tflock” 			//create a dynamodb table with LockID column –type String for State Locking


```

```
TF CLOUD REMOTE OPERATIONS :
--- terraform login : create an api token and authenticate...



root@ip-172-31-11-146:~/cloud# cat ec2.tf 
terraform {
  cloud {
    organization = "raman-tf"

    workspaces {
      name = "cli-workspace"
    }
  }
}

provider "aws" {
region="ap-south-1"
}

resource "aws_instance" "ec2" {
instance_type= "t2.medium"
ami="ami-0d92749d46e71c34c"
tags = {
    Name = "raman-server"
  }
}


```

terraform init
plan and apply from local to cloud..


```
VCS ---- TF CLOUD

```


