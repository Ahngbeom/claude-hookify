# Claude Hookify

Claude Code 에이전트 선호도 훅 플러그인. 파일 편집이나 명령어 실행 시 전문 에이전트 사용을 권장합니다.

## Installation

```bash
claude plugin install claude-hookify@ahngbeom-claude-config
```

## Hooks

| Hook | Event | Trigger | Recommended Agent |
|------|-------|---------|-------------------|
| `prefer-commit-commands` | bash | `git commit/push` commands | /commit, /commit-push-pr |
| `prefer-jira-retrospective` | prompt | Retrospective keywords | jira-retrospective |
| `prefer-commit-retrospective` | prompt | Commit retrospective keywords | commit-retrospective |

## How It Works

Hookify 파일은 Claude Code hook 시스템을 활용합니다:

- **`file` event hooks**: 특정 파일 패턴에 매칭되는 파일을 편집할 때 경고 메시지 표시
- **`bash` event hooks**: 특정 bash 명령어 패턴이 감지되면 경고 메시지 표시
- **`prompt` event hooks**: 사용자 입력에 특정 키워드가 감지되면 에이전트 사용 제안

각 훅은 `enabled: true/false`로 개별 활성화/비활성화 가능합니다.

## Hook File Format

```yaml
---
name: prefer-example-agent
enabled: true
event: file          # file | bash | prompt
conditions:          # prompt event는 field: user_prompt
  - field: file_path
    operator: regex_match
    pattern: \.example\.ts$
action: warn         # warn | suggest
---

Markdown body with recommendation message...
```

## Requirements

이 플러그인은 독립적으로 동작하지만, 권장하는 에이전트와 커맨드를 사용하려면 해당 플러그인이 설치되어 있어야 합니다:

- `commit-commands` (공식) - Git workflow 관련 훅
- `productivity-agents` - retrospective 관련 훅

## License

MIT
