# 권한 실습

[← README로 돌아가기](../README.md)

| 대상 | 변경 | 결과 |
|------|------|------|
| 파일 `a.txt` | `644` → `664` → `644` | 그룹 쓰기 권한 추가 후 복구 |
| 폴더 `test` | `755` → `655` → `755` | 주인의 `x`를 빼면 `cd`가 거절됨 |

`644`는 주인만 파일을 고칠 수 있고 나머지는 읽기만 하는 값입니다. `755`는 폴더에 들어가고 목록을 볼 수 있게 하되, 안의 파일을 만들고 지우는 것은 주인만 할 수 있는 값입니다.

![파일과 폴더의 기본 권한](images/perm-ls-l.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ touch a.txt
hunyhan@HJH:~/terminal-practice$ touch b.txt
hunyhan@HJH:~/terminal-practice$ ls
a.txt  b.txt
hunyhan@HJH:~/terminal-practice$ ls -l
total 0
-rw-r--r-- 1 hunyhan hunyhan 0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan 0 Oct 29 23:09 b.txt
hunyhan@HJH:~/terminal-practice$ mkdir test
hunyhan@HJH:~/terminal-practice$ ls
a.txt  b.txt  test
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
```

</details>

![chmod g+w, chmod u-x, chmod u+x 변경 전후](images/perm-chmod.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ chmod g+w a.txt
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ chmode u-x test/
Command 'chmode' not found, did you mean:
  command 'chmod' from deb coreutils (9.4-3ubuntu6.2)
Try: sudo apt install <deb name>
hunyhan@HJH:~/terminal-practice$ chmod u-x test/
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drw-r-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ chmod u+x test/
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
```

</details>

![폴더의 x 권한을 뺀 뒤 cd가 거절되고 복구 후 성공](images/perm-cd-denied.png)

<details>
<summary>화면 원문</summary>

```text
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ chmod u-x test/
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drw-r-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ cd test/
-bash: cd: test/: Permission denied
hunyhan@HJH:~/terminal-practice$ chmod u+x test/
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ cd test/
hunyhan@HJH:~/terminal-practice/test$ cd ..
hunyhan@HJH:~/terminal-practice$ cd test/
hunyhan@HJH:~/terminal-practice/test$ pwd
/home/hunyhan/terminal-practice/test
```

</details>

![숫자 표기로 664에서 644로 변경](images/perm-chmod-644.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ chmod 664 a.txt
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-rw-r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
hunyhan@HJH:~/terminal-practice$ chmod 644 a.txt
hunyhan@HJH:~/terminal-practice$ ls -l
total 4
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 a.txt
-rw-r--r-- 1 hunyhan hunyhan    0 Oct 29 23:09 b.txt
drwxr-xr-x 2 hunyhan hunyhan 4096 Oct 29 23:09 test
```

</details>
