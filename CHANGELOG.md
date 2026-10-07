# Changelog — Design System TCE Ceará

Mais recente primeiro.

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
