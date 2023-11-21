# jpmc


``` bnglore :
23RIC3469_U01 : shubhu : p , p

23RIC3469_U02 : arin , p , p


23RIC3469_U03 : ravi : p , p

4

23RIC3469_U04 : floyd : p , p

5

23RIC3469_U05 : jojin : p , p

6

23RIC3469_U06 : karthik : p , p

7

23RIC3469_U07 : simi : p, p


vaibhav : np , p



hyderbd :

8

23RIC3469_U08 : nirmal : p , p

9

23RIC3469_U09 : govind p , p

10

23RIC3469_U10 : omkar p, p


```

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
