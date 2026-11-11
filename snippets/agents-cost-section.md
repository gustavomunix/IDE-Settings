## Modelos e custo

Teto por 1M de tokens: input **$1,50** e output **$2,50**. Modelo acima do teto não entra em agente, default ou fallback.

| Contexto | Modelo |
|---|---|
| Leitura e análise em massa | `opencode/deepseek-v4.1-flash-free` |
| Código geral | `opencode-go/deepseek-v4.1-flash` |
| Patch pequeno/médio | `opencode-go/qwen3.8-flash` |
| Terminal/DevOps | `opencode-go/glm-5.3-flash` |
| Contexto >200K, PDF ou imagem | `antigravity-shim/gemini-4-argon-high` |
| Tarefa difícil | `opencode-go/deepseek-v4.1-flash#xhigh` |

- Nunca use `opencode-go/gemini-4-argon`. Custa $2/$10 por 1M.
- Rota de assinatura (`claude-agent`, `claude-luciana`, `antigravity-shim`) consome cota. Não é `$0`.
- Nomeie o modelo no prompt do subagente. O modelo é fixo no frontmatter.
- `max` só com pedido explícito.
