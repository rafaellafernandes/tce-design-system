# Spec de Espaçamento — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade para espaçamento de layout (gap, padding, margem). Os valores vêm da coleção **Spacing** do arquivo ⭐ Design System TCE (página Spacing). Itens marcados **A DECIDIR** ainda não foram aprovados pelo design: não implemente esses pontos por conta própria, pergunte.
>
> Índice geral: `design-system-index.md`. Grid e layout: `grid-layout-spec-tce.md`.
>
> Espaçamento **de texto** (letter-spacing, word-spacing, line-height, espaço entre parágrafos) é outro assunto: está definido na `typography-spec-tce.md`, seção 5 (decidido em 2026-10-28). A seção 8 abaixo só aponta para lá.

| Campo | Valor |
|---|---|
| **Versão da spec** | **1.1.0** (rascunho) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **1. Átomos (tokens)** |
| **Depende de** (data da última atualização lida) | Nenhuma (é base). Remete a `grid-layout-spec-tce.md` 1.0.0 (2026-10-28, margem de página e gutter) e a `typography-spec-tce.md` 4.1.0 (2026-10-28, espaçamento de texto) |
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

| Token Figma | Valor | rem (px ÷ 16) | Nome sugerido no código (A DECIDIR, E-5) |
|---|---|---|---|
| `spacing/4` | 4px | 0,25 | `--tcece-space-4` |
| `spacing/8` | 8px | 0,5 | `--tcece-space-8` |
| `spacing/12` | 12px | 0,75 | `--tcece-space-12` — **A DECIDIR** (o CSS original não usa) |
| `spacing/16` | 16px | 1 | `--tcece-space-16` |
| `spacing/24` | 24px | 1,5 | `--tcece-space-24` |
| `spacing/32` | 32px | 2 | `--tcece-space-32` |
| `spacing/48` | 48px | 3 | `--tcece-space-48` |

**Atenção ao CSS legado.** O arquivo `variables_v1.css` já tem `--tcece-spacing-*` e `--tcece-margin-*` com **outros valores** (ex.: `--tcece-spacing-md` = 16px, `-lg` = 18px, `-xl` = 20px, `-2xl` = 24px). Por isso os tokens novos levam o valor no nome. Não mapeie `spacing/12` para `--tcece-spacing-md`.

### Tokens semânticos (alias da escala)

| Token Figma | Aponta para | Uso |
|---|---|---|
| `spacing/label-input` | 8 | Distância entre label e campo |
| `spacing/title-body` | 16 | Distância entre título e texto de apoio |
| `spacing/form-field-gap` | 16 | Distância entre campos de formulário |
| `spacing/section-section` | 32 | Distância entre seções |
| `spacing/card-padding` | 16 | Padding interno de cards — **A DECIDIR** (E-3) |

## 3. Como escolher o token

1. O espaço está **dentro** de um componente (entre a borda e o conteúdo)? → **padding**, valores da seção 4.
2. O espaço está **entre elementos irmãos** do mesmo bloco? → **gap**: label→campo 8, campo→campo 16, título→texto 16, rótulo→valor 4, título→subtítulo 8.
3. O espaço está **entre blocos da página** (seção→seção)? → 32. Respiro de página: 48.
4. É a **margem lateral da página** ou o **espaço entre colunas**? → tokens de `grid-layout-spec-tce.md`.
5. É distância entre **linhas ou parágrafos** de texto? → não é espaçamento de layout. Ver seção 8.

## 4. Componentes

A coluna "Fonte" diz de onde vem o valor: **CSS** (CSS original, confirmado), **Figma** (como está hoje no protótipo, ainda não validado contra a escala).

| Componente | Padding | Outros | Fonte |
|---|---|---|---|
| Botão (`contained`, `outlined`, `elevated`, `text`) | 8 vertical, 16 horizontal | altura mínima 44 (desktop), 48 (mobile), margem 4. Detalhe em `button-spec-tce.md` | CSS |
| Input, select | 8 vertical, 16 horizontal | altura mínima 44, margem 4 | CSS |
| Botão do DS no Figma | 8 vertical, 16 horizontal (12 no lado do ícone) | altura mínima 44 (desktop) e 48 (mobile), largura mínima 64, ícone 20, gap 8 | Figma, alinhado ao CSS em 2026-10-28 (ver `button-spec-tce.md`) |
| Bloco de código (`pre`) | 8 | margem 16 acima e abaixo | CSS |
| Card | 16 (`card-padding`) | gap interno a definir | Spec — **A DECIDIR** (E-3: protótipos usam 24) |
| Modal | a definir | label→campo 8 | falta levantar |
| Chip / badge | 12 horizontal, 3 vertical | altura 30 | Figma — 3 está fora da escala, **A DECIDIR** (E-6). Com o piso de 16px de texto (`title-sm`, line-height 1.4 ≈ 22), proposta: 4 vertical (dentro da escala), altura mínima 30 |
| Barra de ações fixa | a definir | a definir | falta levantar |
| Linha de tabela, item de menu, breadcrumb | a documentar | — | falta levantar |

## 5. Grid e layout de página

Margem de página, gutter, colunas e menu lateral têm spec própria: **`grid-layout-spec-tce.md`** (coleções Grid e Layout; páginas 📏 Grid e 🧱 Layout no Figma). Esses valores (80, 112, 40 e outros) ficam fora da escala deste arquivo de propósito e não servem como padding de componente.

Valores de página que continuam aqui:

| Elemento | Valor | Fonte |
|---|---|---|
| Distância seção→seção | 32 | semântico `section-section` |
| Respiro de página | 48 | escala |
| Espaço do conteúdo até a barra fixa | a definir | falta levantar |

Os valores 64, 80 e 96px de `div`, `main` e `section` em `main.css`, `grid.css` e `sections.css` são layout da página de documentação do guia de estilo. **Não** são regras para produtos.

## 6. Alvos clicáveis

- Altura e largura mínimas: 44px (desktop) e 48px (mobile) (NBR 17225).
- Espaço mínimo entre alvos vizinhos: **A DECIDIR** (o CSS usa margem de 4px).
- O foco visível (outline) não pode ser cortado pelo padding do container.

## 7. Responsivo

A escala de espaçamento (seção 2) é **a mesma em todos os breakpoints**. O que muda por breakpoint é margem, gutter e colunas, descritos em `grid-layout-spec-tce.md` (seções 3 e 7).

## 8. Espaçamento de texto (definido na spec de tipografia)

Line-height, letter-spacing, word-spacing e espaço entre parágrafos **não são definidos aqui**: a única definição está em **`typography-spec-tce.md`, seção 5** (decidido em 2026-10-28: letter-spacing e word-spacing `0`, parágrafo 24px, line-height do token, e exigência de que os componentes aguentem os valores da WCAG 1.4.12 sem cortar texto). Os valores do CSS original (letter-spacing 0,08 a 0,12 em, word-spacing 0,16 em, parágrafo 32px) deixam de valer como padrão e passam a ser o **teste de aceitação** de acessibilidade.

## 9. Mapa Figma ↔ código

| Figma | Código (proposta) | Observação |
|---|---|---|
| `spacing/8` | `--tcece-space-8` / `0.5rem` | Figma em px, código em rem (ver `design-system-index.md`, seção 5) |
| `spacing/label-input` | `--tcece-space-label-input` | alias de `--tcece-space-8` |
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
- [ ] Foco visível não cortado pelo container

## 12. Governança

- Valor novo na escala só com aprovação do design system.
- Todo valor fora da escala encontrado em tela deve virar um ajuste ao token mais próximo ou uma exceção registrada aqui, com motivo.
- Mudança de valor de um token existente exige aviso aos devs e lista de usos afetados (a renumeração de `--tcece-measure-0` entre `variables.css` e `variables_v1.css` é o exemplo do que evitar).
- Versionar este arquivo: data e resumo da mudança no topo.

## 13. Pontos em aberto

Todos os pontos em aberto de espaçamento estão em **`decisoes-em-aberto.md`** (E-1 a E-7; E-8 foi resolvido em `button-spec-tce.md`). Os de grid e layout, no mesmo arquivo (G-1 a G-7).

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 1.1.0 | 2026-10-28 | Botão com padding 8/16, altura mínima 44/48, largura mínima 64, ícone 20 e gap 8 (fecha E-8); espaçamento de texto remetido à tipografia |
| 1.0.0 | 2026-10-07 | Rascunho de 2026-10-05; grid e layout separados em `grid-layout-spec-tce.md`; revisão estrutural (`ds-v1`) |
