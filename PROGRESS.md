# 진행 로그

> 최신이 위로.

## 2026-07-18 (7) — lsd 입양에 두 번째 커미터 (Mark Linimon)

- **Mark Linimon**(FreeBSD ports 버그 트리아지의 산증인, 수십년 ports Bugzilla 관리)이 Bug 296864 제목 정리:
  `[MAINTAINER] sysutils/lsd: adopt port` → `sysutils/lsd: adopt port`
- **관례 학습**: `[MAINTAINER]` 접두어는 *기존* 메인테이너가 자기 port 고칠 때 붙이는 것. 고아 port *입양*은 그냥 `sysutils/xxx: adopt port`가 정확. → 다음 입양 땐 이 형식으로.
- 제목 정리 = 거절 아니라 **트리아지(정식 처리 대기열에 올림)**. 3시간 만에 커미터 2명(Vladimir 첨부정정 + Mark 제목표준화)이 손댐 = ports 큐 치고 매우 빠름(깔끔한 케이스라 다들 통과 모드).
- 대화 흐름: 01:10 나(요청+패치) → 01:56 Vladimir(patch 인식) → 03:07 Mark(제목). 다음은 누가 commit → Closed/FIXED + 나 lsd 메인테이너 등극.
- 할 일 = 여전히 기다리기.

## 2026-07-18 (6) — 왜 하는가: 한국인 FreeBSD 커미터라는 빈자리 🇰🇷🐡

`git log`(magit-log)로 CURRENT 최근 커밋들을 훑다가 깨달은 것 — 커밋 저자가 거의 유럽/미국/일본(Bjoern Zeeb 독일, Konstantin Belousov 러시아, Kurosawa/Ichiki 일본...). **한국인 FreeBSD 커미터는 극히 드물다.**

배경: 한국은 리눅스 절대 우세라 BSD 저변이 얇음. 일본은 유닉스 문화가 두터워 BSD 커뮤니티 강함(AsiaBSDCon도 도쿄) — 대조가 뼈아픔. 오픈소스 upstream 기여 문화 자체가 한국에선 아직 얇음.

**뒤집으면 이게 기회다:**
- 희소성 = 가치. 레드오션 1만등보다 블루오션 선구자.
- AsiaBSDCon 등에서 한국 발표자는 귀함. "홈랩으로 FreeBSD committer 된 한국인 이야기"는 그 자체로 화제.
- 이 저장소가 한국어 → 나중에 "FreeBSD 하고 싶은 한국인"에게 지도가 될 수 있음.
- "한국 이름이 안 보인다" = "내 자리가 없다"가 아니라 **"아직 비어있는 자리가 있다"**.

지금 magit-log 맨 위에 이미 `Seongil Park`(nvmf 커밋, 3시간 전)가 Bjoern/Mark/Konstantin 사이에 있음. 꾸준함이 무기 — 이 페이스면 몇 달 뒤 이 로그에 정기적으로 등장하게 된다. **그게 이 로드맵을 하는 이유.**

## 2026-07-18 (5) — 첫 리뷰어 반응 (lsd 입양)

- **Bug 296864에 FreeBSD ports 커미터 Vladimir Druzenko(vvd@FreeBSD.org)가 반응**
  - 본인을 CC에 추가(= 지켜보겠다는 신호)
  - 첨부 메타데이터 정정: `is patch: 0→1`, mime `application/mbox → text/plain`
  - 원인: git format-patch 결과물이 `From ...` 헤더로 시작해 Bugzilla가 mbox로 오인 → 다음 patch 첨부 땐 `git diff` 형식 쓰거나 mime을 text/plain으로 직접 지정할 것
- 현재 상태: Status=New, Assignee=freebsd-ports-bugs(Nobody) — 아직 담당 커미터 미배정(정상). 이제 patch로 표시돼 Details/Diff 링크 생김 = 커미터가 클릭 적용 가능
- **할 일 = 없음, 기다리기.** 흐름: 커미터가 집어감 → patch 적용 커밋 → Closed/FIXED + 나 lsd 메인테이너 등극. 며칠~몇 주.
- 의미: 기여가 커뮤니티와 처음 상호작용. 커널 blame에 이름(nvmf) + ports 리뷰 진행(lsd), 두 트랙 다 살아 움직이는 중.

## 2026-07-18 (4) — 개발 환경 완성 + 커널 blame에 내 이름 🎯

- **fish 셸 이관** — bash → fish 기본 셸 (fb-crnt). alias(ls/l/t/gos/gop/ds), starship, fzf, broot, git완성 다 이관. git 자동완성/자동제안/구문 하이라이팅은 fish 기본 내장(설정 0). ble.sh는 GNU 도미노(gmake/gawk) 겪고 "지저분"해서 폐기 → fish로. GNU 걷어내는 게 FreeBSD 정신과도 맞음 ㅋ
- **clangd 커널 탐색 개통** — Doom+eglot+clangd로 `/usr/src` 정의점프(gd) 됨. 삽질 교훈: init.el에 `(cc +lsp)`/`(lsp +eglot)` 켜는 게 **1순위**였는데 compile_commands.json부터 파느라 30분 헤맴. LSP 켜짐 확인 → doom sync → Emacs 재시작 순서. compile DB는 intercept-build로 nvmf 모듈 캡처 + `-I.`→obj절대경로 치환(위치독립).
- **커널 blame에서 내 이름 확인** — `nvmf.c` 306줄 → gd → `nvmf_transport.c` 우리 패치 도착 → `SPC g B`(magit-blame):
  ```
  69  Seongil Park   2026-07-18  nvmf: Report when no transport...   ← 나
  72  John Baldwin   2024-05-03  nvmf: Add infrastructure kernel...  ← nvmf 창시자
  ```
  내 코드가 서브시스템 창시자(jhb, 내 PR 리뷰어) 코드와 같은 함수에 나란히. PR #2329 머지되면 본가 blame에 영구 기록.
- 일주일 전 "buildworld가 뭐야?" → 오늘 자기가 고친 커널 코드에 점프로 도착 + blame에 이름.

## 2026-07-18 (3) — 첫 기여 2건 제출! 🚀🚀

**하루에 src PR + ports 입양 둘 다 세상에 냄. Phase 1(첫 패치) + Phase 2a(메인테이너) 동시 진입.**

### src 기여: nvmf 진단 메시지 (GitHub PR #2329)
- https://github.com/freebsd/freebsd-src/pull/2329
- `nvmf: Report when no transport is registered for a host association`
- 직접 발견한 UX 함정(nvmf_tcp 미로드 시 오해 유발 에러) 수정
- 전 과정 통과: style(9) checkstyle9 0 errors → 모듈 컴파일(-Werror, kprintf 포맷검사 통과) → 런타임 검증(dmesg에 `NVMF: No transport registered for trtype N` 실제 출력 확인) → 커밋 → fork push → PR
- 배운 것: 커널 모듈 반영 3단계(빌드≠설치≠로드), /boot/kernel이 /boot/modules보다 우선, git format-patch로 VM→Mac 패치 이송(fb-crnt엔 gh 토큰 없어서)

### ports 기여: lsd 입양 (Bugzilla Bug 296864)
- https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=296864
- `[MAINTAINER] sysutils/lsd: adopt port` — 고아 port(ports@) 입양, MAINTAINER를 내 이메일로
- ports 워크플로 학습: portlint(경고 읽는 법 — "내 변경과 무관한 기존 경고는 무시"), ports는 GitHub PR이 아니라 **Bugzilla + patch 첨부**로 제출(src와 정책 다름), `[MAINTAINER]` 제목 접두어 관례
- poudriere는 이번엔 불필요(텍스트 한 줄 변경) → difftastic 신규 port 때 데뷔 예정

**다음**: ① 두 건 리뷰 대응 (nvmf=jhb, lsd=ports 팀) ② difftastic 신규 port (+poudriere)
## 2026-07-18 (2) — 자작 NanoBSD NAS "zen" 공개 & 수리 🛠️

- **사용자가 독학으로 NanoBSD 커스텀 NAS OS(zen)를 빌드해 VM으로 가동 중이었음이 밝혀짐** (USB 썸드라이브 타깃 연습용)
  - 15.1 기반, tmpfs /etc·/var(플래시 마모 보호), 32M cfg 파티션, 자작 rc.d(zenzpool), Samba+NFS+rsyncd+ftpd+lighttpd, ZFS 풀(tank) 분리 — 사실상 미니 FreeNAS
- 수리한 것: GPT [CORRUPT](이미지<디스크 크기의 고전 증상) → `gpart recover` + growfs 수동 재실행(firstboot 1회성이라 재부팅으론 안 돎) → 루트 109%→18%
- 발견 1: rc.conf의 `growfs_type=nanobsd-pingpong`은 **FreeBSD base에 존재하지 않는 가공의 knob** (15.1/CURRENT 모두 부재) — 출처 불명 가이드 주의 사례
- 발견 2: ssh 호스트 키가 tmpfs /etc에 있어 부팅마다 재생성 → cfg 영속화 필요
- zen TODO: NANO_IMAGES=2로 진짜 A/B, updatep1/2 업그레이드 절차, 호스트키 영속화, first-boot gpart recover 자동화

## 2026-07-18

- FreeBSD Bugzilla 계정 승인됨 (bugmeister 수동 심사 — AI 스팸 때문에 자동가입 폐지된 시대 ㅋ)
- 다음: nvmf UX 함정 패치 작성 (에러 메시지 + 맨페이지) → GitHub PR

## 2026-07-17 (3) — nvmf "크로스버전 이슈" 조사: 원인 확정 🔍

**결론: 크로스버전 버그가 아니었다. `nvmf_tcp.ko` 미로드 시 connect가 오해를 부르는 에러로 실패하는 UX 함정.**

- 조사 과정 (반나절):
  1. 실험 매트릭스 완성 — CURRENT→15.1만 실패하는 것처럼 보임 (크로스버전 가설)
  2. 용의자 커밋 8개 전수 정독 — 전부 알리바이 성립
  3. 격리 실험: 15.1의 nvmecontrol 바이너리를 CURRENT 커널에서 실행 → 성공 (커널 무죄 판정... 이라 생각했으나)
  4. ktrace 채취 중 재현 소실 → 클린 재부팅으로 재현 조건 복원 → "부팅 후 첫 connect" 패턴 발견
  5. 진범 검거: `kldload nvmf_tcp` 후 connect → 즉시 성공
- 재구성: nvmecontrol의 fabric 로그인은 유저랜드 소켓으로 수행되어 성공하고, 커널 핸드오프 시점에 커널 TCP 전송(nvmf_tcp)이 없으면 `Failed to setup admin queue` + ENXIO. 앞서 "성공"했던 조합들은 전부 target 스택(nvmft/ctld)이 nvmf_tcp를 의존성으로 미리 끌고 온 상태였음
- nvmf(4) 맨페이지에 transport 필요 언급은 한 줄 존재 — 문서 부재가 아니라 **에러 메시지가 원인을 안내하지 못하는 문제**
- **기여 후보 (Phase 1 타깃)**:
  1. 에러 메시지 개선 — transport 미등록 시 "is nvmf_tcp(4) loaded?" 류 힌트 (소형 커널 패치)
  2. nvmecontrol이 connect 시 transport 모듈 자동 로드 (ifconfig가 if_ 모듈 자동 로드하는 선례 있음)
  3. 맨페이지 connect 예제에 kldload nvmf_tcp 명시
- 배운 것: 격리 실험 설계(바이너리 교차 실행), ktrace, 재현 조건의 중요성, "간헐적"처럼 보이는 버그의 상태 의존성

## 2026-07-17 (2) — NVMe-oF 첫 실험 🧪

- **Phase 2b 개시**: VM 2대로 NVMe/TCP 랩 구성
  - Target: 15.1 VM — zvol 5G + ctld(`transport-group`/`controller`/`namespace` 구성) + nvmft, :4420 리스닝
  - 15.1 루프백 연결 성공 → nda0로 attach → newfs/mount/dd까지 완주 (쓰기 207MB/s)
- **크로스버전 이슈 발견**: CURRENT(initiator) → 15.1(target) 연결 시 admin queue 셋업 실패
  - initiator: `nvme0: Failed to setup admin queue` (attach ENXIO), target: `association terminated`
  - 에러 지점 특정: `sys/dev/nvmf/host/nvmf.c:308`
  - 15.1↔CURRENT 분기량: 커밋 8개 / +85줄 — 용의자 명단 짧음
  - 다음: ① 기존 리포트 검색(중복 확인) ② 8개 커밋 정독 ③ 신규면 재현절차 포함 리포트 = **첫 기여 후보**
- 배운 것: ctl.conf가 iSCSI/NVMe-oF 겸용이라는 것, discover는 8009(디스커버리 서비스) 별도라는 것, 에러 문자열 → grep → git log 역추적 루틴

## 2026-07-17

- 커널 모듈 첫 실습 완료 — hello.ko 작성, kldload/kldstat/kldunload 사이클, 모듈 이벤트 핸들러(콜백)와 `void *` 개념 학습
- CURRENT 증분 buildworld 131초 체험 — "CURRENT를 사는" 유지비 확인
- 로드맵 방향 확정: 드릴식 커리큘럼 대신 목표 주도(첫 패치 → ports 메인테이너 → src). 전공 = 스토리지 + 고성능 네트워킹
- 이 저장소 생성

## 2026-07-16

- 16.0-CURRENT VM 구축 (main 스냅샷), src 클론 + 첫 buildworld 완주 (6628초)
  - git.freebsd.org가 느려서 GitHub 미러로 클론하는 요령 습득
- FreeBSD 16 변경사항 학습 — RELNOTES/UPDATING 읽는 법 (pkgbase 기본화, 탈GNU diff3 등)

## 2026-07-14

- VM 디스크 qcow2 → raw 전환 (호스트 ZFS 위 이중 CoW 제거), recordsize=64K 데이터셋 분리

## 2026-07-12

- mini jail에 sqlite3 설치, ZFS snapshot → DELETE → rollback으로 DB 복구 시연 (스토리지 레이어 PITR 개념)

## 2026-07-11 — 시작일

- FreeBSD 15.1-RELEASE VM 구축 (libvirt, cloud-init/nuageinit)
- 첫 buildworld + buildkernel 완주 (5277초 / 303초)
- bin/echo 첫 코드 수정 — /usr/obj 분리 구조, leaky header 추적 (전처리기로 include 경로 파기)
- rc.conf/sysrc, pkgbase, bectl, jail(full/minimal 105MB), gpart/GEOM 학습
- "FreeBSD committer가 꿈"이라고 선언한 날
