# Spec de Botão — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade do componente **Button**. O front usa o **`Button` do MUI** (`@mui/material`), configurado pelo tema (`createTheme`). Não crie um botão novo: use o do MUI com as props da seção 2 e o tema da seção 8. Itens marcados **A DECIDIR** ainda não foram aprovados pelo design: não implemente esses pontos por conta própria, pergunte.
>
> Para a API do MUI (props, `styleOverrides`, classes `Mui-*`), consulte a documentação **da versão do MUI do projeto** pelo Context7 (`design-system-index.md`, seção 6.1); as decisões do botão vêm só desta spec. Versão do MUI: B-8.
>
> Índice geral: `design-system-index.md`. Cores: `color-spec-tce.md` (seção 5). Tipografia: `typography-spec-tce.md`. Espaçamento: `spacing-spec-tce.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **0.8.0** (rascunho) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag (o `CHANGELOG.md` registra `ds-v3` como a confirmar; a tag é decisão do design) |
| **Camada** | **1. Átomos (componente)** |
| **Depende de** (data da última atualização lida) | Tokens: `typography-spec-tce.md` (4.2.1, 2026-10-28), `color-spec-tce.md` (2.2.0, 2026-10-28), `spacing-spec-tce.md` (2.0.0, 2026-10-28), `grid-layout-spec-tce.md` (2026-10-21, só os breakpoints). Detalhe na seção 11 |
| **Usada por** | `padroes-de-interface.md` (modais, paginação, estado vazio, formulários) e, quando existirem, as specs de campo de busca, paginação, banner, modal, tabela, menu lateral e header. Detalhe na seção 11 |
| Arquivo | `specs/button-spec-tce.md` |

**Quem lê (pessoa ou agente):** anote a **versão** e a **data** acima no PR ou no handoff que usar esta spec. Se a versão que você leu for menor que a do repositório, releia antes de implementar. Versões `0.x` são rascunho e podem mudar. Regra de numeração: o primeiro número muda quando um nome de propriedade ou token muda (quebra); o segundo, quando entra regra ou estado novo; o terceiro, em correção de texto. O histórico está na seção 13. O formato do cabeçalho e o significado das camadas estão no índice (`design-system-index.md`, seção 4.1).

**Versão do MUI do front:** 9.1.1 (`@mui/material`; informada em 2026-10-28). Na v9, ao trocar o elemento do botão com `component`, informe `nativeButton={false}` (ou `nativeButton` ao contrário); sem isso o MUI avisa em desenvolvimento. O clique por Enter e Espaço agora chega como `MouseEvent`.

Origem: componente `Button` (antes `btn`) do arquivo ⭐ Design System TCE (fileKey `mn0wkryj2sBHmW412qD2o8`, página 🧩 Componentes, conjunto `106:3174`), com 216 variantes. Os nomes das propriedades no Figma são os mesmos das props do MUI.

## 1. Regras obrigatórias

1. **Use o `Button` do MUI.** Variação visual vem de `variant`, `color` e do tema, nunca de CSS solto no botão.
2. **Nunca use cor, medida ou fonte solta.** Cores vêm dos tokens `primary/*`, `tcece/button/*` e `tcece/focus/*` (spec de cor), medidas da escala de espaçamento e texto do token `title-sm`.
3. **Altura mínima de 44px no desktop e 48px no mobile** (NBR 17225), por `min-height`, **nunca `height` fixa**: o botão cresce com o texto (WCAG 1.4.12).
4. **O foco visível é sempre amarelo e preto**, em todos os `variant` e `color`, com ou sem hover. Não troque por outro anel. Acrescente `outline: 2px solid transparent` ao foco: no modo de alto contraste do Windows (`forced-colors: active`) o fundo e a sombra são removidos e só o `outline` aparece (`spacing-spec-tce.md`, seção 6.2).
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
| `contained` + `primary` | fundo `primary/main`, rótulo `primary/contrastText` | fundo `primary/dark`, rótulo `tcece/button/label/hover-dark` | fundo `tcece/primary/pressed` + `TouchRipple` branco |
| `contained` + `success` | fundo verde de criação (**sem token, B-2**), rótulo branco | fundo verde mais claro (**B-2**) | fundo igual ao repouso + `TouchRipple` branco |
| `outlined` | fundo `tcece/button/bg/white`, contorno 1px `primary/main`, rótulo `primary/contrastText` | tint de 4% da cor do rótulo sobre o repouso | repouso + `TouchRipple` na cor do rótulo |
| `tceceElevated` | fundo `tcece/button/bg/white`, sem contorno, sombra `0 2px 2px rgba(0,0,0,.25)`, rótulo `primary/contrastText` | tint de 4% | repouso + `TouchRipple` |
| `text` | sem fundo, rótulo `primary/contrastText` | tint de 4% | repouso + `TouchRipple` |

Estados comuns a todos:

| Estado | Visual | Observação |
|---|---|---|
| `focusVisible` | fundo `tcece/focus/bg` (amarelo, #FFDD00), rótulo e ícone `tcece/focus/label` (preto), borda inferior de 4px em `tcece/focus/border` (preto) | Contraste 15,6:1. Só com teclado (`:focus-visible`); o clique do mouse não ativa |
| `focusVisible` + hover | igual ao foco, com tint preto de 4% | O amarelo e o preto **não mudam** |
| `focusVisible` + pressed | igual ao foco, com `TouchRipple` preto | A borda preta continua |
| `disabled` | fundo `action/disabledBackground`, rótulo e ícone `action/disabled` | Sem hover e sem ripple; use `disabled` (B-4) |
| `tceceSelected` | fundo `primary/main`, rótulo branco | Só `outlined` e `text`, usado no item de menu (`aria-current="page"`); fora do `Button` do MUI (B-3) |

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

- **Alvo clicável:** 44 (desktop) e 48 (mobile) de altura mínima; largura mínima de 64. Entre botões de um grupo: `spacing/16`; mínimo absoluto entre alvos vizinhos: `spacing/8` (decidido, E-7).
- **Texto:** `min-height`, nunca altura fixa; o botão não corta o texto com line-height 1,5, letter-spacing 0,12 em e word-spacing 0,16 em (WCAG 1.4.12).
- **Foco visível:** WCAG 2.4.7 e 2.4.11. O amarelo (#FFDD00) sozinho dá 1,35:1 sobre branco, por isso sempre com a borda preta.
- **Contraste:** rótulo e fundo em todos os estados com pelo menos 4,5:1; `primary/main` contra o branco dá 7,0:1 como componente de UI (1.4.11). O desabilitado é isento, mas precisa do atributo.
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

No máximo um botão `contained` + `primary` por área de ação. Entre botões de um grupo: 16 (mínimo absoluto entre alvos vizinhos: 8, `spacing-spec-tce.md`, seção 6.1). A posição dos botões em um grupo de ações é definida pela spec de cima, `padroes-de-interface.md` (que usa esta): no modal, confirmação (`contained` + `primary`) à direita e cancelar (`outlined`) à esquerda dela; paginação com "Anterior" e "Próximo" em `outlined`. Fora desses casos a ordem não está definida: pergunte ao design.

## 8. Tema MUI (referência para o front)

Valores em rem (base 16px). As cores são os tokens `primary/*`, `tcece/button/*` e `tcece/focus/*`; gere-as de `tokens.json` quando for regenerado (pendência do ds-v3) em vez de copiar os hex.

```ts
import { createTheme, alpha } from '@mui/material/styles';

declare module '@mui/material/Button' {
  interface ButtonPropsVariantOverrides { tceceElevated: true }
}

// Chaves nossas ficam sob theme.tcece (prefixo, ver seção 2.1); nunca no nível do tema do MUI
const tcece = { focus: { bg: '#FFDD00', fg: '#000000' } };   // tcece/focus/bg, tcece/focus/label
const focus = tcece.focus;

export const theme = createTheme({
  // tcece,   // exponha com module augmentation de Theme se precisar ler fora do tema
  shape: { borderRadius: 8 },
  palette: {
    primary: { main: '#3855A3', dark: '#2C417A', contrastText: '#FFFFFF' }, // primary/main, primary/dark, primary/contrastText
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
          [theme.breakpoints.down('md')]: { minHeight: '3rem' },   // 768px (T-10, decidido)
          '& .MuiTouchRipple-rippleVisible': { opacity: 0.27 },
          // MUI 9: as chaves containedPrimary, containedSuccess, outlined etc. foram removidas; use variants no root
          variants: [
            { props: { variant: 'contained', color: 'primary' }, style: { '&:active': { backgroundColor: '#1F2E5C' }, '& .MuiTouchRipple-rippleVisible': { opacity: 0.3 } } }, // tcece/primary/pressed
            { props: { variant: 'contained', color: 'success' }, style: { '& .MuiTouchRipple-rippleVisible': { opacity: 0.18 } } },
            { props: { variant: 'outlined' }, style: { backgroundColor: '#FFFFFF' } },
          ],
          '&.Mui-focusVisible': {
            outline: '2px solid transparent',   // alto contraste (forced-colors)
            backgroundColor: focus.bg, color: focus.fg,
            boxShadow: `inset 0 -4px 0 ${focus.fg}`,
          },
          '&.Mui-focusVisible:hover': { backgroundColor: focus.bg },
        }),
        startIcon: { marginLeft: '-0.25rem', marginRight: '0.5rem', '& > *:nth-of-type(1)': { fontSize: '1.25rem' } },
        endIcon:   { marginRight: '-0.25rem', marginLeft: '0.5rem', '& > *:nth-of-type(1)': { fontSize: '1.25rem' } },
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

Estado `tceceSelected`: aplique no item de menu (`aria-current="page"`), com fundo `primary/main` e rótulo branco; não faz parte do tema do `Button` (B-3).

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
| `primary/*`, `tcece/button/*`, `tcece/focus/*` | `palette` e `styleOverrides` do tema (seção 8) |

Code Connect ainda não está mapeado para o `Button` (B-6).

## 10. Checklist de revisão

- [ ] `Button` do MUI, sem `div` clicável e sem CSS solto no botão
- [ ] `variant` e `color` entre as combinações da seção 2
- [ ] Cores só por tokens `primary/*`, `tcece/button/*` e `tcece/focus/*`; nenhum hex solto na tela
- [ ] Altura mínima 44 (desktop) e 48 (mobile) por `min-height`, sem `height`
- [ ] Foco visível amarelo e preto, inclusive durante hover e clique
- [ ] Ripple com a opacidade da seção 4 (contraste do rótulo ≥ 4,5:1)
- [ ] Ícones de 20px, `aria-hidden`, na cor do rótulo
- [ ] Rótulo claro, em uma linha, sem caixa alta
- [ ] Desabilitado com `disabled` ou `aria-disabled`
- [ ] No máximo um `contained` + `primary` por área de ação

## 11. Specs relacionadas (manter sincronizadas)

O botão é um **átomo** (camada 1): depende só de tokens e **nunca** de moléculas ou organismos (índice, seção 4.1). Esta spec **não repete** valores de outras specs: ela os referencia. Em caso de divergência vale a spec do assunto (índice, seção 4), exceto no que for específico do botão. **Quando uma spec de que ela depende mudar, revise esta e atualize a versão e o histórico; quando uma mudança no botão afetar uma spec que o usa, atualize a outra.**

### 11.1 Depende de (camada 1, tokens)

| Spec | O que o botão herda | Onde nesta spec | Revisar quando mudar |
|---|---|---|---|
| `typography-spec-tce.md` | `title-sm` (16 / 600 / 1,4), Noto Sans, piso de 16px; espaçamento de texto da seção 5 (letter-spacing 0, word-spacing 0) e teste WCAG 1.4.12 | Regra 6, seção 3, seção 6, tema (seção 8) | `title-sm`, line-height, letter-spacing, teste 1.4.12 |
| `color-spec-tce.md` | Tokens `primary/*`, `tcece/button/*` e `tcece/focus/*` (seção 5 da cor), contraste mínimo (regra 4), foco amarelo e preto (regra 5) | Seção 4, seção 6, tema | Qualquer token `button/*` ou `focus/*`, regra de contraste, tokens de criação (B-2) |
| `spacing-spec-tce.md` | Escala (`spacing/8`, `spacing/16`), padding do botão, alvos clicáveis de 44 e 48 (seção 6), espaço entre alvos e folga do foco (seções 6.1 e 6.2). O padding de 12 no lado do ícone usa `spacing/12` (mantido, E-1 decidida) | Seção 3, seção 6 | Escala, linha do botão na seção 4, alvos clicáveis, foco |
| `grid-layout-spec-tce.md` | Breakpoint do mobile (768px, decidido em T-10 e G-1) que define `tceceDevice`; ocupação de colunas (G-6, decidida; o botão não tem largura de coluna própria) | Seção 2, seção 8 | Breakpoints, ocupação de colunas |
| `decisoes-em-aberto.md` | Pendências B-1 a B-7, N-1; E-1, E-7, G-1 e G-6 decididas | Seção 12 | Toda decisão tomada que toque o botão |
| `design-system-index.md` e `CHANGELOG.md` | Precedência, estrutura em camadas, prefixo `tcece`, cabeçalho e versionamento | Seção 2.1 e cabeçalho | Convenções de nome, de camada e de versão |

### 11.2 Usada por (camadas acima)

Ao usar o botão, essas specs referenciam esta e não redefinem variante, estado, medida nem cor. Se o botão mudar, revise cada uma.

| Camada | Spec ou componente | Como usa o botão |
|---|---|---|
| 2. Moléculas e 3. Organismos | `padroes-de-interface.md` | Modais (confirmação `contained` + `primary` à direita, cancelar `outlined` à esquerda), paginação ("Anterior" e "Próximo" em `outlined`), estado vazio (botão primário), formulários (ações) |
| 2. Moléculas (a criar) | Campo de busca, paginação, banner e snackbar, célula de tabela com ação | Botões em linha: `text`, `outlined` |
| 3. Organismos (a criar) | Modal, tabela, header, filtros de busca ("Buscar" e "Limpar filtros"), menu lateral | Menu lateral usa `text` com `tceceSelected`; filtros usam `contained` e `text` |

As specs marcadas "a criar" aparecem em `design-system-index.md`, seção 4.1.

**Specs que o botão precisa e ainda não existem** (por isso os valores estão aqui, provisórios): elevação e sombra (`tceceElevated`), ícones (tamanho 20, biblioteca `Icons_TCE`), raio e borda (raio 8, contorno 1px), movimento (ripple, `prefers-reduced-motion`) e botão só com ícone (`IconButton`). Quando cada uma existir, o valor passa a ser referência a ela (B-7).

## 12. Pontos em aberto

Todos em **`decisoes-em-aberto.md`** (B-1 a B-7).

## 13. Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 0.8.0 | 2026-10-28 | Foco com `outline` transparente para o modo de alto contraste; 16 entre botões de um grupo; dependências conferidas (espaçamento 2.0.0, cor 2.2.0, tipografia 4.2.1) |
| 0.7.0 | 2026-10-28 | MUI 9.1.1 registrado (B-8 decidida); tema ajustado à v9 (as chaves `containedPrimary`, `containedSuccess` e `outlined` de `styleOverrides` foram removidas na v9; viraram `variants` no `root`); regra do `nativeButton`; foco: botão com preenchimento e demais com anel (C-5 decidida); cor 2.1.0 e tipografia 4.1.0 conferidas |
| 0.6.0 | 2026-10-28 | Tokens de cor renomeados conforme `color-spec-tce.md` 2.0.0 (`primary/main`, `primary/dark`, `tcece/primary/pressed`, `tcece/focus/*`, `tcece/button/*`); tipografia 4.0.1 conferida |
| 0.5.2 | 2026-10-28 | Verificação das specs relacionadas (índice, seção 7): data lida da spec de cor atualizada para 2026-10-28 (a spec de cor só ganhou um ponteiro para esta, sem mudança de valor); tipografia, espaçamento, grid-layout e padrões conferidos |
| 0.5.1 | 2026-10-28 | Campo "Camada" encurtado (a metodologia fica só no índice) |
| 0.5.0 | 2026-10-28 | Consulta à documentação do MUI pelo Context7 (índice, seção 6.1); pendência B-8 (versão do MUI do front) |
| 0.4.0 | 2026-10-28 | Camada 1 (átomo) segundo o Atomic Design; cabeçalho padrão com "Camada", "Depende de" e "Usada por"; seção 11 dividida em 11.1 (depende de) e 11.2 (usada por); `padroes-de-interface.md` deixa de ser dependência (é spec de cima) |
| 0.3.0 | 2026-10-28 | Seção 11 (specs relacionadas e dependências), campo "Depende destas specs" no cabeçalho, ordem dos botões em grupos (referência a `padroes-de-interface.md`), pendência B-7 |
| 0.2.0 | 2026-10-28 | Prefixo `tcece` (seção 2.1): `tceceElevated`, `tceceDevice`, `tceceSelected`, `tceceStartIcon`, `tceceEndIcon`, `tcece-hover-overlay`, `theme.tcece`. Cabeçalho com versão e data |
| 0.1.0 | 2026-10-28 | Criação: mapa Figma ↔ MUI, medidas, estados, ripple por contraste, foco amarelo e preto, acessibilidade, tema MUI, pendências B-1 a B-6 |
