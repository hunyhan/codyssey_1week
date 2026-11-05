# 개발 워크스테이션 구축

nginx로 커스텀 이미지를 만들어, 내가 나중에 궁금하면 찾아볼 수 있는 설명서를 만들었다. 이 과정에서 터미널, 권한, Docker, Git을 직접 설정하고 실행 결과로 확인했다.

저장소: <https://github.com/hunyhan/codyssey_1week>

## 1. 실행 환경

| 항목 | 값 |
|------|------|
| OS | Windows 11, WSL2 `Ubuntu 24.04.5 LTS` |
| 쉘 | `/bin/bash`, Git Bash |
| 터미널 | Windows Terminal, VSCode 통합 터미널 |
| Docker | `29.8.0, build 88096ef` (Docker Desktop) |
| Git | Ubuntu `2.43.0`, Git Bash `2.54.0.windows.1` |

[명령과 출력 보기](docs/01-environment.md)

## 2. 수행 체크리스트와 증거

각 항목의 링크에서 화면과 글자 원문을 함께 볼 수 있습니다.

| 완료 | 수행 항목 | 검증 방법 | 증거 |
|------|------|------|------|
| ✅ | 터미널 기본 조작 | 위치, 숨김 파일, 이동, 생성, 복사, 이름 변경, 삭제, 내용 확인 | [터미널 로그](docs/02-terminal.md) |
| ✅ | 파일·폴더 권한 변경 | `chmod` 전후 `ls -l` 비교 | [권한 실습](docs/03-permissions.md) |
| ✅ | Docker 설치·점검 | `docker --version`, `docker info` | [실행 환경](docs/01-environment.md) |
| ✅ | Docker 운영 명령 | `images`, `ps -a`, `logs`, `stats` | [운영 로그](docs/04-docker-ops.md) |
| ✅ | 컨테이너 실행 | `hello-world`, `ubuntu` 진입, attach와 exec 비교 | [컨테이너 실습](docs/04-docker-ops.md#컨테이너-실행) |
| ✅ | 커스텀 이미지 | `docker build`, 실행, 웹 응답 | [이미지 제작](docs/05-custom-image.md) · [Dockerfile](my-nginx/Dockerfile) · [웹 소스](my-nginx/site/index.html) |
| ✅ | 포트 매핑 | `-p 8083:80`, 주소창 포함 브라우저 화면 | [포트 매핑](docs/06-port-mapping.md) |
| ✅ | 바인드 마운트 | 호스트 파일 변경 전후 비교 | [바인드 마운트](docs/07-bind-mount.md) |
| ✅ | 볼륨 영속성 | 컨테이너 삭제 전후 데이터 비교 | [볼륨](docs/08-volume.md) |
| ✅ | Git 설정 | 사용자 정보, 기본 브랜치, `git config --list` | [Git 설정](docs/09-git-github.md#git-설정) |
| ✅ | GitHub·VSCode 연동 | SSH 연결, VSCode 로그인, 소스 제어 | [연동 증거](docs/09-git-github.md#ssh-키-연결) |
| ✅ | 보너스: SSH 푸시 | SSH 주소로 `git push` | [커밋과 푸시](docs/09-git-github.md#커밋과-ssh-푸시) |
| ✅ | 트러블슈팅 | 문제 → 가설 → 확인 → 해결 6건 | [트러블슈팅](docs/10-troubleshooting.md) |

## 3. 파일 구성

```text
.
├─ README.md
├─ my-nginx/
│  ├─ Dockerfile
│  └─ site/            웹 서버 콘텐츠 (설명서, 용어집)
└─ docs/
   ├─ 01~10 *.md       주제별 증거
   └─ images/          증거 화면
```

## 4. 실행 방법

```bash
git clone https://github.com/hunyhan/codyssey_1week.git
cd codyssey_1week/my-nginx
docker build -t my-nginx:v3 .
docker run -d --name my-nginx-v3 -p 8083:80 my-nginx:v3
curl -I http://localhost:8083
```

브라우저에서 <http://localhost:8083>을 열면 설명서가 나옵니다.

### 주의사항

- 8083번을 이미 쓰고 있다면 `-p 다른번호:80`으로 바꿔 실행합니다.
- 바인드 마운트 명령의 `/home/hunyhan/...`은 내 PC의 경로입니다. 자기 폴더의 절대 경로로 바꿉니다.
- 이 저장소의 `user.email`은 이 폴더에만 적용되는 local 설정입니다.

## 5. 트러블슈팅 요약

| 문제 | 원인 | 해결 |
|------|------|------|
| [`docker`를 못 찾음](docs/10-troubleshooting.md#1-새-ubuntu에서-docker를-못-찾음) | WSL integration이 꺼져 있음 | Docker Desktop 설정에서 켜기 |
| [소켓 `permission denied`](docs/10-troubleshooting.md#2-docker-info에서-소켓-permission-denied) | 그룹이 반영되기 전의 터미널 | Ubuntu 다시 접속 |
| [`>`만 나옴](docs/10-troubleshooting.md#3-터미널이-만-보여-주고-명령이-안-먹힘) | 따옴표를 닫지 않음 | `Ctrl+C` |
| [`ssh -T` 멈춤](docs/10-troubleshooting.md#4-ssh--t가-아무-출력-없이-멈춤) | 주소 자리에 이메일 입력 | `git@github.com`으로 실행 |
| [`not a git repository`](docs/10-troubleshooting.md#5-fatal-not-a-git-repository) | clone 폴더 밖에서 실행 | 폴더로 이동 |
| [브랜치가 안 보임](docs/10-troubleshooting.md#6-vscode에-브랜치가-안-보임) | VSCode 제한 모드 | 폴더 신뢰 |
