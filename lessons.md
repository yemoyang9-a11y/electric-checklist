# lessons

## 2026-11-09 Artifact 게시에서 `files`와 `root`만 보내면 거부됨
- 증상: "`files` and `root` only name supporting files, and nothing was published" 오류.
- 원인: 게시할 대상 파일을 지정하는 `file_path`가 빠졌다.
- 해결(검증됨): `file_path`에 바꾼 파일 하나를 넣고, 나머지만 `files`로 보내 Version 15 게시에 성공했다.

## 2026-11-09 gstack browse의 `eval`이 비동기 결과를 돌려주지 않음
- 증상: `(async () => {...})()` 스크립트를 `$B eval`로 돌리면 출력이 비어 있고, 다음 명령이 실행될 때도 페이지가 아직 순회 중이었다.
- 원인: 이 환경에서 Promise 결과를 기다려 주지 않는 것으로 보인다(동작으로만 확인, 소스는 보지 않음).
- 해결(검증됨): 스크립트를 동기식으로 바꾸고 `location.hash` 변경 뒤 라우터 함수를 직접 호출하니 결과 JSON이 나왔다.

## 2026-11-09 Artifact 안에서는 `#/path` 형태의 해시를 쓰지 않는다
- 증상: Artifact 페이지 규약이 `#name` 형태의 해시만 링크와 주고받는다고 명시한다.
- 해결(검증됨): `#check-0`, `#step-4`처럼 바꾸고 전체 37개 화면 이동을 다시 확인했다.

## 2026-11-09 One Page Love 레퍼런스는 현재 라이브 사이트와 다를 수 있다
- 증상: 라이브 사이트(colinandsamir.com/creator-startup)만 분석해 어두운 시안을 만들었고, 사용자가 기대한 밝은 화면과 달라 시안이 전부 탈락했다.
- 원인: One Page Love의 캡처는 2024년 대기자 모집 버전이고, 라이브 사이트는 이후 강의 안내 페이지로 바뀌었다.
- 해결(검증됨): 소개 페이지 HTML에서 `opl-master-5.jpg`를 찾아 전체 캡처를 받아 보니 라이브에 없는 밝은 커리큘럼 구간이 확인됐다.

## 2026-11-09 REA `capture-browser-scenario` CLI는 이 PC에서 실패하고 MCP는 성공한다
- 증상: CLI가 최소 시나리오에서도 `execution_failure`로 끝났다(Bash와 PowerShell 모두). 같은 입력을 MCP로 보내면 성공했다. CLI가 실패하는 원인은 확인하지 못했다.
- 해결(검증됨): MCP로 캡처하고, 응답이 10MB를 넘어 `resource_constraint`가 나면 `export_evidence_bundle`로 내보낸 파일에서 `normalized_result.steps[].artifacts`를 읽었다.

## 2026-11-09 Bash 도구의 heredoc에서 `\\`가 `\`로 줄어든다
- 증상: heredoc으로 쓴 JSON과 JS, 인라인 Python 정규식이 `Bad escaped character`, `unterminated character set` 오류로 실패했다.
- 해결(검증됨): 백슬래시가 들어가는 스크립트는 Write 도구로 파일을 만들어 실행했다.

## 2026-11-09 `.p p{margin:0}` 리셋이 뒤에 나오는 클래스 여백을 덮어쓴다
- 증상: `.lead`, `.legal` 등에 준 `margin-top`이 적용되지 않아 문단이 붙어 보였다.
- 원인: `.p p`의 명시도(0,1,1)가 `.lead`(0,1,0)보다 높다.
- 해결(검증됨): `.p :where(h1,h2,h3,p,ul){margin:0;padding:0}`로 바꾸고 다시 렌더링해 여백이 살아난 것을 확인했다.
