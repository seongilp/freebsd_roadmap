# 진행 로그

> 최신이 위로.

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
