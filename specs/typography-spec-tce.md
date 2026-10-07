# Spec de Tipografia — Design System TCE Ceará

> **Para o Claude do dev:** este arquivo é a fonte de verdade para **tipografia** do Design System TCE Ceará. Aplicações em produtos específicos ficam no handoff do produto, não aqui. Para espaçamento, use `spacing-spec-tce.md`; para grid e layout, `grid-layout-spec-tce.md`; o mapa completo está em `design-system-index.md`. Ao criar ou alterar qualquer UI, siga as regras da seção 1. Valores vêm do `tokens.json` do Design System; se houver conflito entre este arquivo e valores soltos no código, **este arquivo vence**.

Status: em uso, com pendências em `decisoes-em-aberto.md` (T-1 a T-12). Revisão estrutural em 2026-10-07 (versão **ds-v1**).

> **Atenção — pendência de decisão do design (T-1 em `decisoes-em-aberto.md`):** os frames do Figma auditados usam majoritariamente *Noto Sans*, com line-height de 150%, enquanto os tokens definem *Atkinson Hyperlegible Next* e line-heights 1.4/1.6. Até o design decidir qual lado vale, **implemente pelos tokens** (esta spec) e **não copie fonte/peso/line-height direto do Figma**; tamanhos e hierarquia coincidem na maior parte (a auditoria dos frames de cada produto fica no handoff do produto).

## 1. Regras obrigatórias

1. **Nunca use valores soltos** de `font-size`, `font-weight`, `line-height`, cor ou espaçamento. Use sempre os tokens (CSS custom properties da seção 8 ou o objeto `designTokens`).
2. **Fonte principal:** `Atkinson Hyperlegible Next` em toda a interface. Não introduza outras famílias sem aprovação do design.
3. **Escolha o token pelo papel do elemento**, não pelo tamanho visual (tabela da seção 4). Se nenhum papel serve, pergunte ao design em vez de inventar um tamanho.
4. **Títulos e rótulos usam peso 600; texto corrido usa 400.** O peso já faz parte do token: não acrescente `font-weight` por cima.
5. **Responsivo:** tokens `title-*` e `display-*` têm valor desktop e mobile; os tokens `body-*`, `special` e de componente têm valor único. Mobile = viewport < 768px.
6. **Espaçamento:** só a escala de `spacing-spec-tce.md` (o 12 está em avaliação, E-1). Nada de 10px, 20px, 15px.
7. **Não use** `h1`–`h6`/`Typography variant` padrão do MUI com os tamanhos default. Mapeie para os tokens abaixo.
8. Ao terminar uma tela, rode o checklist da seção 9 e aplique as recomendações da seção 7 para o tipo de página em que está trabalhando.

## 2. Famílias

| Token | Fonte | Uso |
|---|---|---|
| `--font-primary` | Atkinson Hyperlegible Next | Toda a interface |
| `--font-secondary` | Noto Sans | Textos secundários (uso raro) |
| `--font-display` | Noto Sans Display | Displays grandes |
| `--font-mono` | Fira Code | Código |

Pesos usados: **400** (texto), **500** (apenas `blockquote`), **600** (títulos, rótulos, botões). O peso 700 existe em `designTokens.ts` mas não é usado em nenhum token da escala.

## 3. Escala tipográfica

Tamanhos em **px** (Figma) com o equivalente em **rem** (código; `rem = px ÷ 16`, base 16px). No CSS da seção 8 os tamanhos já estão em rem.

Letter-spacing é `0px` em todos os tokens.

### Display e Títulos (desktop → mobile)

| Token | Desktop | Mobile | Peso | Line-height |
|---|---|---|---|---|
| `display-large` | 48px (3 rem) | 36px (2,25 rem) | 600 | 1.2 |
| `display-medium` | 40px (2,5 rem) | 28px (1,75 rem) | 600 | 1.2 |
| `display-small` | 32px (2 rem) | 24px (1,5 rem) | 600 | 1.2 |
| `title-2xl` | 32px (2 rem) | 24px (1,5 rem) | 600 | 1.2 |
| `title-lg` | 24px (1,5 rem) | 20px (1,25 rem) | 600 | 1.4 |
| `title-md` | 20px (1,25 rem) | 18px (1,125 rem) | 600 | 1.4 |
| `title-sm` | 16px (1 rem) | 14px (0,875 rem) | 600 | 1.4 |
| `title-xs` | 14px (0,875 rem) | 12px (0,75 rem) | 600 | 1.4 |
| `title-ss` | 12px (0,75 rem) | 11px (0,6875 rem) | 600 | 1.4 |

### Corpo

| Token | Tamanho | Peso | Line-height | Letter-spacing |
|---|---|---|---|---|
| `body-lg` | 18px (1,125 rem) | 400 | 1.6 | 0px |
| `body-md` | 16px (1 rem) | 400 | 1.6 | 0px |
| `body-standard` | 14px (0,875 rem) | 400 | 1.6 | 0px |

### Especiais

| Token | Tamanho | Peso | Line-height | Letter-spacing |
|---|---|---|---|---|
| `blockquote` | 18px (1,125 rem) | 500 | 1.8 | 0px |
| `code` | 14px (0,875 rem) | 600 | 1.4 | 0px |
| `caption` | 12px (0,75 rem) | 400 | 1.4 | 0px |

### Tipografia de componentes

| Token | Tamanho | Peso | Line-height |
|---|---|---|---|
| `button-primary` | 16px (1 rem) | 600 | 1.4 |
| `button-secondary` | 14px (0,875 rem) | 600 | 1.4 |
| `form-label` | 16px (1 rem) | 600 | 1.4 |
| `form-input` | 16px (1 rem) | 400 | 1.6 |
| `form-helper` | 14px (0,875 rem) | 400 | 1.4 |
| `table-header` | 16px (1 rem) | 600 | 1.4 |
| `table-cell` | 16px (1 rem) | 400 | 1.6 |

## 4. Qual token usar (mapa de papéis)

| Elemento | Token |
|---|---|
| Título da página (ex.: "Gerenciar destinatário") | `title-lg` |
| Título de seção (ex.: "Ocorrências") | `title-md` |
| Subseção / título de tabela (ex.: "Informações internas do TCE Ceará") | `title-sm` |
| Label de campo de formulário | `form-label` (16 / 600 / 1.4) |
| Texto digitado no input | `form-input` (16 / 400 / 1.6) |
| Texto de ajuda (helper) | `form-helper` (14 / 400 / 1.4) |
| Mensagem de erro / sucesso | `body-standard`, cor semântica |
| Cabeçalho de coluna de tabela | `table-header` (16 / 600 / 1.4) |
| Célula de tabela | `table-cell` (16 / 400 / 1.6) |
| Botão principal (`.primary`) | `button-primary` (16 / 600) |
| Botão secundário (`.secondary`), "Anterior/Próximo" | `button-secondary` (14 / 600) |
| Paginação (rótulos e números) | `body-md` |
| Breadcrumb | `body-md`, cor `text/secondary`; links em `link/default` |
| Texto corrido, descrições | `body-md` |
| Abas e itens de menu (ativo/inativo) | `title-sm` |
| Título de modal | `title-lg` |
| Metadado, legenda | `caption` (12 / 400) |

Ênfase dentro de texto corrido (datas, status, valor principal de card): usar peso **600** sobre `body-md`/`body-lg`.

## 5. Espaçamento

A escala, os tokens semânticos e as regras de margem estão em **`spacing-spec-tce.md`**; esta spec não repete esses valores. Espaço entre parágrafos e demais espaçamentos de texto: **A DECIDIR** (E-2 em `decisoes-em-aberto.md`).

## 6. Cores de texto e estados

As cores de texto, link e fundo têm spec própria: **`color-spec-tce.md`** (tokens `text/*`, `link/*`, `button/*`, `surface/*`, página 🎨 Cores no Figma). Esta spec usa esses nomes. Equivalência com os nomes antigos desta spec:

| Antes | Agora | Hex |
|---|---|---|
| `text-dark` | `text/primary` | #27282C |
| `text-medium` | `text/secondary` | #474C52 |
| `text-light` | `text/disabled` (só desabilitado) | #73787E |
| `primary` (links) | `link/default` | #3855A3 |
| `error` | `text/error` | #A31D24 |
| `success` | `text/success` | #206442 |
| `warning` | só como preenchimento (`status/warning/default`); texto sobre ele usa `text/on-warning` | #FFAE00 |

Links: `body-md` em `link/default`, sublinhados em texto corrido; hover `link/hover`; foco com o padrão de foco da spec de cor (anel amarelo com contorno preto). Placeholder: `form-input`, itálico, `text/placeholder`.

## 7. Recomendações de uso por página

Esta seção diz **como aplicar a escala em qualquer tela** dos produtos do TCE Ceará: princípios (7.1) e padrões compartilhados (7.2). A aplicação em telas de um produto específico fica no handoff dele (7.3).

### 7.1 Princípios globais

1. **Uma hierarquia por região, no máximo três níveis visíveis:** `title-lg` (página) › `title-md` (seção) › `title-sm` (subseção/grupo). Se parecer faltar um quarto nível, a estrutura da página precisa mudar, não a escala.
2. **Hierarquia se faz com tamanho e peso do token, nunca com cor ou caixa-alta isolada.** Cor secundária (`text/secondary`) é para apoio, não para criar nível.
3. **Mesmo papel, mesmo token, em todos os perfis de usuário** (equipe do TCE Ceará e jurisdicionados): o que muda é o conteúdo, não o estilo.
4. **Texto nunca abaixo de 14px** em conteúdo (`body-standard`); 12px (`caption`) só para metadado e legenda; 11px (`title-ss` mobile) só para rótulos curtos de apoio.
5. **Não reduza a fonte para caber.** Se o texto não cabe, trunque com reticências + tooltip (tabelas) ou quebre a linha (formulários, cards).
6. **Numerais:** colunas numéricas e identificadores com `font-variant-numeric: tabular-nums` (testar suporte da fonte antes de padronizar).

### 7.2 Padrões compartilhados

Os padrões que valem para todas as páginas (cabeçalho, seções, abas, tabelas, formulários, modais, feedback, status, estado vazio, texto longo) estão em **`padroes-de-interface.md`**.

### 7.3 Aplicação por produto

As recomendações por página e fluxo de cada produto ficam no documento de handoff do produto, não nesta spec.

## 8. Implementação

### CSS (custom properties)

```css
:root {
  /* Famílias */
  --font-primary: 'Atkinson Hyperlegible Next', 'Noto Sans', system-ui, sans-serif;
  --font-secondary: 'Noto Sans', system-ui, sans-serif;
  --font-display: 'Noto Sans Display', system-ui, sans-serif;
  --font-mono: 'Fira Code', ui-monospace, monospace;

  /* Desktop (padrão) */
  --display-large-size: 3rem; --display-large-weight: 600; --display-large-lh: 1.2;
  --display-medium-size: 2.5rem; --display-medium-weight: 600; --display-medium-lh: 1.2;
  --display-small-size: 2rem; --display-small-weight: 600; --display-small-lh: 1.2;
  --title-2xl-size: 2rem; --title-2xl-weight: 600; --title-2xl-lh: 1.2;
  --title-lg-size: 1.5rem; --title-lg-weight: 600; --title-lg-lh: 1.4;
  --title-md-size: 1.25rem; --title-md-weight: 600; --title-md-lh: 1.4;
  --title-sm-size: 1rem; --title-sm-weight: 600; --title-sm-lh: 1.4;
  --title-xs-size: 0.875rem; --title-xs-weight: 600; --title-xs-lh: 1.4;
  --title-ss-size: 0.75rem; --title-ss-weight: 600; --title-ss-lh: 1.4;
  --body-lg-size: 1.125rem; --body-lg-weight: 400; --body-lg-lh: 1.6;
  --body-md-size: 1rem; --body-md-weight: 400; --body-md-lh: 1.6;
  --body-standard-size: 0.875rem; --body-standard-weight: 400; --body-standard-lh: 1.6;
  --blockquote-size: 1.125rem; --blockquote-weight: 500; --blockquote-lh: 1.8;
  --code-size: 0.875rem; --code-weight: 600; --code-lh: 1.4;
  --caption-size: 0.75rem; --caption-weight: 400; --caption-lh: 1.4;

}

@media (max-width: 767px) {
  :root {
    --display-large-size: 2.25rem;
    --display-medium-size: 1.75rem;
    --display-small-size: 1.5rem;
    --title-2xl-size: 1.5rem;
    --title-lg-size: 1.25rem;
    --title-md-size: 1.125rem;
    --title-sm-size: 0.875rem;
    --title-xs-size: 0.75rem;
    --title-ss-size: 0.6875rem;
  }
}
```

Uso:

```css
.page-title   { font: var(--title-lg-weight) var(--title-lg-size)/var(--title-lg-lh) var(--font-primary); }
.table-cell   { font: var(--body-md-weight) var(--body-md-size)/var(--body-md-lh) var(--font-primary); }
```

### TypeScript / MUI

- `designTokens.ts` atual está **incompleto** (faltam `title-2xl/xs/ss`, variantes mobile e tokens `special`). Regenere a partir do `tokens.json`; não edite valores à mão.
- No MUI, crie variantes customizadas no `createTheme` com os nomes dos tokens (`title-lg`, `body-md`…) em vez de reaproveitar `h1`–`h6`/`body1`.
- Em `DataGrid`, aplique `table-header` no `columnHeader` e `table-cell` no `cell` via `sx`.

## 9. Checklist de revisão

- [ ] Nenhum `font-size`, `font-weight` ou `line-height` literal no código novo
- [ ] Título da página `title-lg`, seção `title-md`, subseção `title-sm`
- [ ] Labels acima do input com 8px; campos com 16px entre si
- [ ] Cabeçalho de tabela `table-header`, células `table-cell`, paginação `body-md`
- [ ] Seções separadas por 32px; cards com padding 16px
- [ ] Tokens `title-*` têm override mobile (< 768px)
- [ ] Contraste de texto: `text/primary` ou `text/secondary` sobre `surface/default` ou `surface/page`
- [ ] Estados (hover, focus, disabled, erro) usando as cores da seção 6
- [ ] Apenas **um** `title-lg` por página (o título da página); demais seções em `title-md`/`title-sm`
- [ ] Contadores e números de destaque **não** usam o mesmo token do título da página
- [ ] Links em texto corrido sublinhados; cor nunca é o único indicador (erro, sucesso, status)
- [ ] Texto longo com largura máxima de 60–80 caracteres por linha
- [ ] Nenhuma fonte fora das famílias da seção 2 (sem SF Pro, Roboto etc. vindos de templates)

## 10. Contraste das cores de texto

Os contrastes de cada token de texto, link, botão e fundo estão em `color-spec-tce.md` (seções 3 a 6), calculados sobre os valores atuais do Figma. Os valores e a tabela antiga desta seção (baseados em #212121, #1976D2 etc.) foram substituídos. Regras que continuam valendo: placeholders são texto e atingem 4,5:1 (`text/placeholder`); cor nunca é o único indicador de erro, sucesso ou status.

## 11. Pontos em aberto

Todos os pontos em aberto de tipografia estão em **`decisoes-em-aberto.md`** (T-1 a T-12). Esta spec adota o valor do `tokens.json` até a decisão.
