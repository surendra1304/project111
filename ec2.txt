
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "eu-west-1"
}


module "ec2_instance" {
  source  = "terraform-aws-modules/ec2-instance/aws"

  name = "single-instance"

  instance_type          = "t2.micro"
  key_name               = "key11"
  monitoring             = true
  vpc_security_group_ids = ["sg-009f20ca4d90ba4bd"]
  subnet_id              = "subnet-051c481a09e876207"

  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}
