# Padrões de Interface — Design System TCE Ceará

> **Para o Claude do dev:** este arquivo diz **como montar os blocos recorrentes das telas** (cabeçalho, seções, abas, tabelas, formulários, modais, feedback, status, estado vazio, texto longo) com os tokens do DS. Os valores vêm das specs: `typography-spec-tce.md` (texto), `color-spec-tce.md` (cor), `spacing-spec-tce.md` (espaço) e `grid-layout-spec-tce.md` (grid). Se houver divergência, vale a spec do assunto (ver `design-system-index.md`, seção 4). Itens **A DECIDIR** não se implementam sem resposta do design.

| Campo | Valor |
|---|---|
| **Versão da spec** | **2.0.0** (rascunho) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **2. Moléculas e 3. Organismos (mistura; cada padrão declara a sua)** |
| **Depende de** (data da última atualização lida) | `typography-spec-tce.md` 4.1.0, `color-spec-tce.md` 2.1.0, `spacing-spec-tce.md` 1.1.0, `grid-layout-spec-tce.md` 1.0.0 e `button-spec-tce.md` 0.7.0 (todas lidas em 2026-10-28) |
| **Usada por** | Telas dos produtos (Páginas, fora do DS); specs de componente que nascerem destes padrões (tabela, modal, formulário, paginação…) |
| Arquivo e Figma | `specs/padroes-de-interface.md` |

Histórico na última seção. Formato do cabeçalho: `design-system-index.md`, seção 4.1.

> **Família tipográfica:** todos os padrões abaixo usam **Noto Sans**, exceto onde a tabela disser "Atkinson": o label de formulário e números (contadores, identificadores, colunas numéricas, paginação). Regras completas em `typography-spec-tce.md`, seção 2.1. Se outros rótulos (cabeçalho de tabela, abas, badges, rótulo de par rótulo–valor) também devem usar Atkinson, é a decisão T-13.

## 1. Padrões compartilhados (valem para todas as páginas)

| Padrão | Estrutura tipográfica |
|---|---|
| **Cabeçalho de página** | Breadcrumb `body-md` `text/secondary` (links `tcece/link/default`) → título `title-lg` → descrição `body-md` `text/secondary`, 16px abaixo do título → ação principal (botão primário, `title-sm`) alinhada à direita do título |
| **Seções** | Título `title-md`; descrição `body-md` `text/secondary` 16px abaixo; 32px entre seções |
| **Contagem no título** | "Subtipos (10)": mesmo token e peso do título, sem estilo diferente para o número; o número em Atkinson (`.tcece-num`), o restante do título em Noto Sans |
| **Abas** | `title-sm`; ativa em `tcece/link/default` com underline 2px (cor de ação genérica ainda sem token, ver `color-spec-tce.md` seção 9); inativa em `text/secondary` (não `text/disabled`, que fica abaixo de 4,5:1) |
| **Tabelas** | Cabeçalho `title-sm`; células `body-md`; datas e status destacados com peso 600; alinhamento à esquerda para texto, à direita para números, ao centro para ícones/ações; células numéricas em Atkinson com `tabular-nums` (`.tcece-num`); truncar com tooltip |
| **Formulários** | label (`title-sm`, **Atkinson**) acima do campo (8px) · texto digitado `body-md` · ajuda `caption` · erro em `caption` + ícone + cor `tcece/text/error` (nunca só cor); placeholder (`tcece/text/placeholder`) nunca substitui label |
| **Modais** | Título `title-lg`; descrição `body-md`; botão de confirmação (primário) à direita, cancelar (secundário) à esquerda dele; ambos `title-sm` (componente em `button-spec-tce.md`) |
| **Feedback (alerta, banner, toast)** | Título `title-sm`; mensagem `body-md`; cor semântica em ícone, borda e fundo claro; **texto em `text/primary`**, ou `tcece/text/error`, `tcece/text/success` e `tcece/text/info` em mensagens curtas (todos acima de 4,5:1, ver `color-spec-tce.md`) |
| **Status / badges** | `title-sm` (16/600), `text/primary` sobre fundo claro da cor semântica; texto sempre presente (Aberta, Em revisão, Fechada), cor sozinha não basta |
| **Estado vazio** | `title-sm` + `body-md` `text/secondary`, centralizados, com um botão primário quando houver ação |
| **Par rótulo–valor** (detalhes, revisão) | Rótulo `body-md` `text/secondary`; valor `body-md` `text/primary` (a diferença é cor e posição, não tamanho); 4px entre os dois. Família: Noto Sans (T-13); valor numérico em Atkinson |
| **Identificadores** (nº de ocorrência, protocolo) | **Atkinson** (`.tcece-num`) com `tabular-nums`; em tabela, `body-md` com peso 600; em título, ver T-5 |
| **Texto longo** (justificativas, respostas, conteúdo de comunicações) | `body-md` ou `body-lg`, line-height 1.6, largura máxima 60–80 caracteres (≈ 640–720px), espaço entre parágrafos 24px (`typography-spec-tce.md`, seção 5). Números dentro de frase ficam em Noto Sans |
| **Links em texto corrido** | `tcece/link/default`, **sempre sublinhados**; hover `tcece/link/hover`; foco com anel amarelo e contorno preto |
| **Paginação** | Rótulos `body-md`; números das páginas em Atkinson (`.tcece-num`); "Anterior/Próximo" botão secundário (`title-sm`) |

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 2.0.0 | 2026-10-28 | Tokens de cor com os nomes novos (`color-spec-tce.md` 2.0.0+); classe `.num` → `.tcece-num` (**quebra de nome**); ponteiro para a spec do botão nos modais |
| 1.2.0 | 2026-10-28 | `ds-v3`: tokens de componente (`button-*`, `form-*`, `table-*`) removidos; padrões usam `title-sm`, `body-md` e `caption` |
| 1.1.1 | 2026-10-27 | Piso de 16px (badges, toast e rótulo do par rótulo–valor trocam de token) |
| 1.1.0 | 2026-10-21 | Famílias tipográficas (Noto Sans por padrão; Atkinson só em números e labels) |
| 1.0.0 | 2026-10-07 | Separado da spec de tipografia (antes seção 7.2); revisão estrutural (`ds-v1`) |
