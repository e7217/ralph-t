# ralph-t

`ralph-t`는 `Branch` 아이디어를 Ralph 형식으로 반복 구현하기 위한 작업 기준 저장소다. 프로젝트 자체는 `선택 후 불안`을 줄이는 열린 가능성 지도(open possibility map)로 요약하고, 이 저장소의 초점은 그 철학이 흔들리지 않도록 환경을 구성하고 반복 실행하는 하네스를 정리하는 데 둔다.

## 프로젝트 요약

- `Branch`는 하나의 정답 경로를 추천하는 플래너가 아니다.
- 사용자가 이미 어떤 선택을 한 뒤에도 미래가 완전히 닫히지 않았음을 보여주는 가능성 지도에 가깝다.
- 핵심 경험은 아래 세 가지를 근거 있게 보여주는 것이다.
  - 복구 가능성
  - 다른 경로와의 합류 가능성
  - 아직 열려 있는 다른 방향
- 따라서 구현은 `best path`를 찾는 쪽이 아니라 `still-open possibilities`를 드러내는 쪽으로 수렴해야 한다.

## Ralph 형식의 핵심 원칙

- `map-first, route-second`
  - 처음부터 상세 경로 하나를 확정하지 않는다.
  - 먼저 4-7개의 방향과 가벼운 연결을 보여주고, 선택 이후에만 상세를 확장한다.
- `dynamic multi-path`
  - 고정된 3경로 템플릿을 쓰지 않는다.
  - 목표마다 다른 전략, 다른 톤, 다른 트레이드오프를 가진 방향을 동적으로 만든다.
- `reassurance before certainty`
  - 확신을 파는 톤을 피하고, 왜 아직 가능성이 열려 있는지 연결 근거를 먼저 설명한다.
- `fail honestly`
  - 다양성이 부족하거나, 연결이 빈약하거나, 사실상 단일 정답처럼 보이는 출력은 좋은 결과로 취급하지 않는다.

## 권장 환경 구성

현재 저장소에는 `guides/` 문서만 있으므로, 반복 코딩을 위해서는 아래 같은 역할 분리가 필요하다.

```text
guides/      설계 원문과 판단 근거
prompts/     Ralph 시스템 프롬프트, 금지 표현, 출력 지침
schemas/     directions/routes/nodes/connections/reassurance 스키마
fixtures/    대표 사용자 목표와 기대 행동 예시
runs/        실행 결과 스냅샷과 비교 로그
checks/      다양성, 연결성, 비순위화 검증 규칙
```

환경 구성의 핵심은 모델을 한 번 잘 돌리는 것이 아니라, 같은 철학을 유지한 채 여러 번 다시 돌려도 출력 품질이 무너지지 않게 만드는 것이다. 그래서 프롬프트, 스키마, 픽스처, 검증 규칙이 분리되어야 한다.

## 실행 방안

Ralph 형식의 반복 실행은 아래 루프로 고정하는 편이 맞다.

1. `goal intake`
   - 사용자 목표를 입력으로 받는다.
2. `landscape generation`
   - 4-7개의 방향성과 가벼운 연결 구조를 만든다.
3. `guardrail check`
   - 단일 정답처럼 보이지 않는지, 경로들이 서로 충분히 다른지, 고립된 dead end가 없는지 검사한다.
4. `direction selection`
   - 하나의 방향을 선택한다.
5. `route expansion`
   - 선택된 방향을 `routes[]`, `nodes[]`, `connections[]` 중심의 상세 경로로 확장한다.
6. `reassurance synthesis`
   - 우측 패널 기준으로 아래 순서를 반드시 채운다.
   - 이 선택이 닫지 않는 것
   - 복구 가능한 지점
   - 다시 만나는 지점
   - 나중에 열릴 수 있는 다른 방향
   - 지금 할 수 있는 가장 작은 다음 행동
7. `snapshot and review`
   - 결과를 저장하고 이전 실행과 비교한다.

이 루프를 고정해 두면, 반복 코딩 시에도 `프롬프트 변경`, `스키마 변경`, `UI 변경`이 각각 어떤 품질 차이를 만들었는지 추적할 수 있다.

## 반복 코딩을 위한 하네스 기준

- 입력과 출력을 항상 구조화한다.
  - 입력은 `goal`
  - 출력은 최소한 `directions[]`, `routes[]`, `nodes[]`, `connections[]`, `reassurance`
- 언어 규칙을 고정한다.
  - 금지: `best`, `correct`, `optimal`
  - 권장: `still open`, `can recover`, `can rejoin`, `another direction may open`
- 품질 평가는 감성 문구가 아니라 연결 구조로 판단한다.
  - 복구 지점이 있는가
  - 합류 지점이 있는가
  - 다른 방향이 실제로 남아 있는가
- 저품질 출력은 축소 모드로 처리한다.
  - 상세 그래프가 약하면 방향 지도만 남기고 과한 확신을 제거한다.

## 현재 README의 의도

이 문서는 구현 결과를 설명하는 README가 아니라, `Branch`를 Ralph 형식으로 반복 개발하기 위한 최소 운영 메모다. 실제 코딩은 `guides/`를 source of truth로 두고, 위 환경 구성과 실행 루프를 먼저 갖춘 뒤 진행하는 것을 전제로 한다.

## 참고 문서

- [guides/2026-03-19-branch-open-possibility-design.md](guides/2026-03-19-branch-open-possibility-design.md)
- [guides/2026-03-19-branch-open-possibility-options.md](guides/2026-03-19-branch-open-possibility-options.md)
