# Linux

**1. Linux 파일 관련 명령어**

들어가야 할 내용

```
chown
chgrp
chmod
ls의 옵션들
find
grep
umask
```

- Question : 다음은 ls -al 명령어를 쳤을 때의 결과이다. drwxr-xr-x와 -rw-r--r--이 의미하는 바는 무엇일까요? 그리고 이 권한을 어떻게 바꿀까요? 숫자로 권한을 설정한다면 어떻게 설정할 수 있을까요?

```
$ ls -al
total 52
drwxr-xr-x 1 rwk 197121     0 12월  4 19:43 ./
drwxr-xr-x 1 rwk 197121     0 12월  2 00:02 ../
-rw-r--r-- 1 rwk 197121  7547 12월  4 20:37 리눅스운영및관리.md
-rw-r--r-- 1 rwk 197121 41209 12월  4 19:44 리눅스일반.md   
```

**2. bash shell script 문법**

들어가야 하는 내용

```
쉘 변수 (환경 변수, 매개 변수, 예약 변수)
쉘 산술 연산
쉘 조건문
쉘 반복문
쉘 배열문
```