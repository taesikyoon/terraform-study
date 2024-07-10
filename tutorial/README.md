```
** 너무나도 당연하지만 [AWS CLI, Terraform CLI, AWS 자격증명] 설치 및 사전 작업이 완료되어야함
```

# EC2 인스턴스 생성해보기

\*\* terraform init으로 해당 작업 폴더 초기화

### 1. 간단한 인스턴스 생성

```
# main.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}
```

- terraform fmt 포맷팅
- terraform validate
- terraform plan으로 실행 계획 확인
- terraform apply 실행, yes를 입력해 요구사항 실행하도록 해야함

### 2. AMI 이미지 변경해보기

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-08d70e59c07c61a3a"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}

```

- fmt, validate, plan ... 해보기
- AMI를 수정하는건 새로운 인스턴스를 만들어야한다고 판단해서 인스턴스를 삭제하고 새로 만들겠다는 부분을 잘 확인해보기!
