# 터미널 조작 로그

[← README로 돌아가기](../README.md)

실습 폴더: `~/terminal-practice`

![폴더 이동, 현재 위치 확인, 빈 파일 생성, 목록 확인](images/terminal-cd-touch.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~$ cd terminal-practice
hunyhan@HJH:~/terminal-practice$ pwd
/home/hunyhan/terminal-practice
hunyhan@HJH:~/terminal-practice$ touch memo.txt
hunyhan@HJH:~/terminal-practice$ ls
memo.txt
hunyhan@HJH:~/terminal-practice$
```

</details>

![파일 내용 확인과 덮어쓰기](images/terminal-echo-cat.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ cat memo.txt
hunyhan@HJH:~/terminal-practice$ echo "hello" > memo.txt
hunyhan@HJH:~/terminal-practice$ cat memo.txt
hello
hunyhan@HJH:~/terminal-practice$ echo "secend"> memo.txt
hunyhan@HJH:~/terminal-practice$ cat memo.txt
secend
```

</details>

![이어 붙이기, 복사, 원본 유지 확인](images/terminal-append-cp.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ echo "third" >> memo.txt
hunyhan@HJH:~/terminal-practice$ cat memo.txt
secend
third
hunyhan@HJH:~/terminal-practice$ cp memo.txt memo-copy.txt
hunyhan@HJH:~/terminal-practice$ ls
memo-copy.txt  memo.txt
hunyhan@HJH:~/terminal-practice$ cat memo-copy.txt
secend
third
hunyhan@HJH:~/terminal-practice$ echo "changed" > memo-copy.txt
hunyhan@HJH:~/terminal-practice$ cat memo-copy.txt
changed
hunyhan@HJH:~/terminal-practice$ cat memo.txt
secend
third
```

</details>

![이름 변경, 숨김 파일 확인, 폴더 생성](images/terminal-mv.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ ls
memo-copy.txt  memo.txt
hunyhan@HJH:~/terminal-practice$ mv memo-copy.txt .memo-copy.txt
hunyhan@HJH:~/terminal-practice$ ls
memo.txt
hunyhan@HJH:~/terminal-practice$ ls -a
.  ..  .memo-copy.txt  memo.txt
hunyhan@HJH:~/terminal-practice$ ls
memo.txt
hunyhan@HJH:~/terminal-practice$ mkdir backup
hunyhan@HJH:~/terminal-practice$ ls
backup  memo.txt
hunyhan@HJH:~/terminal-practice$ mv memo.txt backup/
hunyhan@HJH:~/terminal-practice$ ls
backup
hunyhan@HJH:~/terminal-practice$ ls backup/
memo.txt
hunyhan@HJH:~/terminal-practice$ ls -a
.  ..  .memo-copy.txt  backup
```

</details>

![삭제와 폴더 삭제](images/terminal-rm.png)

<details>
<summary>화면 원문</summary>

```text
hunyhan@HJH:~/terminal-practice$ pwd
/home/hunyhan/terminal-practice
hunyhan@HJH:~/terminal-practice$ ls -a
.  ..  .memo-copy.txt  backup
hunyhan@HJH:~/terminal-practice$ rm .memo-copy.txt
hunyhan@HJH:~/terminal-practice$ ls -a
.  ..  backup
hunyhan@HJH:~/terminal-practice$ rm backup/
rm: cannot remove 'backup/': Is a directory
hunyhan@HJH:~/terminal-practice$ ls
backup
hunyhan@HJH:~/terminal-practice$ rm backup
rm: cannot remove 'backup': Is a directory
hunyhan@HJH:~/terminal-practice$ rma -r backup/
Command 'rma' not found, but there are 17 similar ones.
hunyhan@HJH:~/terminal-practice$ ls
backup
hunyhan@HJH:~/terminal-practice$ rm -r backup/
hunyhan@HJH:~/terminal-practice$ ls
hunyhan@HJH:~/terminal-practice$ ls -a
.  ..
```

</details>
