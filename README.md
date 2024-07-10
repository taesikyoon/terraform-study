```
# 제 Github을 보고 테라폼을 연습하신다면 설치는 직접 해당 링크를 접속해서 하시면 됩니다.

https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
```

## 목차 [Table of Contents]

- [테라폼이란?](#테라폼이란)
- [Terraform Configuration](#terraform-configuration)
- [Terraform Commands](#terraform-commands)
- [Create EC2](#create-eC2)

# 테라폼 공식문서를 활용한 공부 [Study Terraform Using docs]

## 테라폼이란? [What is Terraform]

💡 IaC (Infra as Code)
수동 프로세스가 아닌 코드를 통해 인프라를 관리하고 프로비저닝하는 것. 인프라 사양을 담은 구성 파일이 생성되어 구성 편집 및 배포가 보다 용이하다. 또한 매번 동일한 환경을 프로비저닝할 수 있도록 한다.

# 테라폼의 구성 [Terraform Configuration]

<details>
  <summary>클릭하여 내용 보기</summary>

## 1. 테라폼 설정 파일(\*.tf) [Terraform Configuration Files]

테라폼은 resource, data, output, variable의 블럭들로 파일이 구성된다.

### Resource

### Data

### Output

### variable

</details>

# Terraform Commands

<details>
  <summary>클릭하여 내용 보기</summary>

Terraform은 인프라스트럭처를 코드로 관리하는 도구입니다. 다음은 Terraform을 사용할 때 기본적으로 자주 사용되는 주요 명령어들입니다:

## `terraform init`

이 명령은 Terraform 프로젝트를 초기화합니다. 필요한 Terraform 프로바이더 플러그인을 설치하고, 기타 필요한 구성 파일을 준비합니다.

## `terraform plan`

이 명령은 설정된 Terraform 코드를 기반으로 실행 계획을 생성합니다. 이 계획은 실제 리소스에 적용되기 전에 무엇이 변경될지 미리 보여줍니다.

## `terraform apply`

이 명령은 terraform plan에서 생성된 실행 계획을 실제 인프라에 적용합니다. 이 과정에서 실제 리소스가 생성, 변경, 삭제됩니다.

## `terraform destroy`

이 명령은 Terraform을 통해 생성된 모든 리소스를 제거합니다. 이 명령은 인프라를 철거할 때 사용됩니다.

## `terraform validate`

이 명령은 Terraform 구성 파일이 유효한지 검사합니다. 구성 오류를 사전에 찾아내는 데 유용합니다.

## `terraform fmt`

이 명령은 Terraform 구성 파일을 표준 형식에 맞게 자동으로 정렬합니다. 코드의 가독성을 높이고 일관성을 유지하는 데 도움을 줍니다.

## `terraform taint`

특정 Terraform 관리 리소스를 '손상된' 상태로 표시합니다. 다음 apply 실행 시 Terraform은 이 리소스를 강제로 재생성합니다.

## `terraform untaint`

terraform taint로 손상된 리소스의 손상 표시를 제거합니다.

## `terraform workspace`

여러 환경을 동일한 구성으로 관리할 수 있도록 워크스페이스를 제공합니다. 이 명령은 워크스페이스를 생성, 변경, 목록 보기 등을 수행할 수 있습니다.

## `terraform workspace list`

이 명령어들은 Terraform을 사용하여 인프라를 효율적으로 관리하는 데 필수적인 도구입니다.

</details>

## Create EC2

[- EC2 생성하기 README 이동하기](create-ec2/README.md)  
[- terraform dock 이동하기 ](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build)

```

```
