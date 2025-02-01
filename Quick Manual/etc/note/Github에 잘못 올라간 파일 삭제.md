- .gitignore 설정을 제대로 하지 못하여 Github에 올라가면 안 될 파일이 업로드 되었을 때 삭제 하는 방법

```bash

# 원격 저장소와 로컬 저장소에 있는 파일을 삭제한다. 주의 요망
$ git rm [File Name]   #<<<<<< 한번 더 생각해 볼 것

# 원격 저장소에 있는 파일을 삭제한다. 로컬 저장소에 있는 파일은 삭제하지 않는다.
$ git rm --cached [File Name]

# ex) src/main/resources/application.properties 삭제 시
$ git rm --cached src/main/resources/application.properties
```
