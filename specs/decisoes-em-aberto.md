# Decisões em aberto — Design System TCE Ceará

> **Para o Claude do dev:** tudo o que está aqui **não foi decidido**. Não implemente nenhum desses pontos por conta própria; use a coluna "Enquanto isso" e pergunte ao design se precisar de mais. Cada decisão tomada atualiza a spec de origem e sai desta lista.

Status: consolidado em 2026-10-05; **lista única** de pendências do DS desde 2026-10-07 (as specs apontam para os IDs daqui). Revisão estrutural em 2026-10-07 (versão **ds-v1**). Atualizado em 2026-10-21: T-1 decidido e removido; T-13 incluído. Atualizado em 2026-10-27: piso de 16px decidido; T-7 e T-8 removidos; T-14 incluído (número de destaque decidido: `title-2xl`). Índice geral: `design-system-index.md`.

Legenda de impacto: **Bloqueante** = o dev não deve fechar a padronização sem a decisão. **Importante** = muda valor ou nome usado em várias telas. **Menor** = afeta poucos casos.

## Tipografia (`typography-spec-tce.md`)

Decidido em 2026-10-21 (sai da lista): **T-1, família tipográfica.** A fonte principal é Noto Sans; Atkinson Hyperlegible Next só em números e labels.

Decidido em 2026-10-28 (sai da lista), segunda rodada:
- **T-6** título de modal e de página: `title-lg` (24).
- **T-9** line-height dos títulos: o do token.
- **T-10** ponto de quebra mobile: 768px (o conflito com o grid segue em G-1).
- **T-11** negrito em texto corrido: 600.
- **T-14** `display-*`: papel e escala definidos (seção 3 e 3.1 da tipografia): `display-2xl` (80/44) e `display-xl` (64/40) novos, ambos peso 700; um `display-*` por página, só em hero e páginas institucionais. O letter-spacing do hero ficou para **T-16**.
- **T-15** mapeamento para o MUI: variantes com o nome do MUI e o prefixo `tcece` (`tceceH1`, `tceceBody1`, `tceceButton`, `tceceCaption`…). Os níveis de cada uma estão na tipografia, seção 12 (ainda a confirmar com o front).
- **C-5 (foco)**: botão com preenchimento amarelo, texto preto e borda inferior preta de 4px; links, campos e os demais com anel amarelo e contorno preto.
- **Tokens de cor mais próximos do MUI:** `tcece/text/error`, `tcece/text/success`, `tcece/text/info`, `tcece/action/create`, `tcece/link/default` e `tcece/link/hover` passaram a ser alias de `error/main`, `success/main`, `info/main`, `success/main`, `primary/main` e `primary/dark`. No código use o token do MUI. Os alias saem quando os usos migrarem.
- **B-8** versão do MUI do front: **9.1.1** (`@mui/material`, `@mui/icons-material` e `@mui/system` em 9.1.1; `@emotion/react` ^11.14.0; `@emotion/styled` ^11.14.1), informada em 2026-10-28.

Decidido em 2026-10-28 (sai da lista): **escala tipográfica única e espaçamento de texto.** Resolve **T-2** (line-height: valores do token, 1.2 / 1.4 / 1.6 / 1.8; 1,5 só como teste de aceitação) e **E-2** (letter-spacing `0`, word-spacing `0`, parágrafo 24px; o texto deve aguentar os valores da WCAG 1.4.12 sem corte). Os tokens de componente `button-*`, `form-*` e `table-*` foram removidos: usam `title-sm`, `body-md` e `caption`. Ver `typography-spec-tce.md`, seções 3 a 5.

Decidido em 2026-10-27 (sai da lista): **piso de 16px para qualquer texto.** Resolve **T-7** (`title-sm` mobile = 16) e **T-8** (`form-helper` = 16). Os tokens `title-xs`, `title-ss` e `body-standard` foram removidos; `caption`, `code`, `form-helper` e `button-secondary` passaram a 16px.

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| T-3 | Peso | 600 como único peso de ênfase; botões em 600 ou Regular | Tokens (600) | Importante | Usar 600 |
| T-4 | Tamanho 18px | Criar tokens `title` e `button` de 18 ou padronizar em 16/20 | Sem token | Importante | Não usar 18px fora de `body-lg` |
| T-5 | Número da ocorrência em título | Token `title-lg-regular` ou peso 600 do título | Peso do título | Menor | `title-lg` com o peso do título (família do título: Noto Sans, ver T-13) |
| T-15 | Quais níveis do MUI recebem cada token (`tceceH1`–`tceceH4`, `tceceBody1`, `tceceBodyLg`…) | Ver tipografia, seção 12 | `tceceH1` = `title-2xl` … `tceceH4` = `title-sm`; `tceceBody1` = `body-md`; `tceceButton` = `title-sm`; `tceceCaption` = `caption` | Menor | Usar o mapa da seção 12; confirmar com o front |
| T-16 | Revisar o letter-spacing (e o word-spacing) de todo o DS | Hoje é `0` em todos os tokens (decidido em 2026-10-28), mas o hero do Conecta usa espaçamento largo, o CSS original usava 0,08 a 0,12 em e os estilos antigos do Figma 4 a 12%. Rever token a token: `display-*`, títulos, labels, botão, números, `caption` | A decidir | Importante | `0`, como na tipografia, seção 5 |
| T-12 | Cores de texto | Resolvido em parte por `color-spec-tce.md` (abas inativas em `text/secondary`, placeholder em `tcece/text/placeholder`, texto verde com 7,1:1); resta o alerta amarelo (C-2) | Resolvido em parte | Menor | Usar os tokens de cor |
| T-13 | O que conta como "label" para a Atkinson (além do label de formulário) | Incluir ou não: cabeçalho de tabela, abas e itens de menu, badges de status, rótulo de par rótulo–valor, labels de checkbox/radio, `caption` | Só o label de formulário e números; o resto em Noto Sans | Importante | Atkinson só no label de formulário e em números (typography-spec, seção 2.1); perguntar antes de ampliar |

## Espaçamento (`spacing-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| E-1 | `spacing/12` | Manter ou remover (o CSS original não usa) | Em avaliação | Menor | Evitar 12 em tela nova |
| E-3 | `card-padding` | 16 (spec) ou 24 (uso atual em protótipos) | Token em 16 | Importante | Perguntar |
| E-5 | Prefixo e nomes dos tokens de espaçamento | `--tcece-space-*` ou `--space-*`; alinhar com nomes de tipografia (`title-desk-md` no CSS, `title-md` na spec) | `--tcece-space-*` | Importante | `--tcece-space-*` |
| E-6 | Padding vertical do chip | 3 está fora da escala | — | Menor | Perguntar |
| E-7 | Espaço mínimo entre alvos clicáveis | O CSS usa margem de 4 | — | Menor | 4 |

## Botão (`button-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| B-1 | Combinações de `variant` e `color` | Só as 5 que existem no Figma, ou criar `outlined`/`text` com `success` | Só as 5 existentes | Menor | Não usar outras combinações |
| B-2 | Cor do botão de criação (`contained` + `success`) | Hoje verde fixo (#216342; hover #2B7D54; pressed = repouso), sem token semântico. O hover **clareia** e o do primário **escurece** | Criar tokens `button/bg/create-*` e padronizar hover e pressed | Importante | Usar os valores do Figma; perguntar |
| B-3 | Estado `selected` (antes `Active`) | Fica no `Button` como estilo do tema, ou vai para o componente de item de menu | Item de menu | Importante | Aplicar só no menu lateral |
| B-4 | Visual de `disabled` nos `outlined`, `elevated` e `text` | Manter fundo e contorno ou só trocar a cor do rótulo | Fundo `action/disabledBackground` e rótulo `action/disabled` | Menor | Conferir no Figma (`state=disabled`) |
| B-5 | Botão só com ícone | `IconButton` com spec própria (hoje existe `Btn_icon_primary` no Figma, fora desta spec) | Spec própria | Importante | Perguntar |
| B-6 | Code Connect do `Button` | Mapear o componente do Figma ao `Button` do MUI | Mapear depois que os nomes estabilizarem | Menor | Handoff descreve as props da seção 2 |
| B-7 | Specs de fundação que o botão usa e ainda não existem | Criar specs de elevação e sombra, ícones, raio e borda, movimento (ripple e movimento reduzido) | Valores provisórios na `button-spec-tce.md` | Importante | Usar os valores da spec do botão; perguntar antes de reutilizar em outro componente. **Lista de pendência: a Rafaella cria as specs quando os tokens voltarem (2026-10-28)** |

## Grid e layout (`grid-layout-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| G-1 | Largura em que cada breakpoint começa (Desktop 14, divisão iPad/Mobile) | 1920 é suposição | — | **Bloqueante** para o responsivo do grid | Implementar só Desktop 12 e perguntar sobre os demais |
| G-2 | Margem desktop | 80 (Figma) ou 24 com largura máxima de 1440 (CSS original) | Figma (80) | Importante | Perguntar |
| G-3 | Menu lateral no iPad e Mobile | Drawer, só ícones ou barra inferior | — | **Bloqueante** para telas com menu abaixo do desktop | Não implementar comportamento abaixo do desktop |
| G-4 | Margem lateral com menu | 48 (token) ou 46 (valor usado em protótipos existentes) | 48 | Menor | 48 |
| G-5 | Nomes dos tokens de grid e layout no código | `--tcece-grid-*`, `--tcece-layout-*` | Proposta | Menor | Proposta |
| G-6 | Ocupação de colunas por tipo de conteúdo | Ex.: formulário em 8 de 12 colunas; empilhamento abaixo do desktop | Não definido | Importante | Perguntar |
| G-7 | Publicação da biblioteca | Variáveis, grid styles e componentes só chegam aos protótipos depois de publicados | — | Importante | Aguardar publicação |

## Cor (`color-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| C-1 | Cor da marca | `#194383` (CSS institucional) ou `#3855A3` (Figma, blue/700) | Vale o Figma (`#3855A3`) até decidir | **Bloqueante** para re-ancorar a escala de blue | Usar os tokens semânticos; trocar a marca só muda as primitivas |
| C-2 | Alerta amarelo como borda/ícone | yellow/700 (4,4:1) ou ícone escuro sobre preenchimento; hoje yellow/500 dá 1,9:1 | Proposta: yellow/700 | Importante | Alerta só como preenchimento, com `tcece/text/on-warning` |
| C-3 | `tcece/button/bg/active` e `tcece/primary/pressed` | Unificar (mesmo valor) | Unificar | Menor | Usar `pressed` |
| C-4 | Nomes das cores no código | `--tcece-color-*` (o CSS original já usa esse prefixo com outro significado) | Decidido em 2026-10-28: nomes do MUI onde o papel existe (`theme.palette.*`) e `--tcece-color-*` para o que é só do TCE (`color-spec-tce.md` 2.0.0, seção 7) | Importante | Decidido; resta conferir colisão com o CSS original na migração |
| C-5 | Nomes de botão por aparência (`hover-light`, `hover-dark`) | Renomear por papel | Na spec de botões | Menor | Manter |
| C-6 | Limpeza do Figma (legacy/Green na coleção errada, coleção Focus, 8 estilos de cor antigos) | Mover, unificar e remover | — | Menor | Não usar |
| C-7 | Tokens fora da spec de cor que os produtos já usam | Bordas (`divider`), cabeçalho de tabela (`tcece/table/header`), status (`status/success/*`, `status/warning/*`), ícones (`tcece/icon/on-action`): documentar na spec de cor | Escrever a seção de bordas, status e ícones | **Bloqueante** para fechar o handoff dos produtos | Usar os tokens como estão no Figma; não criar tokens novos |

## Transversal (vale para todas as specs)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| N-1 | Convenção de nomes no código (consolida C-4, E-5 e G-5) | **Prefixo `tcece` decidido em 2026-10-28** (índice, seção 5). Resta o padrão de nomes por assunto: tipografia, cor, espaçamento, grid e layout | `--tcece-<assunto>-*` em todas as specs | Importante | Seguir a proposta de cada spec; tipografia usa os nomes da seção 8 da spec |

## Tabela (componente `Table` e `Cell Content`, Figma do DS, página 🧩 Componentes)

Já feito em 05/10/2026: cabeçalho em `tcece/table/header` (novo token, alias de grey/100), bordas em `divider`, padding e gap ligados a `spacing/*` (cabeçalho de 14 para 12), cabeçalho em Desktop/Título/16px com altura mínima de 48, texto das células em `text/primary`, propriedade **Estado** (Dados/Vazio, 60 variantes) e documentação corrigida.

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| TB-1 | Largura e alinhamento por coluna | Colunas iguais (hoje), primeira coluna mais larga, largura definida por coluna; números à direita | Primeira coluna mais larga e números à direita | Importante | Dev define as larguras no CSS |
| TB-2 | Propriedade Tamanho (P/M/G em px) | Manter só como pré-visualização ou trocar por densidade (confortável e compacta) | Trocar por densidade; produção usa 100% do grid | Menor | Usar 100% do grid |
| TB-3 | Nomes das variantes do Cell Content | Unificar caixa e idioma (`Badge - Ativado`, `level badge`, `badge detail - em edicao`); um tipo Badge com propriedade de status ligada a `status/*` | Unificar | Importante, **quebra** os protótipos que usam os nomes atuais | Manter os nomes; migrar junto com a atualização dos protótipos |
| TB-9 | Botões do Cell Content: padding de 20 px (fora da escala) e alturas diferentes (Button 56, double e triple button 44) | Padronizar em 16 ou 24 e uma altura | Padronizar na spec de botões | Média | Manter |
| TB-4 | Espaçamentos fora da escala nos badges do Cell Content | 2, 3, 5, 14 e 20 px | Levar à spec do Badge | Menor | Manter |
| TB-5 | Cor do badge "Em rascunho" (#B7791F fixo, cerca de 3,6:1 sobre branco) | Depende de C-2: yellow/700 ou outro token de texto de alerta | Aguardar C-2 | Importante (contraste) | Manter; Ativado e Desativado já usam `status/*` |
| TB-6 | Funcionalidades ausentes | Ordenação, linha em hover e selecionada, estado carregando e erro, paginação, cabeçalho fixo, rolagem horizontal | Definir por prioridade; ordenação e carregando primeiro | Importante | Não usar |
| TB-7 | Linhas 1 e 2 não têm propriedade para ocultar | Criar booleanos ou usar o estado Vazio | Usar Estado=Vazio | Menor | Estado=Vazio |
| TB-8 | Frame de documentação com cores fixas (cerca de 500 preenchimentos) | Ligar aos tokens | Fazer na limpeza geral do DS | Menor | Manter |

## Tarefas de design pendentes (não são decisões)

- Alinhar o Figma e o `tokens.json` à decisão de família (2026-10-21) e ao piso de 16px (2026-10-27): Noto Sans como principal; Atkinson só no label de formulário e em números; nenhum texto abaixo de 16px. Corrigir também as lacunas de tipografia: peso SemiBold, line-height (em %, ligado ao estilo), letter-spacing (`0`) e versões mobile. Migrar os textos dos estilos antigos do Figma para os `Spec/*` e apagar os estilos e a coleção Tipografia Responsiva (escala única, ds-v3).
- Spec de cor: faltam bordas, ícones, status e alertas, estados de campo, cor de ação genérica e elevação (`color-spec-tce.md`, seção 9).
- Mapear Code Connect dos componentes de grid e layout.
