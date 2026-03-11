# n8n Self-Hosted AI Starter Kit

n8n + PostgreSQL + Qdrant + Ollama(Mac 네이티브) + Python Task Runner 구성의 자기 완결 배포 패키지.

## 사전 준비

- Docker Desktop 설치 및 실행
- [Ollama](https://ollama.com/) Mac 앱 설치 및 실행
  ```bash
  ollama pull llama3.2
  ```

## 실행 방법

### 1. `.env` 파일 생성

```bash
cp .env.example .env
```

`.env`를 열어 빈 값을 채워 넣습니다. 보안 키는 아래 명령어로 생성:

```bash
openssl rand -hex 32
```

채워야 할 항목:
- `POSTGRES_PASSWORD` — 원하는 비밀번호
- `N8N_ENCRYPTION_KEY` — `openssl rand -hex 32` 출력값
- `N8N_USER_MANAGEMENT_JWT_SECRET` — `openssl rand -hex 32` 출력값
- `N8N_RUNNERS_AUTH_TOKEN` — `openssl rand -hex 32` 출력값

### 2. 빌드

```bash
docker compose build
```

### 3. 실행

```bash
docker compose up -d
```

### 4. 접속

브라우저에서 http://localhost:5678 접속

---

## 포함된 서비스

| 서비스 | 포트 | 설명 |
|--------|------|------|
| n8n | 5678 | 워크플로우 자동화 |
| PostgreSQL | — | n8n 데이터 저장 (내부 전용) |
| Qdrant | 6333 | 벡터 데이터베이스 |
| n8n-runners | — | Python Task Runner |

## 종료

```bash
docker compose down
```

데이터 완전 삭제 (볼륨 포함):
```bash
docker compose down -v
```
