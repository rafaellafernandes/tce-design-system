# Changelog — Design System TCE Ceará

Mais recente primeiro.

## ds-v2 — 2026-10-21 (a confirmar; a tag é decisão do design)

**Decisão tomada: família tipográfica (fecha o T-1)**
- **Noto Sans** passa a ser a fonte principal de toda a interface. **Atkinson Hyperlegible Next** vira fonte de acento e só entra em **números** e **labels** (`form-label`, contadores, identificadores, colunas numéricas, paginação). Antes, a spec mandava Atkinson em toda a interface, e foi isso que fez o código aplicar Atkinson na maior parte do sistema.
- `typography-spec-tce.md`: novo token `--font-accent` (Atkinson) e `--font-primary` agora é Noto Sans; `--font-secondary` removido; nova seção 2.1 (onde a Atkinson entra); coluna "Família" nos tokens de componente; classe `.num`; orientação para `createTheme` do MUI (`fontFamily` em Noto Sans, Atkinson só no label e nos números); regra 3 (não declarar `font-family` à mão) e checklist atualizados.
- `design-system-index.md`: regra 6 e estado da tipografia atualizados.
- `padroes-de-interface.md`: famílias indicadas por padrão (formulários, tabelas, identificadores, paginação, contagem no título).
- `decisoes-em-aberto.md`: T-1 removido; **T-13** incluído (o que mais conta como "label" para a Atkinson).

**Impacto para os devs**
- Quem copiou a família de `--font-primary` ou do tema do MUI precisa revisar: a família principal mudou de Atkinson para Noto Sans. Os usos de Atkinson devem ficar só em labels e números.
- `tokens.json` e `designTokens.ts` precisam ser corrigidos na origem e regenerados (ainda não feito).

## ds-v1 — 2026-10-07

Primeira versão neste repositório, com revisão estrutural das specs.

**Contradições corrigidas**
- A spec de tipografia não repete mais a escala de espaçamento (seção 5) nem as variáveis `--space-*`: a escala vale só pela `spacing-spec-tce.md`.
- Espaço entre parágrafos marcado como A DECIDIR (E-2), em vez de 12px na tipografia e 32px no CSS original.
- O valor 12 da escala passa a ser tratado como "em avaliação" (E-1) em todas as specs.

**Decisão tomada: unidades**
- Figma e specs em **px**; código em **rem** (base 16px, `rem = px ÷ 16`). Tabela de conversão no índice; tipografia e espaçamento mostram px e rem lado a lado; o CSS de tipografia já usa rem. Fecha o E-4 e tira a unidade do N-1.

**Organização**
- Novo `padroes-de-interface.md`, com a seção 7.2 da tipografia (sem mudança de conteúdo).
- Lista de pendências única em `decisoes-em-aberto.md`; as specs apontam para os IDs (T, E, G, C). Novos itens: **C-7** (tokens de borda, status e ícone sem spec) e **N-1** (convenção de nomes no código).
- Conteúdo específico do Conecta saiu das specs (vai para o `conecta-docs`): efeito da mudança de cores, valores dos protótipos, handoff e processo de design com IA.
- `espacamento-e-css-original-correcoes.md` virou arquivo de referência, em `referencias/`.
- Cabeçalho padronizado (status, data e versão) em todas as specs.
