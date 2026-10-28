# Spec de Cor — Design System TCE Ceará (RASCUNHO, escopo parcial)

> **Para o Claude do dev:** este arquivo é a fonte de verdade para as cores de **texto, links, botões e fundos/superfícies**. Os valores vêm das coleções **Color / Primitives** e **Color / Semantic** do arquivo ⭐ Design System TCE (página 🎨 Cores). Bordas, ícones, status/alertas, tabelas e o legado ainda não têm spec (seção 9). Itens **A DECIDIR** não se implementam sem resposta do design.
>
> Índice geral: `design-system-index.md`. Tipografia: `typography-spec-tce.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **2.0.0** (rascunho, escopo parcial) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **1. Átomos (tokens)** |
| **Depende de** | Nenhuma (é a base). Referência externa: paleta do MUI (`theme.palette`) |
| **Usada por** | `typography-spec-tce.md` (cores de texto), `button-spec-tce.md`, `padroes-de-interface.md` e todas as specs de componente |
| Arquivo e Figma | `specs/color-spec-tce.md`; coleções Color / Primitives, Color / Semantic, Focus e Cor / Ícone do ⭐ Design System TCE |

Histórico na seção 12. Formato do cabeçalho: `design-system-index.md`, seção 4.1.

## 1. Regras obrigatórias

1. **Use sempre o token semântico** (`text/primary`, `primary/main`…). Nunca use a primitiva (`grey/800`), o hex solto ou uma cor copiada do Figma.
2. **Escolha o token pelo papel**, não pela cor que parece certa.
3. **Cor nunca é o único indicador** de erro, sucesso, status ou link: acompanhe de ícone e texto, e sublinhe links em texto corrido (WCAG 1.4.1).
4. **Contraste mínimo:** 4,5:1 para texto normal e 3:1 para texto grande e para componentes de UI e ícones que carregam informação (WCAG 1.4.3 e 1.4.11). Texto desabilitado é isento.
5. **Foco visível:** sempre o anel amarelo (`tcece/focus/ring`) com o contorno preto (`tcece/focus/border`) juntos. O amarelo sozinho dá 1,35:1 sobre branco.
6. **Se nenhum token serve, pergunte ao design.** Não crie cor nova.
7. Ao terminar uma tela, rode o checklist da seção 10.

## 2. Nomes: MUI e específicos do TCE

Os tokens seguem o caminho da paleta do MUI onde o papel existe (`primary/main`, `error/main`, `text/primary`, `background/paper`, `divider`, `action/disabled`…). Assim o nome no Figma é o mesmo do `theme.palette` e o handoff é cópia direta. O que o MUI não tem leva o prefixo `tcece/` (`tcece/focus/bg`, `tcece/link/default`, `tcece/primary/pressed`…). Escalas (primitivas): `grey` (grafia do MUI), `blue`, `red`, `green`, `yellow` e `purple`.

## 2.1 Arquitetura

- **Color / Primitives:** escalas 50–900 de grey, blue, green, red e yellow, mais white, black, purple/700 e alpha/black-60. Sem significado de uso; ocultas nos seletores do Figma. **Não use em telas nem em componentes.**
- **Color / Semantic:** dá o papel e aponta para uma primitiva. Um modo (Light). Se uma escala mudar, tudo que usa o token muda junto.
- **Collection Focus:** `tcece/focus/ring` e `tcece/focus/border`.
- **Legado:** `legacy/Gray/*`, `legacy/Blue/*` e `legacy/Green/*` são aliases obsoletos, mantidos só para não quebrar usos antigos. **Não use em código novo.**

## 3. Texto

Contraste calculado sobre o fundo indicado.

| Token | Primitiva | Hex | Contraste | Uso |
|---|---|---|---|---|
| `text/primary` | grey/800 | #27282C | 14,7:1 sobre branco | Texto principal: títulos, corpo, valores |
| `text/secondary` | grey/700 | #474C52 | 8,7:1 sobre branco | Apoio: descrições, ajuda, breadcrumb, rótulos secundários |
| `tcece/text/placeholder` | grey/700 | #474C52 | 8,7:1 sobre branco | Placeholder, em itálico. Nunca substitui o label |
| `text/disabled` | grey/600 | #73787E | 4,45:1 (isento) | Texto desabilitado |
| `tcece/text/inverse` | white | #FFFFFF | 14,7:1 sobre `tcece/background/inverse` | Texto sobre fundo escuro |
| `tcece/text/error` | red/700 | #A31D24 | 7,6:1 sobre branco | Mensagem de erro, com ícone |
| `tcece/text/success` | green/800 | #206442 | 7,1:1 sobre branco | Mensagem de sucesso, com ícone |
| `tcece/text/info` | blue/700 | #3855A3 | 7,0:1 sobre branco | Mensagem informativa |
| `tcece/text/on-warning` | grey/900 | #1C1D1F | 9,1:1 sobre `warning/main` | Texto sobre o preenchimento amarelo de alerta |

- O amarelo de alerta **nunca** é cor de texto (1,9:1 sobre branco).
- Sobre `background/default` (#F7F8FA) os pares continuam acima de 4,5:1: `text/primary` 13,9:1, `text/secondary` 8,2:1, `tcece/text/error` 7,2:1, `tcece/text/success` 6,7:1, `tcece/link/default` 6,6:1.
- Sobre `tcece/table/row/blue`: `text/primary` 13,3:1 e `tcece/link/default` 6,3:1.
- O mapa de qual token de texto usar por elemento (título, label, helper, tabela…) está em `typography-spec-tce.md`, seção 4.

## 4. Links

| Token | Primitiva | Hex | Contraste sobre branco | Uso |
|---|---|---|---|---|
| `tcece/link/default` | blue/700 | #3855A3 | 7,0:1 | Link. Sempre sublinhado em texto corrido |
| `tcece/link/visited` | purple/700 | #551A8B | 11,0:1 | Link visitado |
| `tcece/link/hover` | blue/800 | #2C417A | 9,8:1 | Link em hover |
| `tcece/link/disabled` | grey/600 | #73787E | 4,45:1 (isento) | Link desabilitado |

Link em foco usa o padrão de foco da regra 5.

## 5. Botões

> Uso no componente (variantes, estados, ripple e foco): `button-spec-tce.md`. Esta seção é a fonte dos tokens; se um token `primary/*`, `tcece/button/*` ou `tcece/focus/*` mudar, revise aquela spec.

| Estado | Fundo | Rótulo | Contraste | Observação |
|---|---|---|---|---|
| Primário | `primary/main` (blue/700) | `primary/contrastText` (white) | 7,0:1 | Ação principal |
| Primário em hover | `primary/dark` (blue/800) | `tcece/button/label/hover-dark` (white) | 9,8:1 | |
| Pressionado | `tcece/primary/pressed` (blue/900) | `primary/contrastText` (white) | 13,1:1 | `tcece/button/bg/active` tem o mesmo valor (unificar, ver C-3) |
| Secundário em hover | `tcece/button/bg/hover-light` (blue/100) | `tcece/button/label/hover-light` (blue/800) | 7,9:1 | Também terciário |
| Desabilitado | `action/disabledBackground` (grey/100) | `action/disabled` (grey/700) | 7,3:1 | Isento de contraste |
| Foco | `tcece/focus/bg` (yellow/300) | `tcece/focus/label` (black) | 15,6:1 | Sempre com contorno `tcece/focus/border` |

- Botão secundário em repouso: fundo `tcece/button/bg/white` com contorno `primary/main`.
- `primary/main` contra o branco dá 7,0:1, então passa 3:1 como componente de UI.
- `action/disabledBackground` contra o branco dá 1,2:1: isento por ser desabilitado, mas o estado precisa ser comunicado também pelo atributo `disabled`/`aria-disabled`.

## 6. Fundos e superfícies

| Token | Primitiva | Hex | `text/primary` sobre ele | Uso |
|---|---|---|---|---|
| `background/paper` | white | #FFFFFF | 14,7:1 | Cards, campos, modais |
| `background/default` | grey/50 | #F7F8FA | 13,9:1 | Fundo de página e painéis |
| `tcece/background/inverse` | grey/800 | #27282C | usar `tcece/text/inverse` (14,7:1) | Rodapé, barras escuras |
| `tcece/overlay` | alpha/black-60 | #000000 a 60% | — | Sobreposição atrás de modais |
| `tcece/table/row/white` | white | #FFFFFF | 14,7:1 | Linha de tabela |
| `tcece/table/row/blue` | blue/50 | #EFF3FF | 13,3:1 | Linha alternada de tabela |

## 7. Mapa Figma ↔ código

A sintaxe de código WEB já está preenchida em cada variável do Figma.

| Figma | Código |
|---|---|
| Tokens com nome do MUI (`primary/main`, `error/main`, `text/primary`, `background/paper`, `divider`, `action/disabled`…) | `theme.palette.<caminho com ponto>`, por exemplo `theme.palette.primary.main` |
| Tokens `tcece/…` (`tcece/focus/bg`, `tcece/link/default`…) | `--tcece-color-<caminho com hífen>`, por exemplo `--tcece-color-focus-bg`; no tema, em `theme.palette.tcece` |
| Primitivas `grey/500`, `blue/700`… | `theme.palette.grey[500]` para `grey`; `--tcece-color-blue-700` para as demais |

O CSS original já usa `--tcece-color-*` com outro significado (`brand-primary-01…`, `sys-*`). Os nomes novos têm o caminho completo, então não colidem; conferir na migração (C-4).

**Não deixe o `createTheme` derivar:** `primary/dark` (hover) e `tcece/primary/pressed` são valores do DS. No tema, defina `primary.main`, `primary.dark` e `primary.contrastText` explicitamente.

## 8. Aplicação em produtos

A migração dos tokens antigos para os semânticos e as cores fixas de cada produto ficam no handoff do produto, não aqui. Regra geral: depois de publicar a biblioteca, conferir se os usos migraram e se os valores novos mantêm a tela equilibrada. Tokens `legacy/*` não entram em código novo.

## 9. Fora do escopo desta versão (sem spec ainda)

Bordas (`divider`, `tcece/border/*`), ícones (`tcece/icon/*`), status e alertas (`*/main`, `tcece/*/subtle`), foco como tokens além da regra 5, elevação e sombra, tabelas além das linhas, estados de campo (fundo desabilitado), item de menu selecionado, cor de ação genérica (aba ativa, chip). Até haver spec, quem precisar deles deve perguntar ao design em vez de escolher uma primitiva.

## 10. Checklist de revisão

- [ ] Nenhuma cor com hex solto ou primitiva em tela e componente
- [ ] Texto com `text/*` ou `tcece/text/*`, links com `tcece/link/*`, botões com `primary/*` e `tcece/button/*`, fundos com `background/*`
- [ ] Pares de texto e fundo com 4,5:1 (3:1 para texto grande e UI)
- [ ] Erro, sucesso e status com ícone e texto, nunca só cor
- [ ] Links em texto corrido sublinhados
- [ ] Foco com `tcece/focus/ring` e `tcece/focus/border` juntos
- [ ] Texto amarelo não usado (alerta só como preenchimento)
- [ ] Nenhum token `legacy/*` em código novo

## 11. Pontos em aberto

Todos os pontos em aberto de cor estão em **`decisoes-em-aberto.md`** (C-1 a C-7).

## 12. Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 2.0.0 | 2026-10-28 | Nomes dos tokens alinhados ao MUI (`primary/main`, `error/main`, `background/paper`…); específicos do TCE com prefixo `tcece/`; `gray` → `grey`; sintaxe de código WEB preenchida; cabeçalho padrão; seção 7 (mapa) definida. **Quebra de nome** |
| 1.0.0 | 2026-10-07 | Revisão estrutural (`ds-v1`) sobre o rascunho de 2026-10-05 |
