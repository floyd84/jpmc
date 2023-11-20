https://forms.office.com/r/wNEtQYeakB


# jpmc


```
23RIC3469_U01 : shubhu

23RIC3469_U02 : arin


23RIC3469_U03 : ravi

4

23RIC3469_U04 : floyd

5

23RIC3469_U05 : jojin

6

23RIC3469_U06 : karthik

7

23RIC3469_U07 : simi

8

23RIC3469_U08 : nirmal

9

23RIC3469_U09 : govind

10

23RIC3469_U10 : omkar

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
