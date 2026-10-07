# Padrões de Interface — Design System TCE Ceará

> **Para o Claude do dev:** este arquivo diz **como montar os blocos recorrentes das telas** (cabeçalho, seções, abas, tabelas, formulários, modais, feedback, status, estado vazio, texto longo) com os tokens do DS. Os valores vêm das specs: `typography-spec-tce.md` (texto), `color-spec-tce.md` (cor), `spacing-spec-tce.md` (espaço) e `grid-layout-spec-tce.md` (grid). Se houver divergência, vale a spec do assunto (ver `design-system-index.md`, seção 4). Itens **A DECIDIR** não se implementam sem resposta do design.

Status: rascunho. Separado da spec de tipografia (antes seção 7.2) em 2026-10-07 (versão **ds-v1**), sem mudança de conteúdo além das referências.

## 1. Padrões compartilhados (valem para todas as páginas)

| Padrão | Estrutura tipográfica |
|---|---|
| **Cabeçalho de página** | Breadcrumb `body-md` `text/secondary` (links `link/default`) → título `title-lg` → descrição `body-md` `text/secondary`, 16px abaixo do título → ação principal (`button-primary`) alinhada à direita do título |
| **Seções** | Título `title-md`; descrição `body-md` `text/secondary` 16px abaixo; 32px entre seções |
| **Contagem no título** | "Subtipos (10)": mesmo token e peso do título, sem estilo diferente para o número |
| **Abas** | `title-sm`; ativa em `link/default` com underline 2px (cor de ação genérica ainda sem token, ver `color-spec-tce.md` seção 9); inativa em `text/secondary` (não `text/disabled`, que fica abaixo de 4,5:1) |
| **Tabelas** | Cabeçalho `table-header`; células `table-cell`; datas e status destacados com peso 600; alinhamento à esquerda para texto, à direita para números, ao centro para ícones/ações; truncar com tooltip |
| **Formulários** | `form-label` acima do campo (8px) · `form-input` · `form-helper` · erro em `form-helper` + ícone + cor `text/error` (nunca só cor); placeholder (`text/placeholder`) nunca substitui label |
| **Modais** | Título `title-lg`; descrição `body-md`; botão de confirmação `button-primary` à direita, cancelar `button-secondary` à esquerda dele |
| **Feedback (alerta, banner, toast)** | Título `title-sm`; mensagem `body-md` (ou `body-standard` em toast); cor semântica em ícone, borda e fundo claro; **texto em `text/primary`**, ou `text/error`, `text/success` e `text/info` em mensagens curtas (todos acima de 4,5:1, ver `color-spec-tce.md`) |
| **Status / badges** | `title-xs` (14/600), `text/primary` sobre fundo claro da cor semântica; texto sempre presente (Aberta, Em revisão, Fechada), cor sozinha não basta |
| **Estado vazio** | `title-sm` + `body-md` `text/secondary`, centralizados, com um botão `button-primary` quando houver ação |
| **Par rótulo–valor** (detalhes, revisão) | Rótulo `body-standard` `text/secondary`; valor `body-md` `text/primary`; 4px entre os dois |
| **Identificadores** (nº de ocorrência, protocolo) | Mesma família do corpo, `tabular-nums`; em tabela, `table-cell` com peso 600; em título, ver T-5 |
| **Texto longo** (justificativas, respostas, conteúdo de comunicações) | `body-md` ou `body-lg`, line-height 1.6, largura máxima 60–80 caracteres (≈ 640–720px), espaço entre parágrafos: A DECIDIR (E-2) |
| **Links em texto corrido** | `link/default`, **sempre sublinhados**; hover `link/hover`; foco com anel amarelo e contorno preto |
| **Paginação** | Rótulos e números `body-md`; "Anterior/Próximo" `button-secondary` |
