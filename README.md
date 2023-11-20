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
