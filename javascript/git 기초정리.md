## git 초기 세팅

### git 설치 확인

```javascipt
git --version
```

### git 초기 설정

```javascript
git config --global user.name "abc"
git config --global user.email abc@gmail.com
```
프로젝트별로 사용자를 다르게 설정할 예정이라면 --global 을 빼고 설정하면 됨

```javascript
git config user.name "abc"
git config user.email abc@gmail.com
```

### git 설정 확인하기

```javascript
git config --list
```

### 설정된 계정 삭제하기

```javascript
//global
git config --unset user.name
git config --unser user.email

//local
git config --unset --global user.name
git config --unset --global user.email
```

### 저장소 생성하기
git init 명령어를 실행하면, 현재 디렉토리를 기준으로 Git 저장소가 생성됩니다.

```javascript
git init
```

### 상태 확인하기
```javascript
git status
```

### Staging 영역에 추가
```javascript
git add . //현재 디렉토리에 있는 업데이트 된 파일을 전부 스테이징 영역으로 추가
git add -A //수정된 파일 전부를 스테이징 영역에 추가
```

### Repository에 commit하기
```javascript
$ git commit -m "메시지"
-m 은 메세지의 약자이고, 뒤에 ""안에 공유할 메시지 내용을 적어주시면 됩니다.
```

### 원격 저장소에 push, 업데이트 된 내용은 pull하기
내 local 디렉토리로 부터 원격저장소(Remote repository)로 보내기 위해서는 push 명령어를 사용합니다.

```javascript
$ git branch -M main //브랜치 이름을 main으로 바꿀때
$ git remote add origin (원격 저장소 github URL) //origin은 remote repository의 이름이며, 다른 이름으로 설정해도 무방합니다.
$ git push origin "branch명"
$ git pull origin "branch명"
```





