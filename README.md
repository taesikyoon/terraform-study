```
# 제 Github을 보고 테라폼을 연습하신다면 설치는 직접 해당 링크를 접속해서 하시면 됩니다.

https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
```

## 목차 [Table of Contents]

- [테라폼이란?](#테라폼이란-what-is-terraform)
- [Terraform Configuration](#테라폼의-구성-terraform-configuration)
- [Terraform Commands](#테라폼-명령어-terraform-commands)
- [Tutorial](#tutorial)

# 테라폼 공식문서를 활용한 공부 [Study Terraform Using docs]

# 테라폼이란? [What is Terraform]

💡 IaC (Infra as Code)
수동 프로세스가 아닌 코드를 통해 인프라를 관리하고 프로비저닝하는 것. 인프라 사양을 담은 구성 파일이 생성되어 구성 편집 및 배포가 보다 용이하다. 또한 매번 동일한 환경을 프로비저닝할 수 있도록 한다.

# 테라폼의 구성 [Terraform Configuration]

<details>
  <summary>클릭하여 내용 보기</summary>

## 1. 테라폼 설정 파일(\*.tf) [Terraform Configuration Files]

### terraform 블록

- terraform version
- provider version
- cloud
- backend
  테라폼의 구성을 명시하는 데 사용된다. 테라폼 버전이나 프로바이더 버전과 같은 값들은 자동으로 설정되지만 다른 사람과 함께 작업할 때는 버전을 명시적으로 선언하고 필요한 조건을 입력하여 실행 오류를 최소화할 것을 권장하고 있다. 또한 협업을 위한 관점으로 확장할 경우 다른 사람이 실행하는 경우에 대비해 테라폼의 구성 정보를 명확하게 정의해야 오류를 방지해야한다.

**버전 표기**  
버전 체계는 시맨틱 버전 관리 방식을 따르고 테라폼 내에서 버전이 명시되는 terraform, module에서만 사용 가능하며 버전을 제약함으로 항상 의도한 대로 실행하는 것을 목적으로 한다.

**시멘틱 버전**  
Ex) 1.3.4 (Major.Minor.Patch)

- Major 버전: 내부 동작의 API가 변경 또는 삭제되거나 하위 호환이 되지 않는 버전
- Minor 버전: 신규 기능이 추가되거나 개선되고 하위 호환이 가능한 버전
- Patch 버전: 버그 및 일부 기능이 개선된 하위 호환이 가능한 버전

**버전 제약 구문**

- = 또는 연산자 없음: 지정된 버전만을 허용하고 다른 조건과 병기할 수 없다.
- !=: 지정된 버전을 제외한다.
- > ,>=,<,<=: 지정한 버전과 비교해 조건에 맞는 경우 허용한다.
- ~>: 지정한 버전에서 가장 자리수가 낮은 구성요소만 증가하는 것을 허용한다.~> X•y인 경우 서만,~>x•y•2인 경우 2 버전에 대해서만 보다 큰 버전을 허용한다

### resource 블록

### data 블록

### variable 블록

### local 블록

### output 블록

</details>

# 테라폼 명령어 [Terraform Commands]

<details>
  <summary>클릭하여 내용 보기</summary>

Terraform은 인프라스트럭처를 코드로 관리하는 도구입니다. 다음은 Terraform을 사용할 때 기본적으로 자주 사용되는 주요 명령어들입니다:

## `terraform init`

**기본 사용법: terraform [global options] init [options]**

이 작업을 실행하는 디렉터리를 루트 모듈이라 부른다. 테라폼을 시작하는 데 사용되는 첫 번 째 명령어로 테라폼에서 사용되는 프로바이더, 모듈 등의 지정된 버전에 맞춰 루트 모듈을 구성하는 역할을 수행한다.

자동화 구성을 위한 파이프라인 설계 시 테라폼을 실행하는 시점에 필수적으로 요청되는 명령어이기도 하다.

자바의 pom.xmL, Node.js의 package.json, 파이썬 의 requirements. txt처럼 구성에서 필요한 의존성 정의를 읽고, 최초 실행 시 실행에 필요한 아티팩트나 라이브러리를 다운로드하고 준비시키는 역할과 비슷하다.

## `terraform plan`

이 명령은 설정된 Terraform 코드를 기반으로 실행 계획을 생성합니다. 이 계획은 실제 리소스에 적용되기 전에 무엇이 변경될지 미리 보여줍니다.

테라폼으로 적용할 인프라의 변경 사항에 관한 실행 계획을 생성하는 동작이다. 또한 출력되는 결과를 확인하여 어떤 변경이 적용될지 사용자가 미리 검토하고 이해 하는 데 도움

**기본 사용법: terraform [global options] plan [options]**

**-detailed-exitcode**

실행 계획 생성 명령과 함께 사용하기에 좋은 추가 옵션으로, 파이프라인 설계에서 활용할 수 있는 -detailed-exitcode를 추가해 실행하면 옵션이 없던 때와 결과는 같지만 exitcode가 환경 변수로 구성된다.

```
# 명령어 실행
terraform paln detailed-exitcode
...
echo %errorlevel%
2 << 출력값
```

- 0: 변경 사항이 없는 성공
- 1 : 오류가 있음
- 2: 변경 사항이 있는 성공

## `terraform apply`

**기본 사용법: terraform [global options] apply [options] [PLAN]**

이 명령은 terraform plan에서 생성된 실행 계획을 실제 인프라에 적용합니다. 이 과정에서 실제 리소스가 생성, 변경, 삭제됩니다.

apply 명령은 plan에서 작성된 적용 내용을 토대로 작업을 실행한다. terraform plan 명령 으로 생성되는 실행 계획이 필요하지만, 만약 없다면 새 실행 계획을 자동으로 생성하고 해당 계획을 승인할 것인지 묻는 메시지가 표시된다

-auto-approve

## `terraform destroy`

이 명령은 Terraform을 통해 생성된 모든 리소스를 제거합니다. 이 명령은 인프라를 철거할 때 사용됩니다.

**기본 사용법: terraform [global options] destroy [options]**

terraform destroy 명령은 테라폼 구성에서 관리하는 모든 개체를 제거하는 명령어다. 테라 폼 코드로 구성된 리소스의 일부만 제거하기 위해서는 테라폼의 선언적 특성에 따라 삭제하려

## `terraform validate`

**기본 사용법: terraform [global options] validate [options]**

커맨드 단어 의미대로 디렉터리에 있는 테라폼 구성 파일의 유효성을 확인한다.  
이때 대상이 되는 인프라와 서비스의 상태를 확인하기 위한 원격 작업이나 API 작업은 발생하지 않고, 코드 적인 유효성만 검토한다.  
API 작업이 발생하는 테라폼 Plan 동작과 달리 작성된 구성의 문법, 종속성, 속성 이름이나 연결된 값의 정확성 확인을 수행한다.

## `terraform fmt`

이 명령은 Terraform 구성 파일을 표준 형식에 맞게 자동으로 정렬합니다. 코드의 가독성을 높이고 일관성을 유지하는 데 도움을 줍니다.

**기본 사용법: terraform fmt [options] [DIR]**

format 또는 reformat의 줄임 표시로 terraform fmt 명령어로 커맨드를 수행한다. fmt 명령 어는 테라폼 구성 파일을 표준 형식과 표준 스타일로 적용하는 데 사용한다. 주로 구성 파일에 작성된 테라폼 코드의 가독성을 높이는 작업에 사용되는데, 이를테면 코드 협업 과정에서 각 작업자별로 코드 작성에 쓰인 정렬, 빈칸, 내려쓰기 등의 규칙이 다른 경우에 유용하다.

## `terraform taint`

특정 Terraform 관리 리소스를 '손상된' 상태로 표시합니다. 다음 apply 실행 시 Terraform은 이 리소스를 강제로 재생성합니다.

## `terraform untaint`

terraform taint로 손상된 리소스의 손상 표시를 제거합니다.

## `terraform workspace`

여러 환경을 동일한 구성으로 관리할 수 있도록 워크스페이스를 제공합니다. 이 명령은 워크스페이스를 생성, 변경, 목록 보기 등을 수행할 수 있습니다.

## `terraform workspace list`

이 명령어들은 Terraform을 사용하여 인프라를 효율적으로 관리하는 데 필수적인 도구입니다.

</details>

## Tutorial

[- Tutorial README 이동하기](tutorial/README.md)
