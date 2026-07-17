# FreeBSD Committer Roadmap 🐡

> 목표: **FreeBSD src committer**
> 전공 분야: **스토리지(Storage) + 하이퍼포먼스 네트워킹(High-Performance Networking)**
> 시작: 2026-07-11 (첫 buildworld 완주한 날)

## 원칙

1. **목표 주도 학습** — 커리큘럼을 순서대로 밟지 않는다. 실물 목표(패치, port, 벤치마크)를 걸고, 필요한 지식을 그때 흡수한다.
2. **직접 겪은 문제를 고친다** — 홈랩에서 실제로 쓰다가 만난 버그/문서 공백이 최고의 기여 소재다.
3. **CURRENT를 산다** — main 브랜치를 주기적으로 pull/build 하며 개발 흐름 위에서 생활한다.
4. **커뮤니티는 관전부터** — 메일링리스트와 코드 리뷰를 눈팅하며 문화를 흡수한 뒤에 발화한다.

## 왜 스토리지 + 네트워킹인가

- 인프라/운영 배경 (ZFS 실운영, iSCSI, 홈랩 네트워크 구축) → 코드를 읽을 때 "왜 이렇게 설계했는지"가 보이는 영역
- FreeBSD가 세계 최강인 두 분야다 — Netflix Open Connect(전 세계 트래픽의 상당량을 나르는 FreeBSD 박스)가 이 교집합의 상징
- 이 분야 전문가를 채용하는 회사들이 실존한다: Netflix, NetApp, Juniper, iXsystems, Klara

---

## Phase 0 — 기반 다지기 ✅ (완료)

- [x] FreeBSD 15.1-RELEASE VM 구축 (운영 연습용)
- [x] 16.0-CURRENT VM 구축 (개발 추적용)
- [x] buildworld 완주 — RELEASE(5277s) & CURRENT(6628s), 증분 빌드 체험(131s)
- [x] 유저랜드 코드 첫 수정 (bin/echo) — /usr/obj 분리, 스타일(9) 개념
- [x] 시스템 관리 기초 — rc.conf/sysrc, pkg/pkgbase, bectl(부트 환경), jail(풀/미니멀), ZFS 루트
- [x] 커널 모듈 첫 작성 — hello.ko (KLD, 모듈 이벤트 핸들러, kldload/kldstat/kldunload)
- [x] RELNOTES/UPDATING 읽는 습관 시작

## Phase 1 — 첫 패치 제출 🎯 (목표: ~1개월)

**핵심: 내용의 크기가 아니라 프로세스 한 바퀴가 목표.**

- [ ] FreeBSD Bugzilla 계정 생성
- [ ] 전공 분야 맨페이지/문서에서 개선 후보 찾기 — 후보 사냥터:
  - `nvmf(4)`, `nvmecontrol(8)` — NVMe-oF는 신생 서브시스템이라 문서 공백이 많다
  - `ctld(8)`, `iscsi(4)` — 실제로 쓰고 있는 iSCSI 스택
  - `tcp_rack(4)`, `tcp_bbr(4)` — pluggable TCP 스택 문서
- [ ] 패치 작성 (`git diff` 형식) + Bugzilla 제출
- [ ] 피드백 대응 → 머지될 때까지 팔로우업

## Phase 2 — 이름 쌓기 (목표: ~3개월)

### 2a. ports 메인테이너 되기

- [ ] 내가 쓰는 도구 중 port가 없거나 낡았거나 메인테이너 공석(`ports@`)인 것 조사
- [ ] 하나 골라 update/신규 패치 제출 → `MAINTAINER` 필드에 내 이메일 등록
- [ ] 업스트림 릴리스 따라가며 유지보수 반복

### 2b. 전공 홈랩 — NVMe over Fabrics 실험실

FreeBSD의 가장 젊은 스토리지 서브시스템. 모두가 초보라서 지금 진입하면 테스터로서 가치가 크다.

- [ ] VM 2대로 NVMe-oF(TCP) 타깃/이니시에이터 랩 구성 (zvol export)
- [ ] 성능 측정, 이상 동작/문서 공백 기록 → 버그 리포트 or 문서 패치로 환원
- [ ] iSCSI(ctld)와 아키텍처/성능 비교 정리

### 2c. 전공 홈랩 — 고성능 네트워킹

- [ ] pluggable TCP 스택 체험: RACK/BBR 로드 후 기본 스택과 실측 비교 (홈랩 2.5G 환경)
- [ ] kTLS 학습 — Netflix가 base에 넣은 그 코드 읽기
- [ ] netmap(4) 개념 학습 — 커널 바이패스 프레임워크

### 2d. 커뮤니티 관전

- [ ] 메일링리스트 — 시작은 3개만: **freebsd-current@**(CURRENT 생존), **freebsd-fs@**(스토리지), **freebsd-net@**(네트워킹). 웹 아카이브 눈팅으로 시작해도 됨. 나중에 freebsd-scsi@(CAM/NVMe), freebsd-hackers@ 추가
- [ ] Phabricator(reviews.freebsd.org)에서 전공 분야 리뷰 매주 눈팅
- [ ] Drew Gallatin의 Netflix 발표들 시청 (NUMA, 400Gbps serving)

## Phase 3 — src 기여 (목표: 6~12개월)

- [ ] 홈랩에서 직접 겪은 버그를 src 레벨에서 수정 → Phabricator 리뷰 제출
- [ ] 전공 서브시스템(cam/nvmf/netinet)에서 반복 기여
- [ ] 커널 지식 심화는 이 단계의 필요가 소환하는 순서로: KLD 심화 → 시스템콜 경로 → DTrace → 락킹/메모리
- [ ] 기여가 쌓이면: 기존 committer의 멘토링 → commit bit 제안은 그들이 먼저 꺼낸다

---

## 상비 자원

| 자원 | 용도 |
|---|---|
| McKusick 외, *The Design and Implementation of the FreeBSD OS* 2판 | 설계 의도가 궁금할 때 찾아 읽는 사전 |
| [FreeBSD Architecture Handbook](https://docs.freebsd.org/en/books/arch-handbook/) | 커널 내부 공식 문서 (무료) |
| [Developers' Handbook](https://docs.freebsd.org/en/books/developers-handbook/) | KLD 등 실습 튜토리얼 |
| `man 9 <api>` | 커널 API 공식 문서 — 코드 읽다 막히면 1순위 |
| /usr/src 자체 | 최고의 교과서. `grep -r`이 스승 |

## 주간 루틴 (CURRENT 생활)

```sh
cd /usr/src && git pull
git log --oneline HEAD@{1}..HEAD | head -30   # 이번 주 커밋 구경
git diff HEAD@{1} RELNOTES UPDATING            # 신문 읽기
make -j8 buildworld                            # 증분이라 몇 분
```

## 진행 로그

[PROGRESS.md](PROGRESS.md) 참고.
