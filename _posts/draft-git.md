## SourceTree 설치
- .NET 설치 필요
- Bitbucket 선택 (atlassian 로그인 필요)

## Remote branch 확인
```
git branch -r (전체 branch 보려면 -a)
git ls-remote --heads <remote-name>
git remote show <remote-name>
```

## Remote branch 정보 동기화
```
git remote update <remote-name> --prune
```

## Remote branch로 부터 Checkout
```
git checkout -b test <name of remote>/test
git checkout -t <name of remote>/test
```
