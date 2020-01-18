## 안녕하세요. 


Git pull/push 시 Password 물어보지 않도록 설정하기(credential.helper)
on August 23, 2018  in Coding, Git 
git을 쓰다보면 간혹 config 미스, 환경 변경으로 push/pull 등 기능 실행 시 계정과 패스워드를 물어보는 경우가 발생합니다.

credential 설정이 되어있지 않다면 계정정보를 요청하는게 당연하지만 한창 개발하고 있는 과정에서는 굉장히 귀찮고 번거로워집니다.
(특히나 제 툴들은 대다수가 git pull로 업데이트를 수행하기 떄문에...더더욱..)

여러가지 방법이 있겠지만 아래 2가지 방법이 개인적으로 맘에들어 사용합니다.

1. Credential 정보 저장
```bash
#> git config credential.helper store
```

credential.helper의 store 옵션을 주게되면 해당 git directory에선 반영구적으로 인증 절차가 생략됩니다.(저장된 credential 정보를 이용해 인증 처리)

2. 캐시 저장

```bash
#> git config credential.helper cache
```

임시로 일정 시간동안 저장하기에는 cache 가 더욱 유용합니다. cache 옵션을 주게되면 기본적으로 15분 동안 인증 절차를 요구하지 않습니다.
시간은 timeout 옵션으로 지정해줄 수 있습니다. (초 단위이며 아래와 같이 지정 시 3600초, 즉 1시간의 유효시간을 가집니다)

```bash
#> git config credential.helper 'cache --timeout=3600'
```

모드 프로젝트에 적용
git config의 공통적인 설정과 같이 --global 옵션을 주게되면 해당 git directory 이외에 모든 git 활동에서 저장된 정보를 이용하게 됩니다.

```bash
#> git config credential.helper store --global
```
