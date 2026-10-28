# Spec de Cor — Design System TCE Ceará (RASCUNHO, escopo parcial)

> **Para o Claude do dev:** este arquivo é a fonte de verdade para as cores de **texto, links, botões e fundos/superfícies**. Os valores vêm das coleções **Color / Primitives** e **Color / Semantic** do arquivo ⭐ Design System TCE (página 🎨 Cores). Bordas, ícones, status/alertas, tabelas e o legado ainda não têm spec (seção 9). Itens **A DECIDIR** não se implementam sem resposta do design.
>
> Índice geral: `design-system-index.md`. Tipografia: `typography-spec-tce.md`.

Status: rascunho de 2026-10-05. Escopo parcial. Revisão estrutural em 2026-10-07 (versão **ds-v1**).

## 1. Regras obrigatórias

1. **Use sempre o token semântico** (`text/primary`, `button/bg/default`…). Nunca use a primitiva (`gray/800`), o hex solto ou uma cor copiada do Figma.
2. **Escolha o token pelo papel**, não pela cor que parece certa.
3. **Cor nunca é o único indicador** de erro, sucesso, status ou link: acompanhe de ícone e texto, e sublinhe links em texto corrido (WCAG 1.4.1).
4. **Contraste mínimo:** 4,5:1 para texto normal e 3:1 para texto grande e para componentes de UI e ícones que carregam informação (WCAG 1.4.3 e 1.4.11). Texto desabilitado é isento.
5. **Foco visível:** sempre o anel amarelo (`focus/ring`) com o contorno preto (`focus/border`) juntos. O amarelo sozinho dá 1,35:1 sobre branco.
6. **Se nenhum token serve, pergunte ao design.** Não crie cor nova.
7. Ao terminar uma tela, rode o checklist da seção 10.

## 2. Arquitetura

- **Color / Primitives:** escalas 50–900 de gray, blue, green, red e yellow, mais white, black, purple/700 e alpha/black-60. Sem significado de uso; ocultas nos seletores do Figma. **Não use em telas nem em componentes.**
- **Color / Semantic:** dá o papel e aponta para uma primitiva. Um modo (Light). Se uma escala mudar, tudo que usa o token muda junto.
- **Collection Focus:** `focus/ring` e `focus/border`.
- **Legado:** `legacy/Gray/*`, `legacy/Blue/*` e `legacy/Green/*` são aliases obsoletos, mantidos só para não quebrar usos antigos. **Não use em código novo.**

## 3. Texto

Contraste calculado sobre o fundo indicado.

| Token | Primitiva | Hex | Contraste | Uso |
|---|---|---|---|---|
| `text/primary` | gray/800 | #27282C | 14,7:1 sobre branco | Texto principal: títulos, corpo, valores |
| `text/secondary` | gray/700 | #474C52 | 8,7:1 sobre branco | Apoio: descrições, ajuda, breadcrumb, rótulos secundários |
| `text/placeholder` | gray/700 | #474C52 | 8,7:1 sobre branco | Placeholder, em itálico. Nunca substitui o label |
| `text/disabled` | gray/600 | #73787E | 4,45:1 (isento) | Texto desabilitado |
| `text/inverse` | white | #FFFFFF | 14,7:1 sobre `surface/inverse` | Texto sobre fundo escuro |
| `text/error` | red/700 | #A31D24 | 7,6:1 sobre branco | Mensagem de erro, com ícone |
| `text/success` | green/800 | #206442 | 7,1:1 sobre branco | Mensagem de sucesso, com ícone |
| `text/info` | blue/700 | #3855A3 | 7,0:1 sobre branco | Mensagem informativa |
| `text/on-warning` | gray/900 | #1C1D1F | 9,1:1 sobre `status/warning/default` | Texto sobre o preenchimento amarelo de alerta |

- O amarelo de alerta **nunca** é cor de texto (1,9:1 sobre branco).
- Sobre `surface/page` (#F7F8FA) os pares continuam acima de 4,5:1: `text/primary` 13,9:1, `text/secondary` 8,2:1, `text/error` 7,2:1, `text/success` 6,7:1, `link/default` 6,6:1.
- Sobre `table/row/blue`: `text/primary` 13,3:1 e `link/default` 6,3:1.
- O mapa de qual token de texto usar por elemento (título, label, helper, tabela…) está em `typography-spec-tce.md`, seção 4.

## 4. Links

| Token | Primitiva | Hex | Contraste sobre branco | Uso |
|---|---|---|---|---|
| `link/default` | blue/700 | #3855A3 | 7,0:1 | Link. Sempre sublinhado em texto corrido |
| `link/visited` | purple/700 | #551A8B | 11,0:1 | Link visitado |
| `link/hover` | blue/800 | #2C417A | 9,8:1 | Link em hover |
| `link/disabled` | gray/600 | #73787E | 4,45:1 (isento) | Link desabilitado |

Link em foco usa o padrão de foco da regra 5.

## 5. Botões

> Uso no componente (variantes, estados, ripple e foco): `button-spec-tce.md`. Esta seção é a fonte dos tokens; se um token `button/*` ou `focus/*` mudar, revise aquela spec.

| Estado | Fundo | Rótulo | Contraste | Observação |
|---|---|---|---|---|
| Primário | `button/bg/default` (blue/700) | `button/label/default` (white) | 7,0:1 | Ação principal |
| Primário em hover | `button/bg/hover-dark` (blue/800) | `button/label/hover-dark` (white) | 9,8:1 | |
| Pressionado | `button/bg/pressed` (blue/900) | `button/label/default` (white) | 13,1:1 | `button/bg/active` tem o mesmo valor (unificar, ver C-3) |
| Secundário em hover | `button/bg/hover-light` (blue/100) | `button/label/hover-light` (blue/800) | 7,9:1 | Também terciário |
| Desabilitado | `button/bg/disabled` (gray/100) | `button/label/disabled` (gray/700) | 7,3:1 | Isento de contraste |
| Foco | `button/bg/focus` (yellow/300) | `button/label/focus` (black) | 15,6:1 | Sempre com contorno `focus/border` |

- Botão secundário em repouso: fundo `button/bg/white` com contorno `button/bg/default`.
- `button/bg/default` contra o branco dá 7,0:1, então passa 3:1 como componente de UI.
- `button/bg/disabled` contra o branco dá 1,2:1: isento por ser desabilitado, mas o estado precisa ser comunicado também pelo atributo `disabled`/`aria-disabled`.

## 6. Fundos e superfícies

| Token | Primitiva | Hex | `text/primary` sobre ele | Uso |
|---|---|---|---|---|
| `surface/default` | white | #FFFFFF | 14,7:1 | Cards, campos, modais |
| `surface/page` | gray/50 | #F7F8FA | 13,9:1 | Fundo de página e painéis |
| `surface/inverse` | gray/800 | #27282C | usar `text/inverse` (14,7:1) | Rodapé, barras escuras |
| `surface/overlay` | alpha/black-60 | #000000 a 60% | — | Sobreposição atrás de modais |
| `table/row/white` | white | #FFFFFF | 14,7:1 | Linha de tabela |
| `table/row/blue` | blue/50 | #EFF3FF | 13,3:1 | Linha alternada de tabela |

## 7. Mapa Figma ↔ código

Proposta, **A DECIDIR** (C-4). O CSS original já usa `--tcece-color-*` com outro significado (`brand-primary-01…`, `sys-*`), então os nomes novos não podem reaproveitar esses.

| Figma | Código (proposta) |
|---|---|
| `text/primary` | `--tcece-color-text-primary` |
| `link/default` | `--tcece-color-link-default` |
| `button/bg/default` | `--tcece-color-button-bg-default` |
| `surface/page` | `--tcece-color-surface-page` |

Regra de conversão: o nome do token Figma com `/` virando `-`, prefixado por `--tcece-color-`.

## 8. Aplicação em produtos

A migração dos tokens antigos para os semânticos e as cores fixas de cada produto ficam no handoff do produto, não aqui. Regra geral: depois de publicar a biblioteca, conferir se os usos migraram e se os valores novos mantêm a tela equilibrada. Tokens `legacy/*` não entram em código novo.

## 9. Fora do escopo desta versão (sem spec ainda)

Bordas (`border/*`), ícones (`icon/*`), status e alertas (`status/*`), foco como tokens além da regra 5, elevação e sombra, tabelas além das linhas, estados de campo (fundo desabilitado), item de menu selecionado, cor de ação genérica (aba ativa, chip). Até haver spec, quem precisar deles deve perguntar ao design em vez de escolher uma primitiva.

## 10. Checklist de revisão

- [ ] Nenhuma cor com hex solto ou primitiva em tela e componente
- [ ] Texto com `text/*`, links com `link/*`, botões com `button/*`, fundos com `surface/*`
- [ ] Pares de texto e fundo com 4,5:1 (3:1 para texto grande e UI)
- [ ] Erro, sucesso e status com ícone e texto, nunca só cor
- [ ] Links em texto corrido sublinhados
- [ ] Foco com `focus/ring` e `focus/border` juntos
- [ ] Texto amarelo não usado (alerta só como preenchimento)
- [ ] Nenhum token `legacy/*` em código novo

## 11. Pontos em aberto

Todos os pontos em aberto de cor estão em **`decisoes-em-aberto.md`** (C-1 a C-7).
