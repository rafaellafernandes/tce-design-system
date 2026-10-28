# Spec de Botão — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade do componente **Button**. O front usa o **`Button` do MUI** (`@mui/material`), configurado pelo tema (`createTheme`). Não crie um botão novo: use o do MUI com as props da seção 2 e o tema da seção 8. Itens marcados **A DECIDIR** ainda não foram aprovados pelo design: não implemente esses pontos por conta própria, pergunte.
>
> Índice geral: `design-system-index.md`. Cores: `color-spec-tce.md` (seção 5). Tipografia: `typography-spec-tce.md`. Espaçamento: `spacing-spec-tce.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **0.2.0** (rascunho) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão para a próxima tag `ds-vN` (última tag: `ds-v2`; ver `CHANGELOG.md`) |
| Arquivo | `specs/button-spec-tce.md` |

**Quem lê (pessoa ou agente):** anote a **versão** e a **data** acima no PR ou no handoff que usar esta spec. Se a versão que você leu for menor que a do repositório, releia antes de implementar. Versões `0.x` são rascunho e podem mudar. Regra de numeração: o primeiro número muda quando um nome de propriedade ou token muda (quebra); o segundo, quando entra regra ou estado novo; o terceiro, em correção de texto. O histórico está na seção 12.

Origem: componente `Button` (antes `btn`) do arquivo ⭐ Design System TCE (fileKey `mn0wkryj2sBHmW412qD2o8`, página 🧩 Componentes, conjunto `106:3174`), com 216 variantes. Os nomes das propriedades no Figma são os mesmos das props do MUI.

## 1. Regras obrigatórias

1. **Use o `Button` do MUI.** Variação visual vem de `variant`, `color` e do tema, nunca de CSS solto no botão.
2. **Nunca use cor, medida ou fonte solta.** Cores vêm dos tokens `button/*`, `focus/*` (spec de cor), medidas da escala de espaçamento e texto do token `title-sm`.
3. **Altura mínima de 44px no desktop e 48px no mobile** (NBR 17225), por `min-height`, **nunca `height` fixa**: o botão cresce com o texto (WCAG 1.4.12).
4. **O foco visível é sempre amarelo e preto**, em todos os `variant` e `color`, com ou sem hover. Não troque por outro anel.
5. **Cor nunca é o único indicador** de estado: desabilitado usa também `disabled`/`aria-disabled`; selecionado usa também `aria-pressed` ou `aria-current`.
6. **O rótulo diz a ação** ("Salvar", "Enviar para o TCE Ceará"), em até uma linha sempre que possível. Texto em `title-sm`, sem caixa alta (`textTransform: 'none'`).
7. Ao terminar uma tela, rode o checklist da seção 10.

## 2. Mapa Figma ↔ MUI

| Propriedade no Figma | Valores | Prop no MUI | Observação |
|---|---|---|---|
| `variant` | `contained`, `outlined`, `text`, `tceceElevated` | `variant` | `tceceElevated` **não existe no MUI**: é variante customizada do tema (seção 8) |
| `color` | `primary`, `success` | `color` | `contained` + `success` é o botão de criação |
| `tceceDevice` | `desktop`, `mobile` | (nenhuma) | Não existe prop no código: o tema aplica a altura mínima por breakpoint. Use sempre `size="medium"` do MUI. O nome leva prefixo porque `size` do MUI tem outro significado |
| `state` | `default`, `hover`, `pressed`, `focusVisible`, `disabled`, `tceceSelected` | ver seção 4 | Estado não é prop (exceto `disabled`): vem do navegador, do `TouchRipple` e das classes `Mui-*` |
| `startIcon`, `endIcon` | `false`, `true` | `startIcon`, `endIcon` | O ícone se troca em `tceceStartIcon` e `tceceEndIcon` (só Figma) |
| `children` | texto | `children` | Rótulo do botão |
| (não existe no Figma) | — | `disabled`, `fullWidth`, `href` | Valem como no MUI |

Correspondência com os nomes antigos do Figma: Primário = `contained` + `primary`; Criação = `contained` + `success`; Secundário = `outlined`; Terciário = `tceceElevated`; Quaternário = `text`; `Active` = `tceceSelected`; `Dispositive` = `tceceDevice`. Combinações que não existem no Figma (por exemplo `outlined` + `success`) **não devem ser usadas** (B-1).

### 2.1 Prefixo `tcece` (palavras reservadas do MUI)

Nomes que o MUI já usa **não podem ser reaproveitados com outro significado** (props, classes `Mui-*`, `--mui-*`, chaves do tema). Por isso:

- **Espelha o MUI, sem prefixo:** `variant`, `color`, `startIcon`, `endIcon`, `children`, `contained`, `outlined`, `text`, `primary`, `success` e os estados `hover`, `pressed`, `focusVisible`, `disabled`.
- **É nosso, com prefixo `tcece`:** `tceceElevated` (variante), `tceceDevice` e `tceceSelected` (Figma), `tceceStartIcon` e `tceceEndIcon` (trocas de ícone no Figma), `tcece-hover-overlay` (camada do Figma), `--tcece-*` (variáveis CSS), `theme.tcece` (chaves do tema), `.tcece-*` (classes) e `TceceButton` (só se houver wrapper).
- **Nunca** use `--mui-*`, `.Mui-*` nem nomes começando com `Mui` para algo nosso.
- O prefixo único para o repositório inteiro está em `design-system-index.md`, seção 5.

## 3. Anatomia e medidas

| Item | Valor | rem | Fonte |
|---|---|---|---|
| Padding vertical | 8 | 0,5 | `spacing/8` |
| Padding horizontal | 16 | 1 | `spacing/16` |
| Padding no lado do ícone | 12 | 0,75 | Equivale ao −4 do MUI (`marginLeft: -4` no `startIcon`) |
| Espaço ícone ↔ rótulo | 8 | 0,5 | `spacing/8` |
| Ícone | 20 × 20 | 1,25 | MUI usa 20 no `medium` |
| Altura mínima | 44 (desktop), 48 (mobile) | 2,75 e 3 | NBR 17225; por `min-height` |
| Largura mínima | 64 | 4 | Padrão do MUI |
| Raio | 8 | 0,5 | Do DS (o MUI usa 4) |
| Texto | `title-sm`: 16 / 600 / line-height 1,4 | 1 | `typography-spec-tce.md` |
| Estrutura | `startIcon` · rótulo · `endIcon`, alinhados ao centro | — | Layout flex, largura do conteúdo (hug) |

Botão só com ícone **não é este componente**: usa `IconButton` e `aria-label` obrigatório (spec própria, B-5).

## 4. Estados e tokens

Os tokens estão em `color-spec-tce.md`, seção 5. Esta tabela diz **qual usar em cada variante**.

| `variant` | Repouso | Hover | Pressed |
|---|---|---|---|
| `contained` + `primary` | fundo `button/bg/default`, rótulo `button/label/default` | fundo `button/bg/hover-dark`, rótulo `button/label/hover-dark` | fundo `button/bg/pressed` + `TouchRipple` branco |
| `contained` + `success` | fundo verde de criação (**sem token, B-2**), rótulo branco | fundo verde mais claro (**B-2**) | fundo igual ao repouso + `TouchRipple` branco |
| `outlined` | fundo `button/bg/white`, contorno 1px `button/bg/default`, rótulo `button/label/default` | tint de 4% da cor do rótulo sobre o repouso | repouso + `TouchRipple` na cor do rótulo |
| `tceceElevated` | fundo `button/bg/white`, sem contorno, sombra `0 2px 2px rgba(0,0,0,.25)`, rótulo `button/label/default` | tint de 4% | repouso + `TouchRipple` |
| `text` | sem fundo, rótulo `button/label/default` | tint de 4% | repouso + `TouchRipple` |

Estados comuns a todos:

| Estado | Visual | Observação |
|---|---|---|
| `focusVisible` | fundo `button/bg/focus` (amarelo, #FFDD00), rótulo e ícone `button/label/focus` (preto), borda inferior de 4px em `focus/border` (preto) | Contraste 15,6:1. Só com teclado (`:focus-visible`); o clique do mouse não ativa |
| `focusVisible` + hover | igual ao foco, com tint preto de 4% | O amarelo e o preto **não mudam** |
| `focusVisible` + pressed | igual ao foco, com `TouchRipple` preto | A borda preta continua |
| `disabled` | fundo `button/bg/disabled`, rótulo e ícone `button/label/disabled` | Sem hover e sem ripple; use `disabled` (B-4) |
| `tceceSelected` | fundo `button/bg/default`, rótulo branco | Só `outlined` e `text`, usado no item de menu (`aria-current="page"`); fora do `Button` do MUI (B-3) |

### Hover e ripple (padrão do MUI)

- **Hover** nos botões claros é o tint de 4% (`palette.action.hoverOpacity`, já é o padrão do MUI). Nos `contained`, o fundo escurece.
- **Pressed** é o `TouchRipple`: círculo na cor do rótulo (`currentColor`) que nasce no ponto do clique. No teclado (Enter ou Espaço) nasce no centro.
- **Opacidade do ripple por contraste:** o ripple não pode baixar o contraste do rótulo abaixo de 4,5:1 (WCAG 1.4.3). Valores medidos, todos com pelo menos 4,6:1:

| Variante | Opacidade do ripple |
|---|---|
| `contained` + `primary` | 30% |
| `contained` + `success` | 18% |
| `outlined`, `tceceElevated`, `text` | 27% |

  O padrão do MUI é 30%, que **não passa** em quatro destas combinações. Use os valores da tabela.
- **Foco:** desligue o ripple de foco do MUI (`disableFocusRipple`), pois o foco é o amarelo.
- **Movimento reduzido:** com `prefers-reduced-motion: reduce`, não anime o ripple; mantenha o tint.

## 5. Ícones

- `startIcon` e `endIcon` recebem um ícone da biblioteca do DS (hoje `Icons_TCE`), 20 × 20, na cor do rótulo (`currentColor`). A cor do ícone **nunca** é definida à parte: no foco, no hover e no desabilitado ele acompanha o rótulo.
- O ícone é decorativo (`aria-hidden`): a ação é dada pelo rótulo.
- No Figma, o padding de 12 no lado do ícone vale para o botão com ícone. No código, o `margin-left: -4px` do `startIcon` (e `margin-right: -4px` do `endIcon`) produz o mesmo resultado.

## 6. Acessibilidade

- **Alvo clicável:** 44 (desktop) e 48 (mobile) de altura mínima; largura mínima de 64. Espaço entre botões vizinhos: `spacing/8` (E-7).
- **Texto:** `min-height`, nunca altura fixa; o botão não corta o texto com line-height 1,5, letter-spacing 0,12 em e word-spacing 0,16 em (WCAG 1.4.12).
- **Foco visível:** WCAG 2.4.7 e 2.4.11. O amarelo (#FFDD00) sozinho dá 1,35:1 sobre branco, por isso sempre com a borda preta.
- **Contraste:** rótulo e fundo em todos os estados com pelo menos 4,5:1; `button/bg/default` contra o branco dá 7,0:1 como componente de UI (1.4.11). O desabilitado é isento, mas precisa do atributo.
- **Nome acessível:** o texto do rótulo. Botão de ação que abre outra tela ou envia dados diz isso no rótulo.
- **Semântica:** ação usa `<button>`; navegação usa `href` (o MUI renderiza `<a>`). Nunca use `div` clicável.
- **Cor nunca é o único indicador:** `tceceSelected` e `disabled` têm atributo além da cor.

## 7. Uso

| Situação | Variante |
|---|---|
| Ação principal da tela, uma por vez | `contained` + `primary` |
| Criar ou adicionar algo | `contained` + `success` |
| Ação secundária ao lado da principal | `outlined` |
| Ação de apoio sobre fundo claro | `tceceElevated` |
| Ação discreta, menu, ações em linha | `text` |
| Item selecionado no menu lateral | `text` ou `outlined` com `tceceSelected` |

No máximo um botão `contained` + `primary` por área de ação. A ordem e a posição dos botões em um grupo de ações não estão definidas (ver `padroes-de-interface.md`): pergunte ao design.

## 8. Tema MUI (referência para o front)

Valores em rem (base 16px). As cores são os tokens `button/*` e `focus/*`; gere-as de `tokens.json` quando for regenerado (pendência do ds-v3) em vez de copiar os hex.

```ts
import { createTheme, alpha } from '@mui/material/styles';

declare module '@mui/material/Button' {
  interface ButtonPropsVariantOverrides { tceceElevated: true }
}

// Chaves nossas ficam sob theme.tcece (prefixo, ver seção 2.1); nunca no nível do tema do MUI
const tcece = { focus: { bg: '#FFDD00', fg: '#000000' } };   // button/bg/focus, button/label/focus
const focus = tcece.focus;

export const theme = createTheme({
  // tcece,   // exponha com module augmentation de Theme se precisar ler fora do tema
  shape: { borderRadius: 8 },
  palette: {
    primary: { main: '#3855A3', dark: '#2C417A', contrastText: '#FFFFFF' }, // button/bg/default, hover-dark
    success: { main: '#216342', dark: '#2B7D54', contrastText: '#FFFFFF' }, // sem token (B-2)
    action: { hoverOpacity: 0.04 },
  },
  typography: {
    button: {
      fontFamily: '"Noto Sans", sans-serif',
      fontSize: '1rem', fontWeight: 600, lineHeight: 1.4,
      letterSpacing: 0, textTransform: 'none',          // title-sm
    },
  },
  components: {
    MuiButton: {
      defaultProps: { disableElevation: true, disableFocusRipple: true },
      styleOverrides: {
        root: ({ theme }) => ({
          minHeight: '2.75rem', minWidth: '4rem', padding: '0.5rem 1rem',
          [theme.breakpoints.down('md')]: { minHeight: '3rem' },   // 768px (T-10)
          '& .MuiTouchRipple-rippleVisible': { opacity: 0.27 },
          '&.Mui-focusVisible': {
            backgroundColor: focus.bg, color: focus.fg,
            boxShadow: `inset 0 -4px 0 ${focus.fg}`,
          },
          '&.Mui-focusVisible:hover': { backgroundColor: focus.bg },
        }),
        startIcon: { marginLeft: '-0.25rem', marginRight: '0.5rem', '& > *:nth-of-type(1)': { fontSize: '1.25rem' } },
        endIcon:   { marginRight: '-0.25rem', marginLeft: '0.5rem', '& > *:nth-of-type(1)': { fontSize: '1.25rem' } },
        containedPrimary: { '&:active': { backgroundColor: '#1F2E5C' }, '& .MuiTouchRipple-rippleVisible': { opacity: 0.3 } }, // button/bg/pressed
        containedSuccess: { '& .MuiTouchRipple-rippleVisible': { opacity: 0.18 } },
        outlined: { backgroundColor: '#FFFFFF' },
      },
      variants: [
        {
          props: { variant: 'tceceElevated' },
          style: ({ theme }) => ({
            backgroundColor: '#FFFFFF', color: theme.palette.primary.main,
            boxShadow: '0 2px 2px rgba(0,0,0,0.25)',
            '&:hover': {
              backgroundColor: '#FFFFFF',
              backgroundImage: `linear-gradient(${alpha(theme.palette.primary.main, 0.04)}, ${alpha(theme.palette.primary.main, 0.04)})`,
            },
          }),
        },
      ],
    },
  },
});
```

Estado `tceceSelected`: aplique no item de menu (`aria-current="page"`), com fundo `button/bg/default` e rótulo branco; não faz parte do tema do `Button` (B-3).

## 9. Mapa Figma ↔ código

| Figma | Código |
|---|---|
| Componente `Button` (`106:3174`) | `Button` de `@mui/material` |
| `variant`, `color` | props de mesmo nome |
| `tceceDevice` | breakpoint do tema (768px), sem prop |
| `children` | `children` |
| `startIcon` e `endIcon` | props `startIcon` e `endIcon` |
| `state=hover/pressed/focusVisible/disabled` | `:hover`, `TouchRipple`, `.Mui-focusVisible`, `disabled` |
| Camadas `tcece-hover-overlay` e `TouchRipple` do Figma | Comportamento nativo do MUI; não recrie como elemento |
| `button/*`, `focus/*` | `palette` e `styleOverrides` do tema (seção 8) |

Code Connect ainda não está mapeado para o `Button` (B-6).

## 10. Checklist de revisão

- [ ] `Button` do MUI, sem `div` clicável e sem CSS solto no botão
- [ ] `variant` e `color` entre as combinações da seção 2
- [ ] Cores só por tokens `button/*` e `focus/*`; nenhum hex solto na tela
- [ ] Altura mínima 44 (desktop) e 48 (mobile) por `min-height`, sem `height`
- [ ] Foco visível amarelo e preto, inclusive durante hover e clique
- [ ] Ripple com a opacidade da seção 4 (contraste do rótulo ≥ 4,5:1)
- [ ] Ícones de 20px, `aria-hidden`, na cor do rótulo
- [ ] Rótulo claro, em uma linha, sem caixa alta
- [ ] Desabilitado com `disabled` ou `aria-disabled`
- [ ] No máximo um `contained` + `primary` por área de ação

## 11. Pontos em aberto

Todos em **`decisoes-em-aberto.md`** (B-1 a B-6).

## 12. Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 0.2.0 | 2026-10-28 | Prefixo `tcece` (seção 2.1): `tceceElevated`, `tceceDevice`, `tceceSelected`, `tceceStartIcon`, `tceceEndIcon`, `tcece-hover-overlay`, `theme.tcece`. Cabeçalho com versão e data |
| 0.1.0 | 2026-10-28 | Criação: mapa Figma ↔ MUI, medidas, estados, ripple por contraste, foco amarelo e preto, acessibilidade, tema MUI, pendências B-1 a B-6 |
