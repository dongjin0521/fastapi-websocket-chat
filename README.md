# fastapi-websocket-chat
FastAPI와 React를 사용한 실시간 웹소켓 채팅 애플리케이션 - 고급웹프로그래밍 실습


# FastAPI + React 웹소켓 채팅 서비스 (Docker & GitHub 배포 가이드 기반)

이 프로젝트는 Docker 환경에서 FastAPI로 웹소켓 채팅 서버를 구성하고, React를 프론트엔드로 사용하여 실시간 채팅 서비스를 구현한 전체 과정을 정리한 것입니다. 개발 환경 세팅부터 GitHub 배포까지의 전체 워크플로우를 포함합니다.

---

## 🧩 주요 기능

- FastAPI 기반의 웹소켓 서버
- React 기반 실시간 채팅 UI
- 다중 채팅방 지원
- 시스템 메시지 (입장/퇴장 알림)
- Docker 컨테이너 기반 개발환경 구성
- GitHub 배포 연동
- ngrok 기반 외부 접속 지원

---

## 📁 프로젝트 구조

```
fastapi-websocket-chat/
├── backend/
│   ├── app/                # FastAPI 서버 코드
│   ├── www/                # React 정적 파일 배포 디렉토리
│   └── ngrok_setup.py      # ngrok 연결 스크립트
├── frontend/               # React 프로젝트
├── .gitignore
├── README.md
```

---

## ⚙️ 기술 스택

- **백엔드**: FastAPI, Uvicorn, WebSocket, pyngrok
- **프론트엔드**: React, JavaScript, WebSocket API
- **배포**: Docker, GitHub
- **편집 환경**: VS Code Remote-SSH

---

## 🚀 빠른 시작 가이드

### 1. GitHub 저장소 생성 및 토큰 발급
- GitHub에서 새 저장소 생성
- Personal Access Token 생성 (`repo` 권한 부여)

### 2. Docker 컨테이너 실행
```bash
docker run -it --name chat-app -p 3000:3000 -p 22:22 ubuntu:20.04 /bin/bash
```

### 3. 컨테이너 내부 설정
```bash
apt update && apt upgrade -y
apt install -y python3 python3-pip nodejs npm git openssh-server python3-venv
```

### 4. SSH 설정 및 VS Code 연동
- `chatuser` 계정 생성 및 sudo 권한 부여
- `/etc/ssh/sshd_config` 수정
- `Remote-SSH` 확장 설치 후 접속

### 5. 백엔드 구현 (FastAPI)
- `uvicorn`, `websockets`, `python-multipart`, `jinja2` 등 설치
- 채팅방 로직 및 WebSocket 이벤트 처리 구현

### 6. 프론트엔드 구현 (React)
```bash
npx create-react-app frontend
```
- 채팅방 목록(RoomList)과 대화창(ChatRoom) 구현
- WebSocket 연결 후 메시지 송수신 구현

### 7. 빌드 및 연동
```bash
npm run build
cp -r build/* ../backend/www/
```

### 8. ngrok 실행
```bash
python ngrok_setup.py
```

---

## ✅ 실행 명령 정리

- 백엔드 서버:
```bash
uvicorn app.app:app --host 0.0.0.0 --port 3000
```

- ngrok 연결:
```bash
python ngrok_setup.py
```

---

## 🛠 주요 문제 해결

- **ERR_NGROK_108**: 기존 ngrok 세션 종료 필요 (dashboard.ngrok.com)
- **React 빌드 오류**: `npm install` 및 캐시 클리어
- **WebSocket 연결 문제**: 프로토콜 (`ws://`, `wss://`) 및 프록시 확인

---

## 🧠 배운 점

- Docker와 SSH를 이용해 원격 환경을 로컬처럼 다루는 법
- React에서 컴포넌트 기반으로 상태 및 이벤트 흐름 처리
- FastAPI의 WebSocket 통신 구조 및 `ConnectionManager` 설계 방식
- 정적 리소스 배포와 API 서버 통합 운영 방식
- ngrok을 통한 개발 중 외부 접근 터널링의 유용성

---

## 📌 향후 개선 아이디어

- 채팅 메시지 저장 기능 (DB 연동)
- 인증된 사용자 채팅 기능 추가
- WebRTC를 이용한 음성/화상 채팅 확장
- Redis 등을 이용한 메시지 브로드캐스트 최적화

---

본 프로젝트는 강의자료 "[Docker + FastAPI + React 웹소켓 채팅 서비스 구현 및 GitHub 배포 가이드]"를 기반으로 구조화되었습니다.
