# Github 여러 계정 사용하기

## Process

### SSH key-gen 생성

* 개인 계정: yoons2owo
```bash
$ ssh-keygen -t rsa -b 4096 -C "yoons2owo@gmail.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/${userPath}/id_rsa): id_rsa_yoon
```

* 회사 계정: kekwon
```bash
$ ssh-keygen -t rsa -b 4096 -C "kekwon@gmail.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/${userPath}/id_rsa): id_rsa_kekwon
```

### Github에 SSH key 등록
```
$ ssh-add id_rsa_yoon
```
```
$ ssh-add id_rsa_kekwon
```

Github > Settings > SSH and GPG keys > New SSH Key 

.pub 내용 붙여넣기(id_rsa_yoon.pub)

### config 적용
```
$ vi ~/.ssh/config
```
```
# account yoon
Host github.com-yoon
HostName github.com
User git

# account kekwon
Host github.com-kekwon
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_kekwon
```

### 연결 테스트
```
$ ssh -T github.com-yoon
Hi yoons2owo! You've successfully authenticated, but GitHub does not provide shell access.

$ssh -T github.com-kekwon
Hi kekwon! You've successfully authenticated, but GitHub does not provide shell access.
```

### 계정 변경하여 사용하기
```
$ git config user.name "yoons2owo"
$ git config user.email "yoons2owo@gmail.com"
```

### Git Clone or Remote
SSH 주소 이용
```
git clone git@github.com-yoon:yoons2owo/TIL.git
```
or 
```
git remote add origin git@github.com-yoon:yoons2owo/TIL.git
```


