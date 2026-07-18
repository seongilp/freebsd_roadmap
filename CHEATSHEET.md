# 치트시트 — Emacs / Doom / Magit

> evil(vim) 모드 기준. **외우지 말 것** — Doom은 `SPC` 누르고 기다리면 다음 키 후보가 뜬다.
> 이 목록은 "자주 쓰는 것 감 잡기"용.

## 생존 필수

| 키 | 뜻 |
|---|---|
| **`C-g`** | 취소 (막히면 무조건 이거. 만능 탈출) |
| `SPC q q` | Doom 종료 |
| `SPC .` | 파일 열기 (경로) |
| **`SPC SPC`** | 프로젝트 파일 열기 (이름으로) ⭐ |
| `SPC ,` | 열린 버퍼 전환 |
| `:w` / `:q` | 저장 / 닫기 (vim) |
| `SPC : doom/reload` | config.el 변경 반영 (재시작 없이) |

## 버퍼 관리

| 키 | 뜻 |
|---|---|
| `SPC ,` / `SPC b b` | 열린 버퍼 목록/전환 (타이핑으로 좁힘) |
| **`SPC b k`** | 현재 버퍼 죽이기(닫기) |
| `SPC b n` / `SPC b p` | 다음 / 이전 버퍼 |
| (Magit 창에서) `q` | Magit 버퍼 닫기 |

> 버퍼는 수십 개 쌓여도 문제없다 — `SPC ,`로 타이핑해 찾으면 됨. 정리 강박 불필요.

## 이동 / 검색 (커널 탐험)

| 키 | 뜻 |
|---|---|
| **`gd`** | 정의로 점프 (LSP/clangd) |
| **`C-o` / `C-i`** | 뒤로 / 앞으로 (점프 히스토리) |
| `gr` | 이 심볼 참조 전부 찾기 |
| `K` | 심볼 문서/타입 팝업 (안 움직이고 슬쩍) |
| **`SPC s p`** | 프로젝트 전체 내용 검색 (grep) ⭐ |
| `/` | 현재 파일 내 검색 (evil) |
| `SPC s i` | 이 파일의 함수/심볼 목록 점프 |

## 창 / 분할

| 키 | 뜻 |
|---|---|
| `SPC w v` / `SPC w s` | 세로 / 가로 분할 |
| `SPC w w` | 창 전환 |
| `SPC w h/j/k/l` | 왼/아래/위/오른쪽 창 이동 |
| `SPC w c` | 현재 창 닫기 |
| **`SPC w o`** | 현재 창만 남기고 나머지 닫기 (좌우분할 정리용) |

## Magit (git)

| 키 | 뜻 |
|---|---|
| **`SPC g g`** | Magit status (git 홈) ⭐ |
| **`SPC g B`** | blame (줄별 커밋/작성자) |
| `SPC g L` | 이 파일 커밋 히스토리 |

**Magit status 화면 안에서:**

| 키 | 뜻 |
|---|---|
| `TAB` | 섹션 접기/펼치기 |
| `s` / `u` | 스테이지 / 언스테이지 |
| `c c` | 커밋 (메시지 쓰고 `C-c C-c` 확정) |
| `P p` / `F p` | push / pull |
| `l l` | 로그 |
| `b b` / `b c` | 브랜치 전환 / 생성 |
| `Enter` | 커밋·파일 위에서 → 상세 diff |
| **`?`** | 전체 명령 메뉴 (Magit 학습 왕도) |
| `q` | 나가기 |

## 핵심 3개만

1. **`C-g`** — 막히면 탈출
2. **`SPC SPC`** — 파일 순간이동
3. **`?` (Magit 안)** — 뭐 할 수 있는지 다 보여줌

---

## fb-crnt fish alias (참고)

| alias | 명령 |
|---|---|
| `gos` / `gop` | `cd /usr/src` / `cd /usr/ports` |
| `ds` | `doom sync` (init.el 고친 뒤) |
| `ls` / `l` / `t` | lsd (기본/`-altr`/tree) |
| `ll` / `la` / `lt` | eza (상세/all/tree) |

## LSP 안 될 때 체크 순서 (커널 소스 탐색)

1. Doom `~/.config/doom/init.el`에 `(lsp +eglot)` + `(cc +lsp)` 주석 풀렸나 → `ds`(doom sync) → **Emacs 완전 재시작**
2. `/usr/src/compile_commands.json` 있나 (intercept-build로 생성, `-I.`은 obj 절대경로로)
3. `gd`가 TAGS 물으면 = LSP 안 붙은 것 (1번 확인)
