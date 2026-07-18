# TODO — 놀거리 & 다음 할 것

> "딴거 없나?" 싶을 때 여기서 고른다. 끌리는 거 하나 찍고 시작.
> 완료하면 [PROGRESS.md](PROGRESS.md)로 옮긴다.

## ⏳ 리뷰 대기 중 (제출한 기여)

- [ ] **nvmf PR #2329** 리뷰 대응 — https://github.com/freebsd/freebsd-src/pull/2329 (리뷰어: jhb 예상)
- [ ] **lsd 입양 Bug 296864** 리뷰 대응 — https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=296864 (ports 팀)
- [ ] lsd-rs/lsd **Watch(Releases only)** 걸기 → 1.3.0 나오면 port 업데이트 (poudriere 데뷔 무대)

## 🍒 지금 바로, 가볍게 (30분~1시간)

- [ ] **Nerd Font 정리** — `source ~/.bashrc` 후 `ls`(=lsd) 아이콘 깨지는지 확인. 깨지면 Ghostty 폰트를 Nerd Font로 → lsd/eza/starship 아이콘 전부 살아남
- [ ] **difftastic 진짜 없는지 확정** — `pkg search difftastic`. 없으면 다음 신규 port 후보 확정

## 🔨 반나절, 진짜 배우는 것

- [ ] **clangd로 커널 소스 탐험** ⭐ — Doom에서 nvmf.c 열고 `gd`(정의 점프)로 파고들기. 로드맵 3단계(write(2) 시스템콜 경로 추적)를 실제로. `nvmf_allocate_qpair` → `nvmf_supported_trtype` → ... 타고 들어가기
- [ ] **NVMe-oF 랩 심화** — fio로 iSCSI vs NVMe/TCP 성능 비교, 또는 CHAP 인증 붙이기. 스토리지 전공 실력 + 하다 보면 문서 공백/버그 발견(첫 PR도 이렇게 나옴)

## 🏔 주말 프로젝트

- [ ] **difftastic 신규 port 생성** — poudriere 데뷔. "FreeBSD에 없는 도구를 내가 넣는" 가장 강력한 기여. lsd로 워크플로 배웠으니 다음 단계
- [ ] **zen NanoBSD 완성** — 밀린 TODO: 진짜 A/B 슬라이스(NANO_IMAGES=2), 호스트키 영속화(tmpfs /etc 문제), first-boot gpart recover 자동화. 자작 NAS OS 제대로 굴리기

## 🎲 완전 딴 놀이

- [ ] **bhyve 실험** — FreeBSD 네이티브 하이퍼바이저. nested VM으로 "FreeBSD가 FreeBSD 부팅"
- [ ] **DTrace 맛보기** — 살아있는 커널 실시간 엑스레이. `dtrace -n 'syscall::: { @[probefunc] = count(); }'` 한 줄로 시스템콜 실황. 로드맵 4단계

## 🗒 밀린 숙제 (초창기)

- [ ] echo `-u` 옵션 (bin/echo, 옵션 파싱 연습) — 아직 안 함
- [ ] PostgreSQL jail 실습 — ZFS recordsize 튜닝, 스냅샷/클론 DB 복제

---

## 추천 조합

가벼운 날: **difftastic 확인 → clangd 탐험** (다음 목표 정하고 커널 감각 키우기)
각 잡는 날: **difftastic 신규 port** (poudriere까지 제대로)
