# Design System TCE Ceará — Índice das specs

> **Para o Claude do dev:** leia este arquivo primeiro. Ele diz qual spec consultar para cada tarefa, o que vale para todas e o que ainda está pendente. Se duas specs divergirem, vale a ordem de precedência da seção 4. Itens **A DECIDIR** não devem ser implementados por conta própria: pergunte ao design.

Status: rascunho de 2026-10-05. Revisão estrutural em 2026-10-07 (versão **ds-v1**). Atualizado em 2026-10-21 (família tipográfica decidida). Origem: arquivo Figma ⭐ Design System TCE (fileKey `mn0wkryj2sBHmW412qD2o8`), protótipos existentes e CSS original do TCE. As specs são do design system; a aplicação em cada produto fica em um handoff próprio.

## 1. Mapa das specs

| Spec | Arquivo | Cobre | Coleção / página no Figma | Estado |
|---|---|---|---|---|
| Tipografia | `typography-spec-tce.md` | Famílias (Noto Sans principal; Atkinson só em números e labels), escala única, pesos, espaçamento de texto (line-height, letter-spacing, parágrafos), mapa de papéis, padrões de uso, cores de texto, contraste | Estilos de texto do DS | Em uso, com 6 pendências (T-3, T-4, T-5, T-12, T-13, T-15); família decidida em 2026-10-21; piso de 16px decidido em 2026-10-27; escala única e espaçamento de texto decididos em 2026-10-28 |
| Cor (escopo parcial) | `color-spec-tce.md` | Primitivas e semânticos de texto, link, botão e fundo; contraste; regras de uso | Coleções Color / Primitives e Color / Semantic, página 🎨 Cores | Rascunho parcial |
| Espaçamento | `spacing-spec-tce.md` | Escala 4–48, tokens semânticos, padding de componentes, alvos clicáveis, espaçamento de texto | Coleção Spacing, página Spacing | Rascunho |
| Grid e layout | `grid-layout-spec-tce.md` | Colunas, margem, gutter, menu lateral, templates de página | Coleções Grid e Layout, páginas 📏 Grid e 🧱 Layout | Rascunho |
| Botão | `button-spec-tce.md` | Componente `Button` (MUI): propriedades Figma ↔ props do MUI, medidas, estados (hover, ripple, foco amarelo e preto, desabilitado, selecionado), acessibilidade e referência de tema | Página 🧩 Componentes, conjunto `Button` | Rascunho, 7 pendências (B-1 a B-7) |
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

## 4.1 Estrutura das specs (Atomic Design)

As specs seguem as cinco camadas do Atomic Design. A camada diz **de quem a spec pode depender** e **quem pode depender dela**.

| Camada | Atomic Design | No DS TCE | Specs que existem | Specs que faltam (ordem de criação) |
|---|---|---|---|---|
| **1. Átomos (tokens)** | Cor, tipografia, espaçamento: tokens de design | Fundações | `color-spec-tce.md`, `typography-spec-tce.md`, `spacing-spec-tce.md`, tokens de `grid-layout-spec-tce.md` | Elevação e sombra, raio e borda, movimento, iconografia |
| **1. Átomos (componentes)** | button, input, label, icon, heading, image | Componentes indivisíveis | `button-spec-tce.md` | Campos (input, select, checkbox, radio, switch) e label, link, selo e chip, ícone, tooltip, contador, indicador de progresso |
| **2. Moléculas** | Grupos de átomos: campo de busca, form de login, card de produto | Átomos juntos com uma função | Parte de `padroes-de-interface.md` (formulários, paginação, abas, feedback) | Campo de busca, campo de formulário (label + input + helper + erro), chip de filtro, breadcrumb, paginação, item de menu, banner e snackbar, dropdown |
| **3. Organismos** | Seções independentes: header, sidebar, footer, grid de cards | Seções completas da interface | Parte de `padroes-de-interface.md` (cabeçalho de página, tabelas, modais) e menu lateral em `grid-layout-spec-tce.md` | Header, menu lateral, tabela, modal, cards (métrica e indicador), filtros de busca |
| **4. Templates** | Estrutura da página sem conteúdo real | Wireframe com componentes reais, define layout e hierarquia | Templates de página em `grid-layout-spec-tce.md` | Templates de listagem, detalhe e formulário |
| **5. Páginas** | Templates com conteúdo real; onde se testa texto longo, imagens, erros e estados vazios | Produto final | Handoff de cada produto (fora deste repositório) | Não é spec do DS |

Specs que misturam camadas (`padroes-de-interface.md`, `grid-layout-spec-tce.md`) declaram a camada principal e listam as partes de cada camada. Ao detalhar um componente, a parte sai para uma spec própria.

### Regras

1. **A dependência só desce.** Uma spec depende de specs da mesma camada ou de camadas abaixo (organismo usa molécula, molécula usa átomo). Átomo nunca depende de molécula ou organismo; o que a camada de cima define sobre ele (por exemplo, a ordem dos botões em um modal) fica na spec de cima.
2. **Não repita valor de fundação.** Referencie a spec de tokens. Se o valor ainda não tem spec, registre como provisório em `decisoes-em-aberto.md` (B-7 para o botão).
3. **Ordem de criação:** tokens, átomos, moléculas, organismos, templates. Antes de criar uma spec, confira se as de que ela depende existem; se faltar, crie a de baixo primeiro ou registre a pendência.
4. **Referência nos dois sentidos.** Quem usa lista de quem depende (com a data lida); quem é usado lista quem usa. Ao uma spec de cima passar a usar uma de baixo, atualize "Usada por" na de baixo.
5. **Mudança em spec de baixo** exige revisar todas as listadas em "Usada por", com nova versão e data em cada uma.

### Cabeçalho padrão de toda spec

| Campo | Valor |
|---|---|
| Versão da spec | `x.y.z` e estado (rascunho ou em uso) |
| Última atualização | `AAAA-MM-DD` |
| Versão do DS | Tag do DS que a considera (ou "em revisão, ainda sem tag") |
| Camada | Uma das cinco acima, e se é token ou componente |
| Depende de | Specs de camadas iguais ou abaixo, cada uma com a data lida |
| Usada por | Specs de camadas acima que a usam |
| Arquivo e Figma | Caminho do arquivo e página, conjunto ou coleção no Figma |

Modelo: `button-spec-tce.md`. As demais specs ainda têm só data e status e entram em um PR à parte.

## 5. Convenções comuns

- **Formato das specs:** regras obrigatórias, tokens, como escolher, componentes, responsivo, mapa Figma ↔ código, checklist, pontos em aberto.
- **Nomes no código:** proposta `--tcece-space-*`, `--tcece-grid-*`, `--tcece-layout-*`. Unificar a convenção de nomes está pendente (N-1 em `decisoes-em-aberto.md`).
- **Prefixo `tcece` (decidido em 2026-10-28):** tudo o que o DS inventa leva o prefixo `tcece`: variáveis CSS (`--tcece-*`), variantes customizadas (`tceceElevated`), chaves do tema (`theme.tcece`), classes (`.tcece-*`) e propriedades só do Figma (`tceceDevice`, `tceceSelected`). Nomes que espelham o MUI (`variant`, `color`, `startIcon`, `focusVisible`…) ficam sem prefixo, e **nada nosso usa palavras reservadas do MUI** (`Mui*`, `--mui-*`, `.Mui-*`, props como `size` e `selected` com outro significado). Detalhe em `button-spec-tce.md`, seção 2.1.
- **Unidade:** as specs e o Figma usam **px**; o código usa **rem**, com base de 16px (definida em `reset.css`). Converta sempre por `rem = px ÷ 16`. Cada tabela de tokens mostra os dois valores. Não use px para tamanho de fonte, espaçamento nem tamanho de alvo no código: o rem respeita a preferência de tamanho de fonte da pessoa (WCAG 1.4.4).
- **Figma:** cada spec corresponde a uma coleção de variáveis ou a uma página. Os modos de uma coleção são os breakpoints.
- **Versionamento:** cada spec traz no topo a **versão da spec**, a **data da última atualização** e a versão do DS (modelo: `button-spec-tce.md`; as demais specs ainda têm só data e status), e termina com um histórico de versões; quem lê registra versão e data no PR ou no handoff; cada alteração entra no `CHANGELOG.md` do repositório; conjuntos fechados recebem tag `ds-vN`. Os handoffs dos produtos registram a versão do DS que usam.

### Tabela de conversão (px → rem)

| px | 4 | 8 | 12 | 14 | 16 | 18 | 20 | 24 | 32 | 40 | 44 | 48 | 80 | 112 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| rem | 0,25 | 0,5 | 0,75 | 0,875 | 1 | 1,125 | 1,25 | 1,5 | 2 | 2,5 | 2,75 | 3 | 5 | 7 |

Unitless fica unitless: `line-height` (1,2; 1,4; 1,6) e pesos. Letter-spacing e word-spacing (hoje `0`) ficam em `em`. Larguras de breakpoint (media query) ficam em px até a decisão G-1. O menu lateral (255 px) converte para 15,9375 rem.

## 6. Publicação e Code Connect

- Variáveis, grid styles e componentes criados no Figma só ficam disponíveis nos protótipos depois que a biblioteca for publicada.
- Code Connect ainda não está mapeado para nenhum componente de grid ou layout.
- Em 2026-10-05, as variáveis `layout/columns`, `layout/margin` e `layout/gutter` foram renomeadas para `grid/*`. Protótipos que consumiam os nomes antigos precisam ser reapontados após a publicação.

## 6.1 Documentação das bibliotecas (Context7)

O front usa o MUI (`@mui/material`). Para o agente de código não implementar com a API de outra versão do MUI, ele consulta a documentação **da versão que o projeto usa** pelo **Context7** (https://context7.com, da Upstash), que serve documentação atualizada e por versão a agentes de IA.

- **Instalação** (por quem desenvolve; não faz parte do design): no Claude Code, `/plugin install context7@claude-plugins-official`, ou o servidor MCP `https://mcp.context7.com/mcp`, ou `npx ctx7 setup`. A chave de API pode ser necessária; veja https://context7.com/docs/installation.
- **Quando consultar:** ao implementar um componente com o MUI (props, `styleOverrides`, `variants`, classes `Mui-*`, `createTheme`). Procure a biblioteca pelo nome e **use a versão do `package.json` do front**; não assuma o identificador nem a versão.
- **Quando não consultar:** para decisões do design system (tokens, estados, medidas, nomes). Elas vêm só das specs deste repositório.
- **Precedência:** a spec do DS vence a documentação do MUI no que for decisão do DS (por exemplo, hover, ripple e foco do botão). A documentação do MUI vence a memória do agente no que for API do MUI. Se uma spec depender de uma API que a versão do MUI não tem, registre a divergência em `decisoes-em-aberto.md` em vez de contornar.
- **Versão do MUI do front (decidida em 2026-10-28):** `@mui/material` **9.1.1** (também `@mui/icons-material` e `@mui/system` em 9.1.1; `@emotion/react` ^11.14.0; `@emotion/styled` ^11.14.1). Na v9, chaves de `styleOverrides` como `containedPrimary` e `textPrimary` foram removidas (use `variants`), `GridLegacy` foi removido e o `Button` tem a prop `nativeButton`.

## 7. Governança

### Verificação das specs relacionadas (sempre que uma spec mudar)

Toda atualização de spec inclui conferir as specs relacionadas, nas duas direções:

1. Abra os campos **Depende de** e **Usada por** da spec alterada.
2. **Para cima e para baixo:** em cada spec listada, confira se os valores e as referências ainda batem com a mudança. Se a spec de baixo (da qual ela depende) mudou depois da "data lida", revise e atualize a data lida.
3. Atualize os campos **Usada por** e **Depende de** das duas pontas, se a relação mudou.
4. Em **cada spec tocada**: nova versão, nova data e linha no histórico de versões.
5. Registre no `CHANGELOG.md` e, se a mudança resolver ou abrir pendência, em `decisoes-em-aberto.md`.
6. No PR, liste as specs verificadas, **inclusive as que não precisaram mudar**, com a data lida de cada uma. PR sem essa lista não está pronto para mesclar.

- O time de design do design system aprova valores novos e resolve as decisões em aberto.
- Cada decisão tomada atualiza a spec de origem e sai de `decisoes-em-aberto.md`.
