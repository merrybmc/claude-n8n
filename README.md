# Claude Code + n8n 설정

다른 컴퓨터에서 같은 환경을 세팅하는 방법입니다.

## 사전 준비

- [Node.js](https://nodejs.org/) 설치 (v18 이상)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) 설치
- [Claude Code](https://claude.ai/code) 설치

## 1. n8n MCP 서버 설치

```powershell
npm install -g n8n-mcp
```

## 2. n8n 실행 (Docker)

```powershell
docker run -d --name n8n -p 5678:5678 docker.n8n.io/n8nio/n8n
```

## 3. n8n API 키 발급

1. 브라우저에서 `http://localhost:5678` 접속
2. 계정 생성 또는 로그인
3. 우상단 프로필 → Settings → API → Create API Key
4. 발급된 키 복사

## 4. 프로젝트 폴더 설정

```powershell
# 프로젝트 폴더로 이동
cd "C:\Users\YOUR_USERNAME\OneDrive\바탕 화면\automatic"

# .env 파일 생성
Copy-Item .env.example .env
# .env 파일을 열어 YOUR_N8N_API_KEY_HERE를 실제 API 키로 교체
notepad .env

# .claude 폴더 생성
New-Item -ItemType Directory -Force .claude

# settings.json 복사
Copy-Item claude-dotfiles\.claude\settings.json .claude\settings.json
# settings.json에서 YOUR_USERNAME과 YOUR_N8N_API_KEY를 실제 값으로 교체
notepad .claude\settings.json

# settings.local.json 복사
Copy-Item claude-dotfiles\.claude\settings.local.json.example .claude\settings.local.json
```

## 5. 전역 Claude 설정 (선택)

`%USERPROFILE%\.claude\settings.json`:
```json
{
  "autoUpdatesChannel": "latest",
  "theme": "dark-ansi"
}
```

## 파일 구조

```
automatic/
├── .claude/
│   ├── settings.json          # MCP 서버 설정 (API 키 포함, git 제외)
│   └── settings.local.json    # 권한 설정 (git 제외)
├── .env                       # 환경 변수 (git 제외)
└── .env.example               # 환경 변수 템플릿 (git 포함)
```

## MCP 서버 경로 확인

```powershell
npm root -g
# 출력된 경로 + \n8n-mcp\dist\mcp\stdio-wrapper.js 가 settings.json의 args 경로
```
