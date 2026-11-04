# SOL MANAGER — 설치형 웹앱

1인 기업·프리랜서를 위한 생활 & 업무 매니저 (구 SOL ENT.). 서버·로그인 없이 브라우저 저장만 사용한다.

탭: 오늘(3가지·글쓰기·운동·기분·알바·집안일) / 프로젝트(마감 D-day·단계·아이디어 냉동실) / 생활(집안일 주기·알바 기록) / 기록(14일 추이·주간 회고) / 설정(목표·루틴·백업)

## 파일

| 파일 | 역할 |
|---|---|
| `index.html` | 앱 전체 (HTML·CSS·JS 한 파일) |
| `manifest.webmanifest` | 앱 이름·아이콘·전체화면 설정 |
| `sw.js` | 서비스 워커 — 오프라인 실행 |
| `icon-*.png`, `icon.svg` | 홈 화면 아이콘 |

## 올리기 — GitHub Pages

```bash
cd solent-pwa
git init
git add .
git commit -m "SOL ENT. v1"
git branch -M main
git remote add origin https://github.com/<계정>/solent.git
git push -u origin main
```

GitHub 저장소 → Settings → Pages → Source: `main` / `/ (root)` → Save.
1~2분 뒤 `https://<계정>.github.io/solent/` 에서 열린다.

> **HTTPS여야 한다.** 서비스 워커는 https 또는 localhost에서만 동작한다. GitHub Pages는 기본 https라 그대로 되고, Netlify·Vercel에 폴더째 드래그해도 된다.
> 로컬 확인은 `python3 -m http.server 8000` 후 `http://localhost:8000`.

## 폰에 설치

- **Android / Chrome** — 사이트를 열면 아래에 "설치" 버튼이 뜬다. 또는 메뉴 → 앱 설치.
- **iPhone / Safari** — 공유 버튼 → 홈 화면에 추가. (iOS는 Safari에서만 된다.)

설치하면 주소창 없이 전체화면으로 열리고, 오프라인에서도 실행된다.

## 데이터

- 기록은 `localStorage`의 `solmanager.v1` 키 하나에 저장된다. **그 브라우저 안에만 있다.** 예전 SOL ENT. 기록(`solent.v1`)은 지우지 않았고 설정 → 예전 SOL ENT 기록 받기로 내려받을 수 있다.
- 기기를 옮기거나 브라우저 데이터를 지우기 전에는 설정 → **JSON 내보내기**로 백업하고, 새 기기에서 **JSON으로 복원**한다.
- 사파리는 오래 안 쓴 사이트의 저장 데이터를 지울 수 있다. 한 달에 한 번 백업해 두는 편이 안전하다.

## 나중에 서버를 붙일 때

저장은 `index.html` 안의 세 함수에만 들어 있다.

```js
readLocal()   // 불러오기
writeLocal()  // 저장
save()        // writeLocal 호출 지점
```

이 셋을 `GET /api/state`, `PUT /api/state` 로 바꾸면 Spring Boot 백엔드로 옮겨진다.
상태는 통째로 하나의 JSON 문서(`S`)라 테이블 설계 없이 `TEXT` 컬럼 하나로도 시작할 수 있다.

## 고치는 순서

일주일 그냥 써 보고, 실제로 매일 누르는 화면이 뭔지 확인한 다음에 그 화면만 손본다.
