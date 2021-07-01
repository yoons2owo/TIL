# Ubuntu Java 설치

## 환경변수 설정

javac 위치 확인
```
which javac

readlink -f /usr/bin/javac
```
실행 결과가 /usr/lib/jvm/java-8-openjdk-amd64/bin 이라면 $JAVA_HOME은 /usr/lib/jvm/java-8-openjdk-amd64 로 설정한다. 


vi /etc/profile
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$JAVA_HOME/bin/:$PATH
export CLASS_PATH=$JAVA_HOME/lib:$CLASS_PATH
```
source /etc/profile

환경변수를 확인한다.
```
echo $JAVA_HOME
```