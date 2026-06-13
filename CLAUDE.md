# SonAI

AI 학습 및 포트폴리오 제작용 저장소입니다. AI/ML을 공부하면서 만든 실험, 노트, 프로젝트를
이 저장소에 쌓아 포트폴리오로 발전시키는 것이 목표입니다.

## 환경

- OS: Windows 11
- 기본 셸: PowerShell (POSIX 스크립트가 필요하면 Bash 사용)
- 저장소 루트: `d:\Users\son\SonAI`

## Claude 메모리 (중요)

이 저장소는 Claude Code의 **메모리를 git으로 공유**합니다.

- 실제 메모리 데이터: `.claude\memory\` (커밋·공유 대상)
- Claude에게 주어진 사용자별 메모리 경로
  (`C:\Users\son\.claude\projects\d--Users-son-SonAI\memory`)는 위 폴더를
  가리키는 **정션(junction)** 으로만 연결되어 있습니다.

즉 Claude가 자기 메모리 경로에 글을 쓰면 곧바로 `.claude\memory\`에 반영되어
git으로 추적됩니다. 메모리 파일은 frontmatter를 가진 마크다운이며 `MEMORY.md`가 색인 역할을 합니다.

### 다른 PC / 새 클론에서 정션 다시 연결하기

새 환경에서 클론한 뒤, 본인 사용자명에 맞는 메모리 경로로 정션을 한 번 만들어 주면 됩니다
(관리자 권한 불필요):

```powershell
$mem = "$env:USERPROFILE\.claude\projects\d--Users-son-SonAI\memory"
$target = "d:\Users\son\SonAI\.claude\memory"
if (Test-Path $mem) { (Get-Item $mem).Delete() }   # 기존 빈 폴더/링크만 제거
New-Item -ItemType Junction -Path $mem -Target $target
```

> 주의: 정션을 지울 때 `Remove-Item -Recurse`를 쓰면 대상의 실제 데이터까지 삭제될 수
> 있습니다. 링크만 제거하려면 `(Get-Item "<경로>").Delete()`를 사용하세요.

## 버전 관리

- `git add --all` 후 커밋·푸시하면 됩니다. `push.bat`이 이 과정을 자동화합니다.
- `.claude\settings.local.json`은 개인 설정이라 `.gitignore`로 제외합니다.
- `.claude\settings.json`과 `.claude\memory\`는 공유 대상입니다.
