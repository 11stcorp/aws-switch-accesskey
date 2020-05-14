# aws-switch-accesskey
Script for managing multiple aws account

~~awscli 는 AWS_PROFILE 환경변수를 통해 multi accesskey 를 관리할수 있도록 지원하고 있지만,~~

fzf 기능을 활용하여 switch 하기 위해 따로 제작한 스크립트 입니다.

## Usage

clone 해서 받은 a 는 bash script 입니다.

* a 파일을 적절한 위치에 옮겨놓고 바로 사용할 수 있도록 설정합니다.

  ```bash
  chmod +x a
  mv a ~/.aws
  vi ~/.zshrc
  ```

  ```bash
  alias a="~/.aws/a"
  ```

  ```bash
  source ~/.zshrc
  ```

  > /usr/local/bin 위치에 a 를 배치하는것도 하나의 방법입니다.

* 사용할 account 를 설정합니다.

  * IAM 을 통해 받은 ACCESS_KEY 는 ${HOME}/.aws/accouts/list.json 에서 설정합니다.

    ```bash
    mkdir -p ${HOME}/.aws/accouts
    vi ${HOME}/.aws/accouts/list.json
    ```

    ```json
    {
      "jj1": {
        "REGION": "ap-northeast-2",
        "OUTPUT": "json",
        "ACCESS_KEY": "AKIA*****",
        "SECRET_KEY": "f+-----++++++++++++++++"
      },
      "jj2": {
        "ACCESS_KEY": "AKIA*****",
        "SECRET_KEY": "f+-----++++++++++++++++"
      },
      "jj3": {
        "ACCESS_KEY": "AKIA*****",
        "SECRET_KEY": "f+-----++++++++++++++++"
      }
    }
    ```
    
  * SSO 를 통해 CLI 를 사용하고 싶다면 ${HOME}/.aws/accouts/sso-list.json 에서 설정합니다.

    ```bash
    mkdir -p ${HOME}/.aws/accouts
    vi ${HOME}/.aws/accouts/sso-list.json
    ```

    ```json
    {
      "jj-sso": {
        "SSO_URL": "https://sssssooooooo.awsapps.com/start",
        "SSO_REGION": "ap-southeast-1"
      }
    }
    ```


* 사용해봅시다.

  ```bash
  $ a
    5/5
    Select AWS account
  > your-account1
    jj1
    jj2
    jj3
  ```

  ```bash
  $ a sso
  >
    1/1
    Select AWS account
  > jj-sso
  SSO start URL [https://sssssooooooo.awsapps.com/start]:
  SSO Region [ap-southeast-1]:
  There are N AWS accounts available to you.
  Using the account ID 00000000000
  There are 2 roles available to you.
  Using the role name "AdministratorAccess"
  CLI default client Region [ap-northeast-2]:
  CLI default output format [json]:
  CLI profile name [AdministratorAccess-00000000000]: default

  ```
  > profile name 을 `default` 로 하면 --profile 을 지정하지 않아도 되어 편합니다.

