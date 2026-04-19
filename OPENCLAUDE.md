## Config OpenClaude

```bash
$env:CLAUDE_CODE_USE_OPENAI="1"
$env:OPENAI_BASE_URL="https://openrouter.ai/api/v1"
$env:OPENAI_API_KEY=""
$env:OPENAI_MODEL="qwen/qwen3.6-plus:free"

openclaude

```

```bash
set CLAUDE_CODE_USE_OPENAI=1
set OPENAI_BASE_URL=https://openrouter.ai/api/v1
set OPENAI_API_KEY=
set OPENAI_MODEL=qwen/qwen3.6-plus:free

openclaude

```

### Setar as variaveis no sistema

```bash
[System.Environment]::SetEnvironmentVariable("CLAUDE_CODE_USE_OPENAI", "1", "User")
[System.Environment]::SetEnvironmentVariable("OPENAI_BASE_URL", "https://openrouter.ai/api/v1", "User")
[System.Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "", "User")
[System.Environment]::SetEnvironmentVariable("OPENAI_MODEL", "qwen/qwen3.6-plus:free", "User")
[System.Environment]::SetEnvironmentVariable("OPENAI_MODEL", "nvidia/nemotron-3-super-120b-a12b:free", "User")

```