# Trouble Shooting 

Git Trouble Shooting 

## src refspec master does not match any

### Symptom
```
error: src refspec master does not match any
error: failed to push some refs to 'github.com-yoon:yoons2owo/TIL.git'
```

pull 해도 Already up to date 상태

### Cause
github에 있는 파일과 현재 push 하려는 commit이 일치하지 않아 발생

### Resolution
에러를 무시하고 강제로 push
```
git push -f origin
```
파일 손실의 위험이 있으므로 주의

