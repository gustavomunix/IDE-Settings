# IDE-Settings

Configuração versionada de agentes, modelos e prompts para OpenCode, OpenChamber e Zed.

## Regra de custo

Teto por 1M de tokens:

- Input: **$1,50**
- Output: **$2,50**

Acima do teto, o modelo fica `disabled` no `opencode.jsonc` e marcado `bloqueado` em `docs/models.md`. Rota de assinatura (shim) não tem preço por token; nunca trate como `$0`.

O mesmo slug em providers diferentes tem preço diferente. Sempre identifique por `provider/model`.

Exemplo: `opencode-go/gemini-4-argon` custa $2/$10; `antigravity-shim/gemini-4-argon-high` consome cota da conta Antigravity.

## Estrutura

```
agents/      12 subagentes em Markdown, com frontmatter model
AGENTS.md    regra de orquestração, tabela de modelos e effort
CLAUDE.md    estilo de código
docs/        catálogo de modelos ativos e preços
snippets/    trechos JSON/JSONC para colar nas configs locais
zed/         settings do Zed sem segredo
```

## Snippets

| Arquivo | Destino | Conteúdo |
|---|---|---|
| `snippets/opencode.providers.jsonc` | `~/.config/opencode/opencode.jsonc` | `model`, `agents`, `providers` com modelos desativados |
| `snippets/openchamber.routing.json` | `~/.config/openchamber/routing.json` | Auto Routing por categoria |
| `snippets/zed.models.json` | `~/.config/zed/settings.json` | `language_models`, `agent`, `agent_servers` |

Os snippets são trechos. Faça merge no arquivo de destino; não substitua o arquivo inteiro.

## Aplicar agentes

```bash
cp agents/*.md ~/.config/opencode/agents/
cp AGENTS.md ~/.config/opencode/AGENTS.md
cp CLAUDE.md ~/.claude/CLAUDE.md
```

## Modelos

`docs/models.md` tem o catálogo ativo e o preço. Regenere depois de qualquer mudança de catálogo.

Regra de bloqueio no OpenCode é por modelo, não por preço. `policies` só aceita `provider.use` (provider inteiro). Use `"disabled": true` em `providers.<provider>.models.<model>`.

Plano: script `sync-models` + `generate-agents` para atualizar catálogo, injetar custo no prompt de cada agente e falhar quando um modelo ativo passar do teto sem exceção.

## Segredos

Nada de chave, token ou senha neste repositório. Config com segredo fica fora, ou use variável de ambiente.
