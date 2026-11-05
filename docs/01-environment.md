# 실행 환경

[← README로 돌아가기](../README.md)

| 항목 | 값 | 실행한 곳 |
|------|------|------|
| OS | Windows 11, WSL2 `Ubuntu 24.04.5 LTS` | Ubuntu |
| 쉘 | `/bin/bash`, Git Bash | Ubuntu, Windows |
| 터미널 | Windows Terminal, VSCode 통합 터미널 | |
| Docker | `29.8.0, build 88096ef` | Ubuntu |
| Docker 엔진 | Docker Desktop | Ubuntu |
| Git | `2.43.0` | Ubuntu |
| Git | `2.54.0.windows.1` | Git Bash |

## 명령과 출력

```text
hunyhan@HJH:~$ lsb_release -d
No LSB modules are available.
Description:    Ubuntu 24.04.5 LTS
hunyhan@HJH:~$ echo $SHELL
/bin/bash
hunyhan@HJH:~$ docker --version
Docker version 29.8.0, build 88096ef
hunyhan@HJH:~$ git --version
git version 2.43.0
hunyhan@HJH:~$ docker info --format '{{.ServerVersion}} / {{.OperatingSystem}} / {{.Name}}'
29.8.0 / Docker Desktop / docker-desktop
```

```text
hyjyj@HJH MINGW64 ~/codyssey_1week (main)
$ git --version
git version 2.54.0.windows.1
```

프롬프트의 폴더는 읽기 쉽게 `~`로 줄였습니다. 명령과 출력은 실제 실행 결과입니다.
