# Design System TCE Ceará — Índice das specs

> **Para o Claude do dev:** leia este arquivo primeiro. Ele diz qual spec consultar para cada tarefa, o que vale para todas e o que ainda está pendente. Se duas specs divergirem, vale a ordem de precedência da seção 4. Itens **A DECIDIR** não devem ser implementados por conta própria: pergunte ao design.

Status: rascunho de 2026-10-05. Revisão estrutural em 2026-10-07 (versão **ds-v1**). Atualizado em 2026-10-21 (família tipográfica decidida). Origem: arquivo Figma ⭐ Design System TCE (fileKey `mn0wkryj2sBHmW412qD2o8`), protótipos existentes e CSS original do TCE. As specs são do design system; a aplicação em cada produto fica em um handoff próprio.

## 1. Mapa das specs

| Spec | Arquivo | Cobre | Coleção / página no Figma | Estado |
|---|---|---|---|---|
| Tipografia | `typography-spec-tce.md` | Famílias (Noto Sans principal; Atkinson só em números e labels), escala única, pesos, espaçamento de texto (line-height, letter-spacing, parágrafos), mapa de papéis, padrões de uso, cores de texto, contraste | Estilos de texto do DS | Em uso, com 10 pendências (T-3 a T-6, T-9 a T-14); família decidida em 2026-10-21; piso de 16px decidido em 2026-10-27; escala única e espaçamento de texto decididos em 2026-10-28 |
| Cor (escopo parcial) | `color-spec-tce.md` | Primitivas e semânticos de texto, link, botão e fundo; contraste; regras de uso | Coleções Color / Primitives e Color / Semantic, página 🎨 Cores | Rascunho parcial |
| Espaçamento | `spacing-spec-tce.md` | Escala 4–48, tokens semânticos, padding de componentes, alvos clicáveis, espaçamento de texto | Coleção Spacing, página Spacing | Rascunho |
| Grid e layout | `grid-layout-spec-tce.md` | Colunas, margem, gutter, menu lateral, templates de página | Coleções Grid e Layout, páginas 📏 Grid e 🧱 Layout | Rascunho |
| Botão | `button-spec-tce.md` | Componente `Button` (MUI): propriedades Figma ↔ props do MUI, medidas, estados (hover, ripple, foco amarelo e preto, desabilitado, selecionado), acessibilidade e referência de tema | Página 🧩 Componentes, conjunto `Button` | Rascunho, 6 pendências (B-1 a B-6) |
| Padrões de interface | `padroes-de-interface.md` | Blocos recorrentes das telas: cabeçalho, seções, abas, tabelas, formulários, modais, feedback, status, estado vazio, texto longo | — | Rascunho |
| Decisões em aberto | `decisoes-em-aberto.md` | Todos os "A DECIDIR" consolidados, com spec de origem | — | Em andamento |
| Correções do CSS original | `../referencias/espacamento-e-css-original-correcoes.md` | Defeitos do CSS legado e comparação com o Figma | — | Referência (arquivo, não spec viva) |

A spec de cor cobre só texto, link, botão e fundo; bordas, ícones e status ainda não têm spec. As specs são **do design system**, sem referência a um produto. O que for específico de um produto vai para o handoff dele. Ainda não existem specs de elevação, ícones e componentes individuais além do botão (modal, card, tabela). Quando surgirem, entram neste mapa.

## 2. Qual spec consultar

| Tarefa | Leia |
|---|---|
| Handoff de um produto | O handoff do produto (fora deste repositório), que remete às specs |
| Cor de texto, link, botão ou fundo | `color-spec-tce.md` |
| Qualquer tela nova | Este índice, depois tipografia (seção 4, mapa de papéis) e espaçamento (seção 3, como escolher o token) |
| Botão, ação, link com aparência de botão | `button-spec-tce.md` |
| Formulário | Padrões de interface (formulários) + espaçamento (label → campo 8, campo → campo 16) |
| Tabela, listagem | Padrões de interface (tabelas) + grid-layout (colunas) |
| Página com menu lateral | Grid-layout (seção 4) |
| Modal, card | Padrões de interface + espaçamento (seção 4, componentes); padding de card é decisão pendente |
| Responsivo | Grid-layout (seção 7) + tipografia (tokens mobile) |

## 3. Regras que valem para todas as specs

1. **Nunca use valor solto** de fonte, peso, line-height, cor, espaçamento, margem ou gutter. Use sempre o token.
2. **Escolha o token pelo papel**, não pelo valor que parece certo.
3. **Valor novo só com aprovação do design system.** Se nenhum token serve, pergunte.
4. **Alvo clicável: 44px no desktop e 48px no mobile** (NBR 17225).
5. **Cor nunca é o único indicador** de erro, sucesso ou status (WCAG).
6. **Família tipográfica:** Noto Sans em toda a interface; Atkinson Hyperlegible Next só em números e labels (ver `typography-spec-tce.md`, seção 2.1). **Não copie line-height nem letter-spacing de frames antigos do Figma**; siga os tokens da spec (letter-spacing `0`, line-height do token).
7. **O que está marcado A DECIDIR não se implementa.** Registre a dúvida e pergunte.
8. Mudança de valor de um token existente exige aviso aos devs e lista dos usos afetados.

## 4. Precedência quando duas specs divergem

1. Spec do assunto vence a spec de outro assunto. Espaçamento e grid são decididos nas specs de espaçamento e de grid-layout; tipografia, na de tipografia.
2. A spec de tipografia **não repete** a escala de espaçamento: todo valor de espaçamento vale pela `spacing-spec-tce.md`. O espaçamento **de texto** (entrelinha, letter-spacing, word-spacing, parágrafos) está só na spec de tipografia, seção 5.
3. Entre Figma e spec, vale a spec, exceto onde o item estiver em `decisoes-em-aberto.md`: aí vale o que o design decidir.
4. O CSS original do TCE é referência de valores, não de regras; seus defeitos conhecidos estão em `espacamento-e-css-original-correcoes.md`.

## 5. Convenções comuns

- **Formato das specs:** regras obrigatórias, tokens, como escolher, componentes, responsivo, mapa Figma ↔ código, checklist, pontos em aberto.
- **Nomes no código:** proposta `--tcece-space-*`, `--tcece-grid-*`, `--tcece-layout-*`. Unificar a convenção de nomes está pendente (N-1 em `decisoes-em-aberto.md`).
- **Prefixo `tcece` (decidido em 2026-10-28):** tudo o que o DS inventa leva o prefixo `tcece`: variáveis CSS (`--tcece-*`), variantes customizadas (`tceceElevated`), chaves do tema (`theme.tcece`), classes (`.tcece-*`) e propriedades só do Figma (`tceceDevice`, `tceceSelected`). Nomes que espelham o MUI (`variant`, `color`, `startIcon`, `focusVisible`…) ficam sem prefixo, e **nada nosso usa palavras reservadas do MUI** (`Mui*`, `--mui-*`, `.Mui-*`, props como `size` e `selected` com outro significado). Detalhe em `button-spec-tce.md`, seção 2.1.
- **Unidade:** as specs e o Figma usam **px**; o código usa **rem**, com base de 16px (definida em `reset.css`). Converta sempre por `rem = px ÷ 16`. Cada tabela de tokens mostra os dois valores. Não use px para tamanho de fonte, espaçamento nem tamanho de alvo no código: o rem respeita a preferência de tamanho de fonte da pessoa (WCAG 1.4.4).
- **Figma:** cada spec corresponde a uma coleção de variáveis ou a uma página. Os modos de uma coleção são os breakpoints.
- **Versionamento:** data, status e versão do DS no topo de cada spec; cada alteração entra no `CHANGELOG.md` do repositório; conjuntos fechados recebem tag `ds-vN`. Os handoffs dos produtos registram a versão do DS que usam.

### Tabela de conversão (px → rem)

| px | 4 | 8 | 12 | 14 | 16 | 18 | 20 | 24 | 32 | 40 | 44 | 48 | 80 | 112 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| rem | 0,25 | 0,5 | 0,75 | 0,875 | 1 | 1,125 | 1,25 | 1,5 | 2 | 2,5 | 2,75 | 3 | 5 | 7 |

Unitless fica unitless: `line-height` (1,2; 1,4; 1,6) e pesos. Letter-spacing e word-spacing (hoje `0`) ficam em `em`. Larguras de breakpoint (media query) ficam em px até a decisão G-1. O menu lateral (255 px) converte para 15,9375 rem.

## 6. Publicação e Code Connect

- Variáveis, grid styles e componentes criados no Figma só ficam disponíveis nos protótipos depois que a biblioteca for publicada.
- Code Connect ainda não está mapeado para nenhum componente de grid ou layout.
- Em 2026-10-05, as variáveis `layout/columns`, `layout/margin` e `layout/gutter` foram renomeadas para `grid/*`. Protótipos que consumiam os nomes antigos precisam ser reapontados após a publicação.

## 7. Governança

- O time de design do design system aprova valores novos e resolve as decisões em aberto.
- Cada decisão tomada atualiza a spec de origem e sai de `decisoes-em-aberto.md`.
