# Spec de Espaçamento — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade para espaçamento de layout (gap, padding, margem). Os valores vêm da coleção **Spacing** do arquivo ⭐ Design System TCE (página Spacing). Itens marcados **A DECIDIR** ainda não foram aprovados pelo design: não implemente esses pontos por conta própria, pergunte.
>
> Índice geral: `design-system-index.md`. Grid e layout: `grid-layout-spec-tce.md`.
>
> Espaçamento **de texto** (letter-spacing, word-spacing, line-height, espaço entre parágrafos) é outro assunto: está definido na `typography-spec-tce.md`, seção 5 (decidido em 2026-10-28). A seção 8 abaixo só aponta para lá.

| Campo | Valor |
|---|---|
| **Versão da spec** | **2.0.0** (rascunho) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **1. Átomos (tokens)** |
| **Depende de** (data da última atualização lida) | Nenhuma (é base). Remete a `grid-layout-spec-tce.md` 1.1.0 (2026-10-28, margem de página e gutter) e a `typography-spec-tce.md` 4.2.1 (2026-10-28, espaçamento de texto) |
| **Usada por** | `typography-spec-tce.md`, `grid-layout-spec-tce.md`, `button-spec-tce.md`, `padroes-de-interface.md` e todas as specs de componente |
| Arquivo e Figma | `specs/spacing-spec-tce.md`; coleção Spacing do ⭐ Design System TCE |

Histórico na última seção. Formato do cabeçalho: `design-system-index.md`, seção 4.1.

Origem: variáveis criadas no Figma, CSS original do TCE (`variables_v1.css`, `components-form_v1.css`, `typography_v1.css`, `sections.css`, `main.css`, `grid.css`) e protótipos existentes. A aplicação em um produto específico fica no handoff do produto. Ver também `../referencias/espacamento-e-css-original-correcoes.md`.

## 1. Regras obrigatórias

1. **Nunca use valores soltos** de `gap`, `padding` ou `margin`. Use sempre um token da seção 2 (ou, para margem de página e gutter, os tokens de `grid-layout-spec-tce.md`). Nada de 10, 15, 18, 20, 28, 46.
2. **Escolha o token pelo papel** (seção 3), não pelo valor que parece certo.
3. **Espaço entre irmãos é `gap`; espaço interno é `padding`.** Use `margin` só quando o layout não permitir `gap` (ex.: elementos de fluxo de texto). Não use margin para resolver espaço entre linhas de um texto.
4. **Altura mínima de alvo clicável: 44px no desktop e 48px no mobile** (NBR 17225). O padding do componente não pode reduzir isso.
5. **Se nenhum token serve, pergunte ao design.** Não crie valor novo (seção 12).
6. Ao terminar uma tela, rode o checklist da seção 11.

## 2. Escala

| Token Figma | Valor | rem (px ÷ 16) | Nome no código (decidido, E-5) |
|---|---|---|---|
| `spacing/4` | 4px | 0,25 | `--tcece-space-4` |
| `spacing/8` | 8px | 0,5 | `--tcece-space-8` |
| `spacing/12` | 12px | 0,75 | `--tcece-space-12` (padding lateral do botão com ícone e do chip; E-1 decidida: manter) |
| `spacing/16` | 16px | 1 | `--tcece-space-16` |
| `spacing/24` | 24px | 1,5 | `--tcece-space-24` |
| `spacing/32` | 32px | 2 | `--tcece-space-32` |
| `spacing/48` | 48px | 3 | `--tcece-space-48` |
| `spacing/64` | 64px | 4 | `--tcece-space-64` (**só hero e páginas institucionais**) |
| `spacing/96` | 96px | 6 | `--tcece-space-96` (**só hero e páginas institucionais**) |

**Atenção ao CSS legado.** O arquivo `variables_v1.css` já tem `--tcece-spacing-*` e `--tcece-margin-*` com **outros valores** (ex.: `--tcece-spacing-md` = 16px, `-lg` = 18px, `-xl` = 20px, `-2xl` = 24px). Por isso os tokens novos levam o valor no nome. Não mapeie `spacing/12` para `--tcece-spacing-md`.

### Tokens semânticos (alias da escala)

| Token Figma | Aponta para | Uso |
|---|---|---|
| `spacing/label-input` | 8 | Distância entre label e campo |
| `spacing/title-body` | 16 | Distância entre título e texto de apoio |
| `spacing/form-field-gap` | 16 | Distância entre campos de formulário |
| `spacing/section-section` | 32 | Distância entre seções |
| `spacing/card-padding` | 24 | Padding interno de cards (decidido em 2026-10-28, E-3; antes 16) |
| `spacing/hero-eyebrow-title` | 16 | Hero: linha de apoio → título |
| `spacing/hero-title-body` | 24 | Hero: título → complemento |
| `spacing/hero-section` | 64 | Hero → conteúdo (48 no mobile) |
| `spacing/hero-padding-block` | 96 | Padding vertical do hero (64 no mobile) |

### 2.1 Tipos de espaçamento

| Tipo | Onde está definido |
|---|---|
| Padding interno de componente | Seção 4 |
| Espaço entre irmãos (gap, vertical e horizontal) | Seções 3 e 4 |
| Espaço entre blocos e respiro de página | Seção 5 |
| Margem de página, gutter e colunas | `grid-layout-spec-tce.md` |
| Layout com menu lateral | `grid-layout-spec-tce.md` |
| Espaço de texto (entrelinha, parágrafo, letter e word-spacing) | `typography-spec-tce.md`, seção 5 |
| Espaço entre alvos clicáveis | Seção 6.1 |
| Folga do foco | Seção 6.2 |
| Foco não encoberto por elementos fixos | Seção 6.3 |
| Áreas seguras no mobile | Seção 6.4 |
| Hero e páginas institucionais | Seção 2.2 |
| Densidade | Seção 7 |
| Tamanhos mínimos e de ícone | Seção 6.1 |
| Divisores | Seção 4 |
| Raio, borda, elevação, movimento | Fora desta spec (B-7) |

### 2.2 Hero e páginas institucionais

`spacing/64` e `spacing/96` existem **só** para hero e páginas institucionais (os que usam `display-*`, ver `typography-spec-tce.md`, seção 3.1). Em telas de produto o teto continua 48. Valores: linha de apoio → título 16, título → complemento 24, hero → conteúdo 64 (48 no mobile), padding vertical do hero 96 (64 no mobile). Os 64, 80 e 96 do CSS original eram da página de documentação do guia de estilo e não valem para produto.

### 2.3 Ligação com o MUI

O MUI calcula espaçamento com `theme.spacing(n)`, que multiplica uma base (padrão 8). Com a base 8, a escala é: 4 = `spacing(0.5)`, 8 = `spacing(1)`, 12 = `spacing(1.5)`, 16 = `spacing(2)`, 24 = `spacing(3)`, 32 = `spacing(4)`, 48 = `spacing(6)`, 64 = `spacing(8)`, 96 = `spacing(12)`. No código do MUI use `theme.spacing(n)` (ou `sx={{ p: 3 }}`) em vez de número solto. Os valores padrão do MUI citados na seção 4 são os da versão 9.1.1 do front, a conferir no Context7 (`design-system-index.md`, seção 6.1).

## 3. Como escolher o token

1. O espaço está **dentro** de um componente (entre a borda e o conteúdo)? → **padding**, valores da seção 4.
2. O espaço está **entre elementos irmãos** do mesmo bloco? → **gap**: label→campo 8, campo→campo 16, título→texto 16, rótulo→valor 4, título→subtítulo 8.
3. O espaço está **entre blocos da página** (seção→seção)? → 32. Respiro de página: 48.
4. É a **margem lateral da página** ou o **espaço entre colunas**? → tokens de `grid-layout-spec-tce.md`.
5. É distância entre **linhas ou parágrafos** de texto? → não é espaçamento de layout. Ver seção 8.

## 4. Componentes

A coluna "Fonte" diz de onde vem o valor: **CSS** (CSS original, confirmado), **Figma** (como está hoje no protótipo, ainda não validado contra a escala).

| Componente | Padding | Outros | Referência MUI (a conferir) | Fonte |
|---|---|---|---|---|
| Botão (`contained`, `outlined`, `tceceElevated`, `text`) | 8 vertical, 16 horizontal (12 no lado do ícone) | altura mínima 44 (desktop) e 48 (mobile), largura mínima 64, ícone 20, gap 8. Detalhe em `button-spec-tce.md` | altura 36,5; padding `6 16` | CSS e Figma, 2026-10-28 |
| Botão só com ícone | 10 (alvo de 44); 12 no mobile (48) | ícone 24 | `IconButton` com padding 8 (alvo de 40, abaixo do mínimo) | Spec, 2026-10-28 |
| Input, select | 8 vertical, 16 horizontal | altura mínima 44/48; espaço até o alvo vizinho: 8 (seção 6.1) | padding `16.5 14` | CSS |
| Bloco de código (`pre`) | 8 | margem 16 acima e abaixo | — | CSS |
| Card | 24 (`card-padding`) | 16 entre título e conteúdo; 16 entre conteúdo e ações | `CardContent` 16 | Spec, E-3 |
| Modal | título `16 24`, conteúdo `16 24`, ações `16 24` | 16 entre botões | título `16 24`, conteúdo `20 24`, ações 8 | Spec, 2026-10-28 |
| Chip, selo | 4 vertical, 12 horizontal | altura mínima 32; se clicável ou removível, área de toque de 44 | altura 32; pequeno 24 | Spec e Figma (`Selo`), E-6 |
| Tabela (célula) | 12 vertical, 16 horizontal | altura mínima da linha 48 | `16`; compacta `6 16` | Spec, 2026-10-28 |
| Item de menu e de lista | 8 vertical, 16 horizontal | altura mínima 44/48; 16 entre ícone e texto | `8 16`; ícone com largura mínima 36 | Spec, 2026-10-28 |
| Breadcrumb | item com altura mínima 44 | separador com 8 de cada lado | separador com margem 8 | Spec, 2026-10-28 |
| Alerta (banner) | 16 | ícone 24; 12 entre ícone e texto; 16 até a ação | `6 16`; ícone com margem 12 | Spec, 2026-10-28 |
| Tooltip | 8 vertical, 12 horizontal | distância do gatilho 8 | `4 8` | Spec, 2026-10-28 |
| Toast | 16 | 24 das bordas no desktop e 16 no mobile; 8 entre toasts | `6 16`; 24 das bordas | Spec, 2026-10-28 |
| Aba | 12 vertical, 16 horizontal | altura mínima 48; 8 entre ícone e texto | altura mínima 48, `12 16` | Spec, 2026-10-28 |
| Barra de ações fixa | 16 vertical, 24 horizontal (16 no mobile) | 16 entre botões; o conteúdo da página ganha `padding-bottom` = altura da barra + 24 | — | Spec, 2026-10-28 |
| Divisor | — | 16 de cada lado | `Divider` 1px | Spec, 2026-10-28 |
| Avatar, accordion, menu suspenso, seletor de data, paginação | a levantar | — | — | E-10 |

## 5. Grid e layout de página

Margem de página, gutter, colunas e menu lateral têm spec própria: **`grid-layout-spec-tce.md`** (coleções Grid e Layout; páginas 📏 Grid e 🧱 Layout no Figma). Esses valores (80, 112, 40 e outros) ficam fora da escala deste arquivo de propósito e não servem como padding de componente.

Valores de página que continuam aqui:

| Elemento | Valor | Fonte |
|---|---|---|
| Distância seção→seção | 32 | semântico `section-section` |
| Respiro de página | 48 | escala |
| Espaço do conteúdo até a barra fixa | altura da barra + 24 | Spec, 2026-10-28 |

Os valores 64, 80 e 96px de `div`, `main` e `section` em `main.css`, `grid.css` e `sections.css` são layout da página de documentação do guia de estilo. **Não** são regras para produtos.

## 6. Alvos clicáveis, foco e áreas fixas

### 6.1 Alvos clicáveis

- Altura e largura mínimas: 44px (desktop) e 48px (mobile) (NBR 17225).
- **Entre botões de um grupo: 16.** **Mínimo absoluto entre quaisquer alvos vizinhos: 8** (por exemplo, ícones soltos). Decidido em 2026-10-28 (E-7); o 4 do CSS original não vale.
- Botão só com ícone: padding 10 (44) e 12 no mobile (48), ícone de 24.
- Escala de ícone: **20** (pequeno: botão, chip, texto), **24** (padrão: alerta, menu, cabeçalho) e **32** (grande: estado vazio).

### 6.2 Folga do foco

- Anel de 3px em `tcece/focus/ring` (`outline`, `outline-offset: 1px`) com contorno preto de 1px por fora (`box-shadow: 0 0 0 5px` em `tcece/focus/border`); folga total de **5px** reservada ao redor do elemento.
- Nenhum `overflow: hidden` no ancestral próximo e nenhum padding de contêiner que corte o anel.
- Use `outline`, não só `box-shadow`: no modo de alto contraste do Windows (`forced-colors: active`) o `box-shadow` desaparece e o `outline` permanece. O botão tem foco próprio (fundo amarelo, `button-spec-tce.md`) e acrescenta `outline: 2px solid transparent`.

### 6.3 Foco não encoberto (WCAG 2.2, 2.4.11)

Cabeçalho e barra de ações fixos não podem cobrir o elemento focado. Defina `scroll-padding-top` = altura do cabeçalho fixo + 16 e `scroll-padding-bottom` = altura da barra fixa + 16 (e `scroll-margin` nas âncoras). As alturas do cabeçalho e da barra ainda não estão definidas (E-9).

### 6.4 Áreas seguras no mobile

Use `<meta name="viewport" content="..., viewport-fit=cover">` e, em barra fixa na base, `padding-bottom: calc(16px + env(safe-area-inset-bottom))`; na lateral, `padding-inline: max(<margem>, env(safe-area-inset-left))`.

## 7. Responsivo

A escala de espaçamento (seção 2) é **a mesma em todos os breakpoints**; a única diferença é o hero (seção 2.2: 48 e 64 no mobile). O que muda por breakpoint é margem, gutter e colunas, descritos em `grid-layout-spec-tce.md` (seções 3 e 7).

**Densidade:** o DS tem uma só (confortável). Não há tamanho compacto: os alvos de 44/48 e o piso de 16px de texto já limitam. Se uma tabela de dados exigir densidade maior, a propriedade seria `tceceDensity` (`size` é palavra do MUI); decidir caso a caso.

## 8. Espaçamento de texto (definido na spec de tipografia)

Line-height, letter-spacing, word-spacing e espaço entre parágrafos **não são definidos aqui**: a única definição está em **`typography-spec-tce.md`, seção 5** (decidido em 2026-10-28: letter-spacing e word-spacing `0`, parágrafo 24px, line-height do token, e exigência de que os componentes aguentem os valores da WCAG 1.4.12 sem cortar texto). Os valores do CSS original (letter-spacing 0,08 a 0,12 em, word-spacing 0,16 em, parágrafo 32px) deixam de valer como padrão e passam a ser o **teste de aceitação** de acessibilidade.

## 9. Mapa Figma ↔ código

| Figma | Código (proposta) | Observação |
|---|---|---|
| `spacing/8` | `--tcece-space-8` / `0.5rem` | Figma em px, código em rem (ver `design-system-index.md`, seção 5) |
| `spacing/label-input` | `--tcece-space-label-input` | alias de `--tcece-space-8` |
| `spacing/N` no MUI | `theme.spacing(N ÷ 8)` | Ver seção 2.3 |
| Sintaxe de código no Figma | `var(--tcece-space-N)` em todas as variáveis da coleção | Já preenchida |
| coleção Spacing, modo Default | `:root` | um único modo, sem versão mobile |

Tokens de grid e layout: ver `grid-layout-spec-tce.md`, seção 8. No código, use sempre rem (base 16px, definida em `reset.css`); a escala da seção 2 mostra o par px/rem de cada token.

## 10. Exemplos e redlines

As distâncias anotadas no protótipo, com o token de cada uma, ficam no handoff de cada produto.

## 11. Checklist de revisão

- [ ] Nenhum `gap`, `padding` ou `margin` literal fora da escala
- [ ] Label → campo 8; campo → campo 16; título → texto 16; seção → seção 32
- [ ] Alvos clicáveis com no mínimo 44px (desktop) ou 48px (mobile)
- [ ] Espaço entre linhas e parágrafos resolvido pelo estilo de texto, não por margin
- [ ] Margem de página e gutter conforme `grid-layout-spec-tce.md`
- [ ] Nenhum valor de 18, 20, 28, 36 ou 42 usado como espaçamento (são tamanhos de fonte do CSS legado)
- [ ] Foco visível não cortado pelo container (folga de 5px, `outline`)
- [ ] Entre botões de um grupo 16; entre alvos vizinhos nunca menos de 8
- [ ] Cabeçalho e barra fixos com `scroll-padding` (foco não encoberto)
- [ ] Barra fixa no mobile com `env(safe-area-inset-bottom)`
- [ ] `spacing/64` e `spacing/96` só em hero e páginas institucionais

## 12. Governança

- Valor novo na escala só com aprovação do design system.
- Todo valor fora da escala encontrado em tela deve virar um ajuste ao token mais próximo ou uma exceção registrada aqui, com motivo.
- Mudança de valor de um token existente exige aviso aos devs e lista de usos afetados (a renumeração de `--tcece-measure-0` entre `variables.css` e `variables_v1.css` é o exemplo do que evitar).
- Versionar este arquivo: data e resumo da mudança no topo.

## 13. Pontos em aberto

Os pontos em aberto de espaçamento estão em **`decisoes-em-aberto.md`** (E-9 a E-11); E-1 a E-8 estão decididas. Os de grid e layout, no mesmo arquivo (G-8).

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 2.0.0 | 2026-10-28 | Seção 2.1 (tipos de espaçamento), 2.2 (hero), 2.3 (`theme.spacing`); `spacing/64`, `spacing/96` e semânticos de hero; `card-padding` 16 → 24; padding de modal, tabela, menu, breadcrumb, alerta, tooltip, toast, aba, chip, barra fixa e divisor; seção 6 (alvos, folga do foco, foco não encoberto, áreas seguras); densidade única; E-1, E-3, E-5, E-6, E-7 decididas; sintaxe de código no Figma. **Mudança de valor de token (`card-padding`)** |
| 1.1.0 | 2026-10-28 | Botão com padding 8/16, altura mínima 44/48, largura mínima 64, ícone 20 e gap 8 (fecha E-8); espaçamento de texto remetido à tipografia |
| 1.0.0 | 2026-10-07 | Rascunho de 2026-10-05; grid e layout separados em `grid-layout-spec-tce.md`; revisão estrutural (`ds-v1`) |
