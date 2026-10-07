# Decisões em aberto — Design System TCE Ceará

> **Para o Claude do dev:** tudo o que está aqui **não foi decidido**. Não implemente nenhum desses pontos por conta própria; use a coluna "Enquanto isso" e pergunte ao design se precisar de mais. Cada decisão tomada atualiza a spec de origem e sai desta lista.

Status: consolidado em 2026-10-05; **lista única** de pendências do DS desde 2026-10-07 (as specs apontam para os IDs daqui). Revisão estrutural em 2026-10-07 (versão **ds-v1**). Índice geral: `design-system-index.md`.

Legenda de impacto: **Bloqueante** = o dev não deve fechar a padronização sem a decisão. **Importante** = muda valor ou nome usado em várias telas. **Menor** = afeta poucos casos.

## Tipografia (`typography-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| T-1 | Família tipográfica | (a) migrar Figma para Atkinson; (b) trocar a família principal nos tokens | Spec escrita para (a) | **Bloqueante** | Implementar pelos tokens (Atkinson); não copiar fonte do Figma |
| T-2 | Line-height | 1,5 como padrão do corpo ou manter 1,4/1,6 | Tokens (1,4 e 1,6) | Importante | Usar os tokens |
| T-3 | Peso | 600 como único peso de ênfase; botões em 600 ou Regular | Tokens (600) | Importante | Usar 600 |
| T-4 | Tamanho 18px | Criar tokens `title` e `button` de 18 ou padronizar em 16/20 | Sem token | Importante | Não usar 18px fora de `body-lg` |
| T-5 | Número da ocorrência em título | Token `title-lg-regular` ou peso 600 do título | Peso do título | Menor | `title-lg` com o peso do título |
| T-6 | Título de modal e de página | `title-lg` (24) em ambos | Adotado | Menor | `title-lg` |
| T-7 | Escala mobile | Subir `title-sm` mobile de 14 para 16 | Tokens (14) | Importante | Usar os tokens |
| T-8 | Texto de ajuda | 14 (token) ou 16 (guia antigo) | Adotado: 14 | Menor | 14 |
| T-9 | Line-height dos títulos | 1,2 (reset antigo) ou o do token | Adotado: o do token | Menor | Token |
| T-10 | Ponto de quebra mobile | 768px | Adotado | Importante | 768px (ver também G-1) |
| T-11 | Negrito em texto corrido | Sem token | Adotado: 600 | Menor | 600 |
| T-12 | Cores de texto | Resolvido em parte por `color-spec-tce.md` (abas inativas em `text/secondary`, placeholder em `text/placeholder`, texto verde com 7,1:1); resta o alerta amarelo (C-2) | Resolvido em parte | Menor | Usar os tokens de cor |

## Espaçamento (`spacing-spec-tce.md`)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| E-1 | `spacing/12` | Manter ou remover (o CSS original não usa) | Em avaliação | Menor | Evitar 12 em tela nova |
| E-2 | Espaçamento de texto | Manter o do CSS original (letter-spacing 0,08–0,12 em, word-spacing 0,16 em, line-height 1,5, parágrafo 2× o corpo) ou `letter-spacing: 0` e parágrafo 12 da spec de tipografia | Proposta: manter o do CSS original e corrigir a spec de tipografia (seções 3 e 5) | Importante | Perguntar antes de definir letter-spacing, word-spacing e espaço entre parágrafos |
| E-3 | `card-padding` | 16 (spec) ou 24 (uso atual em protótipos) | Token em 16 | Importante | Perguntar |
| E-5 | Prefixo e nomes dos tokens de espaçamento | `--tcece-space-*` ou `--space-*`; alinhar com nomes de tipografia (`title-desk-md` no CSS, `title-md` na spec) | `--tcece-space-*` | Importante | `--tcece-space-*` |
| E-6 | Padding vertical do chip | 3 está fora da escala | — | Menor | Perguntar |
| E-7 | Espaço mínimo entre alvos clicáveis | O CSS usa margem de 4 | — | Menor | 4 |
| E-8 | Botão do DS no Figma | 10/20 (Figma) ou 8/16 com altura mínima 44 (CSS) | Alinhar ao CSS | Importante | 8/16 com min-height 44 |

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
| C-2 | Alerta amarelo como borda/ícone | yellow/700 (4,4:1) ou ícone escuro sobre preenchimento; hoje yellow/500 dá 1,9:1 | Proposta: yellow/700 | Importante | Alerta só como preenchimento, com `text/on-warning` |
| C-3 | `button/bg/active` e `button/bg/pressed` | Unificar (mesmo valor) | Unificar | Menor | Usar `pressed` |
| C-4 | Nomes das cores no código | `--tcece-color-*` (o CSS original já usa esse prefixo com outro significado) | `--tcece-color-text-primary` etc. | Importante | Proposta |
| C-5 | Nomes de botão por aparência (`hover-light`, `hover-dark`) | Renomear por papel | Na spec de botões | Menor | Manter |
| C-6 | Limpeza do Figma (legacy/Green na coleção errada, coleção Focus, 8 estilos de cor antigos) | Mover, unificar e remover | — | Menor | Não usar |
| C-7 | Tokens fora da spec de cor que os produtos já usam | Bordas (`border/subtle`), cabeçalho de tabela (`table/header`), status (`status/success/*`, `status/warning/*`), ícones (`icon/on-action`): documentar na spec de cor | Escrever a seção de bordas, status e ícones | **Bloqueante** para fechar o handoff dos produtos | Usar os tokens como estão no Figma; não criar tokens novos |

## Transversal (vale para todas as specs)

| ID | Decisão | Opções | Proposta / adotado hoje | Impacto | Enquanto isso |
|---|---|---|---|---|---|
| N-1 | Convenção de nomes no código (consolida C-4, E-5 e G-5) | Prefixo único (`--tcece-*`) e padrão de nomes para tipografia, cor, espaçamento, grid e layout | `--tcece-<assunto>-*` em todas as specs | Importante | Seguir a proposta de cada spec; tipografia usa os nomes da seção 8 da spec |

## Tabela (componente `Table` e `Cell Content`, Figma do DS, página 🧩 Componentes)

Já feito em 05/10/2026: cabeçalho em `table/header` (novo token, alias de gray/100), bordas em `border/subtle`, padding e gap ligados a `spacing/*` (cabeçalho de 14 para 12), cabeçalho em Desktop/Título/16px com altura mínima de 48, texto das células em `text/primary`, propriedade **Estado** (Dados/Vazio, 60 variantes) e documentação corrigida.

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

- Levar ao dono do DS as lacunas de tipografia: Atkinson, tamanhos 14/12, peso SemiBold, line-height e letter-spacing.
- Spec de cor: faltam bordas, ícones, status e alertas, estados de campo, cor de ação genérica e elevação (`color-spec-tce.md`, seção 9).
- Mapear Code Connect dos componentes de grid e layout.
