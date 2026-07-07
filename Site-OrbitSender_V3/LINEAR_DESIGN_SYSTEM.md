# Linear Design System — referência para o OrbitSender (indexprincipal.html)

Extraído do dump real em `linear.app/index.html` + `linear.app/assets/*.css`.
Este é o design system base do site OrbitSender. Sempre seguir estes tokens/padrões.

## Cores (tema escuro / marketing — o padrão do Linear)

| Token | Valor |
|---|---|
| `--color-bg-marketing` | `#010102` |
| `--color-bg-primary` | `#08090a` |
| `--color-bg-level-1` | `#0f1011` |
| `--color-bg-level-2` | `#141516` |
| `--color-bg-level-3` | `#191a1b` |
| `--color-bg-secondary` | `#1c1c1f` |
| `--color-bg-tertiary` | `#232326` |
| `--color-text-primary` | `#f7f8f8` |
| `--color-text-secondary` | `#b4bcd0` (ou `#d0d6e0`) |
| `--color-text-tertiary` | `#8a8f98` |
| `--color-text-quaternary` | `#62666d` |
| `--color-border-primary` | `#23252a` |
| `--color-border-secondary` | `#34343a` |
| `--color-border-translucent` | `rgba(255,255,255,0.08)` |
| `--color-border-translucent-strong` | `rgba(255,255,255,0.12)` |
| `--color-accent` | `#7170ff` |
| `--color-accent-hover` | `#828fff` |
| `--color-brand-bg` | `#5e6ad2` |

## Tipografia

- Família: **Inter Variable** (`"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, …`)
- Serif display (raro): `"Tiempos Headline", Georgia, serif`
- Pesos: **regular 400 · medium 510 · semibold 590 · bold 680**
- Letter-spacing dos títulos grandes: **-0.022em**

Escala de títulos:

| Token | Tamanho | line-height |
|---|---|---|
| title-1 | 1.0625rem (17px) | 1.4 |
| title-2 | 1.25rem (20px) | 1.33 |
| title-3 | 1.5rem (24px) | 1.33 |
| title-4 | 2rem (32px) | 1.125 |
| title-5 | 2.5rem (40px) | 1.1 |
| title-6 | 3rem (48px) | ~1.1 |
| title-7 | 3.5rem (56px) | 1.1 |
| title-8 | 4rem (64px) | 1.0 |

Texto: regular **15px** (0.9375rem) · small **14px** · mini **13px** · large **17px** (lh 1.6).

## Layout

- `--homepage-max-width`: **1436px** (= 1344 + 46×2)
- `--page-padding-inline` (outer): **46px** · inset interno: 32px
- `--header-height`: **65px** · `--header-blur`: 20px
- `--grid-gap`: **32px**
- `--rounded-full`: 9999px
- Easing padrão: `--ease-out-quad: cubic-bezier(0.25, 0.46, 0.45, 0.94)`

## Padrão de SEÇÃO (`PageSection`)

- Espaçamento vertical: **padding-top 96px / padding-bottom 128px** (desktop) → **48px / 96px** (mobile).
- **Header em grid 2 colunas** (`grid-template-columns: 1fr 1fr`, `padding-bottom: 96px`):
  - Coluna esquerda: **título h2** — title-6 (48px), `font-weight: 510` (medium), `text-wrap: balance` → cai p/ title-5 (40px) → title-3 (24px) no responsivo.
  - Coluna direita: **descrição p** — title-3 (24px) → title-2 (20px) → title-1 (17px) → regular no responsivo, `text-wrap: balance`, cor secundária.
  - No mobile: vira **1 coluna** (`grid-template-columns: 1fr`, `padding-bottom: 64px`).
- Conteúdo abaixo do header: grids/bento de cards com bordas `1px solid translucent`, raio 12–16px.

## Padrões da HERO (já implementados no indexprincipal.html)

- Texto **alinhado à esquerda**: título no topo, depois uma linha flex (`justify-content: space-between`) com subtítulo à esquerda + link de novidade à direita (com pulse dot).
- Header fixo com blur, marca + nav + CTA; ganha borda ao rolar.
- Ilustração (interface do produto) **plana** (sem 3D), **largura total alinhada às margens do texto** (x=48 a x=1392 em 1440).
- Mobile: interface mantém layout "real" (sidebar recolhida em ícones), mostra só os 4 cards (2×2) e o resto **dissolve com degrade** para o fundo.
- Finalização/transição: faixa de **gradiente roxo animado** (looping) **atrás da dashboard**, opacidade some no topo (máscara), vaza um pouco para baixo com **corte reto** na base = divisor. Full-bleed real com `width: 100vw; margin-inline: calc(50% - 50vw)`.

## Observações técnicas

- `mask-image: url(...)` (imagem externa) é **bloqueado por CORS** ao abrir via `file://`. Máscaras com `linear-gradient(...)` funcionam normalmente.
- `body { overflow-x: hidden }` permite usar `100vw` sem scroll horizontal.
- Verificação visual sempre via Playwright (Chromium), conferindo console sem erros + responsivo (desktop 1440/1920, mobile 390).
