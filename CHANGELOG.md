# Changelog — Design System TCE Ceará

Mais recente primeiro.

## ds-v2 — 2026-10-21 (a confirmar; a tag é decisão do design)

**Decisão tomada em 2026-10-27: piso de 16px para qualquer texto**
- Nenhum texto da interface fica abaixo de 16px (1 rem), em nenhum breakpoint. Abaixo de 18px, a hierarquia se faz com peso e cor.
- **Tokens removidos** (sem alias): `title-xs`, `title-ss` e `body-standard`. Troca de uso: `title-xs` e `title-ss` → `title-sm`; `body-standard` → `body-md`.
- **Tokens que subiram para 16px:** `caption` (era 12), `code` (era 14), `form-helper` (era 14), `button-secondary` (era 14). Mobile: `title-sm` passa de 14 para 16.
- Resolve T-7 e T-8. Novo T-14 (`display-*` sem papel definido).
- **Número de destaque (indicador, KPI):** `title-2xl` com Atkinson e `tabular-nums`; texto de apoio em `body-md` `text/secondary`.
- **Chip de identificação ao lado de um nome** (cargo, perfil): `body-md` (16/400) em `text/secondary`; os demais chips e selos seguem em `title-sm`.
- `typography-spec-tce.md`: afirmação errada sobre o Figma corrigida; `--font-display` removido (`display-*` em Noto Sans); `code` explícito em Fira Code; tokens de componente (`--button-*`, `--form-*`, `--table-*`) no CSS; carregamento das fontes; novos papéis no mapa (selo, tooltip, placeholder, código, rótulo do par rótulo–valor); checklist sem os valores de espaçamento (vale a `spacing-spec-tce.md`).
- `padroes-de-interface.md`: badges em `title-sm`; toast em `body-md`; rótulo do par rótulo–valor em `body-md`.
- **Impacto para os devs:** trocar os usos dos tokens removidos e regenerar `tokens.json` e `designTokens.ts`. Telas com chip, selo, helper ou legenda podem crescer em altura para acomodar 16px.

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
