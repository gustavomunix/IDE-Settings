# Modelos ativos e preço

Gerado em 2026-11-11 a partir de `opencode api get /api/model`.
Preço em USD por 1M de tokens. `-` = provider não informa.

Teto: **input $1,50** e **output $2,50** por 1M. `bloqueado` viola o teto.
Shim é `assinatura` (cota da conta), nunca `$0`.

| Modelo | Input | Output | Cache read | Cache write | Contexto | Status |
|---|---|---|---|---|---|---|
| `opencode-go/gemini-4-argon` | $2.00 | $10.00 | $0.1 | $0 | 1048576 | bloqueado |
| `meta/muse-spark-1.3-contributor` | $0.10 | $0.20 | $0.002 | $0 | 1048576 | ok |
| `opencode-go/claude-haiku-5-5` | $0.10 | $0.50 | $0.01 | $0.125 | 1000000 | ok |
| `opencode-go/claude-haiku-5-5 (>100K)` | $0.50 | $2.50 | $0.05 | $0.625 | 1000000 | ok |
| `opencode-go/deepseek-v4.1-flash` | $0.15 | $0.60 | $0.003 | $0 | 1000000 | ok |
| `opencode-go/glm-5.3-flash` | $0.15 | $0.50 | $0.03 | $0 | 1000000 | ok |
| `opencode-go/mimo-v2.6-flash` | $0.14 | $0.28 | $0.003 | $0 | 1048576 | ok |
| `opencode-go/mimo-v2.6-pro` | $0.43 | $0.87 | $0.004 | $0 | 1048576 | ok |
| `opencode-go/muse-spark-1.3-contributor` | $0.10 | $0.20 | $0.002 | $0 | 1048576 | ok |
| `opencode-go/qwen3.8-flash` | $0.15 | $0.47 | $0.016 | $0.2 | 1000000 | ok |
| `opencode/deepseek-v4.1-flash-free` | $0.00 | $0.00 | $0 | $0 | 200000 | grátis |
| `opencode/glm-5.3-flash-free` | $0.00 | $0.00 | $0 | $0 | 200000 | grátis |
| `opencode/inkling-2-small-free` | $0.00 | $0.00 | $0 | $0 | 1048576 | grátis |
| `opencode/longcat-2.5-free` | $0.00 | $0.00 | $0 | $0 | 1000000 | grátis |
| `opencode/minimax-m3.1-flash-free` | $0.00 | $0.00 | $0 | $0 | 1000000 | grátis |
| `opencode/nemotron-3.5-super-vl-free` | $0.00 | $0.00 | $0 | $0 | 1048576 | grátis |
| `antigravity-shim/claude-opus-5-5-high` | subscription | subscription | - | - | 1000000 | assinatura |
| `antigravity-shim/claude-sonnet-5-5-high` | subscription | subscription | - | - | 1000000 | assinatura |
| `antigravity-shim/claude-sonnet-5-5-low` | subscription | subscription | - | - | 1000000 | assinatura |
| `antigravity-shim/claude-sonnet-5-5-medium` | subscription | subscription | - | - | 1000000 | assinatura |
| `antigravity-shim/gemini-3.5-flash-lite` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-3.8-flash-high` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-3.8-flash-low` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-3.8-flash-medium` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-4-argon-high` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-4-argon-low` | subscription | subscription | - | - | 1048576 | assinatura |
| `antigravity-shim/gemini-4-argon-medium` | subscription | subscription | - | - | 1048576 | assinatura |
| `claude-agent/haiku` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-agent/opus` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-agent/sonnet` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-luciana/claude-haiku-5-5` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-luciana/claude-opus-5-5` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-luciana/claude-opus-5-5-fast` | subscription | subscription | - | - | 1000000 | assinatura |
| `claude-luciana/claude-sonnet-5-5` | subscription | subscription | - | - | 1000000 | assinatura |

## Regerar

```bash
opencode api get /api/model | jq -r '.data[] | select(.status=="active") | [.providerID,.id,(.cost|tostring),(.limit.context|tostring)] | @tsv'
```

## Rotas com o mesmo slug

O slug sozinho não identifica o preço. Sempre use `provider/model`.

| Slug | Rota | Cobrança |
|---|---|---|
| `gemini-4-argon` | `opencode-go/gemini-4-argon` | $2 / $10, bloqueado |
| `gemini-4-argon-high` | `antigravity-shim/gemini-4-argon-high` | assinatura Antigravity |
