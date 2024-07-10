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

Point

1. 첫 사용에는 fmt, validate, plan을 사용하여 무엇을 위해 사용되는 명령어인지 익히기
2. apply를 통한 tf파일 실행하기

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

Point

1. AMI 인스턴스 업데이트하며, 진행되는 과정에 예상했던 부분과 실제 실행되는 부분 비교해보기

해당 AMI 인스턴스를 변경해야하는 상황에선 같은 인스턴스가 되지 않으니 삭제하고 새로운 인스턴스를 실행시킴

### 3. variables 블럭 사용

- main.tf

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
  profile = "study"
}

resource "aws_instance" "app_server" {
  ami           = "ami-08d70e59c07c61a3a"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}

```

- variables.tf

```

variable "instance_name" {
  description = "Value of the Name tag for the EC2 instance"
  type        = string
  default     = "ExampleAppServerInstance"
}
```

Point

1. terraform apply -var "instance_name=YetAnotherName으로 유연하게 이름을 생성 가능함

**변수가 활성화될 경우:**  
유연성 증가: instance_name 변수를 사용하면 EC2 인스턴스의 Name 태그 값을 구성 파일의 다른 부분에서 중복 없이 쉽게 재사용하거나 수정이 가능함 예를 들어, 다른 리소스 또는 여러 인스턴스에서 같은 이름을 사용하려 할 때 유용해짐

사용자 입력 허용: 변수를 사용하면 Terraform 실행 시 사용자로부터 입력을 받거나, 다른 방법으로 변수 값을 동적으로 설정할 수 있음, 이는 특히 다른 환경(개발, 테스트, 프로덕션 등)에 따라 다른 이름을 사용하고자 할 때 유용함

**오류 감소:**  
변수를 사용하지 않을 때, 잘못된 입력이나 외부에서 변수 값을 설정하는 복잡성이 감소하여, 구성의 오류 발생 가능성이 낮아짐
