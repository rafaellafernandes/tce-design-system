# Spec de Tipografia — Design System TCE Ceará

> **Para o Claude do dev:** este arquivo é a fonte de verdade para **tipografia** do Design System TCE Ceará. Aplicações em produtos específicos ficam no handoff do produto, não aqui. Para espaçamento, use `spacing-spec-tce.md`; para grid e layout, `grid-layout-spec-tce.md`; o mapa completo está em `design-system-index.md`. Ao criar ou alterar qualquer UI, siga as regras da seção 1. Se houver conflito entre este arquivo e valores soltos no código, no `tokens.json` ou no `designTokens.ts`, **este arquivo vence**; os dois devem ser regenerados a partir daqui.

| Campo | Valor |
|---|---|
| **Versão da spec** | **4.0.1** (em uso, com pendências) |
| **Última atualização** | **2026-10-28** |
| Versão do DS | em revisão, ainda sem tag (o `CHANGELOG.md` registra `ds-v3` como a confirmar; a tag é decisão do design) |
| **Camada** | **1. Átomos (tokens)** |
| **Depende de** (data da última atualização lida) | Tokens de mesma camada, lidas em 2026-10-28 (ainda sem cabeçalho padrão; última revisão registrada em cada uma): `color-spec-tce.md` (2.0.0, 2026-10-28; cores de texto), `spacing-spec-tce.md` (ds-v1, 2026-10-07; escala, E-1), `grid-layout-spec-tce.md` (ds-v1, 2026-10-07; breakpoints, G-1) |
| **Usada por** | `button-spec-tce.md`, `padroes-de-interface.md` e, quando existirem, as specs de campo, label, tabela, modal, header, menu lateral e demais componentes com texto |
| Arquivo e Figma | `specs/typography-spec-tce.md`; coleção `Typography` e estilos `Spec/*` do arquivo ⭐ Design System TCE (seção 12) |

Pendências abertas: T-3 a T-6, T-9 a T-15 (`decisoes-em-aberto.md`). O histórico de versões está na seção 13; o formato do cabeçalho é o padrão do DS (`design-system-index.md`, seção 4.1).

> **Família tipográfica (decidido em 2026-10-21, fecha T-1):** a fonte principal do sistema é **Noto Sans**. **Atkinson Hyperlegible Next** é a fonte de **acento** e só entra em **números** e em **labels** (seções 2 e 2.1). Todo o resto da interface usa Noto Sans. Os tokens e o CSS antigos que punham Atkinson em toda a interface estão **errados** e devem ser corrigidos. No Figma, os estilos antigos (nomeados por px, em Plus Jakarta Sans ou Atkinson) **não seguem** esta spec e estão sendo migrados: a referência são os estilos `Spec/*`, que são a **única escala** (os valores do Figma e desta spec devem ser os mesmos; se divergirem, vale esta spec).
>
> **Piso de 16px (decidido em 2026-10-27):** nenhum texto da interface pode ter menos de 16px (1 rem), em nenhum breakpoint. A hierarquia abaixo de 18px se faz com **peso (400 ou 600) e cor**, nunca com tamanho menor. Isso vale para badges, chips, legendas, texto de ajuda, tooltips, rodapés e tabelas.
>
> **Escala única (decidido em 2026-10-28):** existe **uma só** definição tipográfica, a da seção 3. Botão, label, input, helper e tabela **não têm token próprio**: usam o token da escala indicado no mapa de papéis (seção 4). Line-height, letter-spacing, word-spacing e espaço entre parágrafos também estão na escala (seção 5). Os frames antigos do Figma com line-height de 150% e letter-spacing de 4 a 12% estão desatualizados: **implemente pelos tokens**.

## 1. Regras obrigatórias

1. **Nunca use valores soltos** de `font-size`, `font-weight`, `line-height`, `letter-spacing`, `word-spacing`, cor ou espaçamento. Use sempre os tokens (CSS custom properties da seção 8 ou o objeto `designTokens`).
2. **Fonte principal:** `Noto Sans`, em toda a interface. **Exceção única:** `Atkinson Hyperlegible Next` em **números** e **labels**, conforme a seção 2.1. Não introduza outras famílias sem aprovação do design.
3. **Não declare `font-family` à mão.** A família vem do token do papel (Noto Sans por padrão; `--tcece-font-accent` só nos casos da seção 2.1). O erro mais comum é aplicar Atkinson no `body` ou no tema inteiro.
4. **Escolha o token pelo papel do elemento**, não pelo tamanho visual (tabela da seção 4). Se nenhum papel serve, pergunte ao design em vez de inventar um tamanho.
5. **Títulos e rótulos usam peso 600; texto corrido usa 400.** O peso já faz parte do token: não acrescente `font-weight` por cima.
6. **Responsivo:** tokens `title-*` e `display-*` têm valor desktop e mobile; os tokens `body-*` e `special` têm valor único. Mobile = viewport < 768px.
7. **Espaçamento:** só a escala de `spacing-spec-tce.md` (o 12 está em avaliação, E-1). Nada de 10px, 20px, 15px.
8. **Não use** `h1`–`h6`/`Typography variant` padrão do MUI com os tamanhos default. Mapeie para os tokens abaixo.
9. Ao terminar uma tela, rode o checklist da seção 9 e aplique as recomendações da seção 7 para o tipo de página em que está trabalhando.
10. **Nenhum texto abaixo de 16px.** Se o conteúdo não cabe, mude o layout (quebra de linha, coluna mais larga, truncar com tooltip); não reduza a fonte.

## 2. Famílias

| Token | Fonte | Uso |
|---|---|---|
| `--tcece-font-primary` | Noto Sans | **Padrão de toda a interface**: títulos, corpo, botões, tabelas, menus, abas |
| `--tcece-font-accent` | Atkinson Hyperlegible Next | **Só** números e labels (seção 2.1) |
| `--tcece-font-mono` | Fira Code | Só o token `code` |

`--font-secondary` (antes Noto Sans) foi removido: Noto Sans agora é a fonte principal.

`display-*` usam Noto Sans (`--tcece-font-primary`); `--font-display` (Noto Sans Display) foi removido.

Pesos usados: **400** (texto), **500** (apenas `blockquote`), **600** (títulos, rótulos, botões). O peso 700 existe em `designTokens.ts` mas não é usado em nenhum token da escala.

### 2.1 Onde a Atkinson Hyperlegible Next entra

| Caso | Regra |
|---|---|
| **Labels de formulário** | Label acima do campo: `title-sm` com `--tcece-font-accent`. É o único papel de texto que usa `--tcece-font-accent` por padrão |
| **Números** | Elementos em que o conteúdo é **o número**: contadores ("(10)", totais por estado), identificadores (nº de ocorrência, protocolo, ID), valores numéricos de destaque, colunas numéricas de tabela, paginação (números de página), datas e prazos exibidos como valor. Sempre com `font-variant-numeric: tabular-nums` |

Fora disso, **Noto Sans**. Em especial:

- Número **dentro de frase** ("Você tem 3 dias para responder") fica em Noto Sans, junto com o resto do texto. Não troque a família no meio da linha.
- Helper, placeholder, texto digitado no input, cabeçalho de tabela, botões, abas e badges ficam em Noto Sans (a decisão sobre cabeçalho de tabela, badges e abas como "labels" está em T-13).
- A família muda; **tamanho, peso e line-height continuam os do token do papel**. Um número em célula de tabela (`body-md`) continua 16 / 400 / 1.6, só que em Atkinson.
- **No Figma**, a troca de família é feita pela variável `font/accent` (Atkinson) ligada ao texto, mantendo o estilo `Spec/*` aplicado; o padrão é `font/primary` (Noto Sans). Não troque a fonte direto no texto: isso solta o estilo da escala. No código, equivale ao `--tcece-font-accent` sobre o token do papel.

## 3. Escala tipográfica

Tamanhos em **px** (Figma) com o equivalente em **rem** (código; `rem = px ÷ 16`, base 16px). No CSS da seção 8 os tamanhos já estão em rem.

**Menor tamanho da escala: 16px.** Letter-spacing é `0` em todos os tokens (seção 5).

### Display e Títulos (desktop → mobile)

| Token | Desktop | Mobile | Peso | Line-height |
|---|---|---|---|---|
| `display-2xl` (proposto, T-14) | 80px (5 rem) | 44px (2,75 rem) | 700 | 1.1 |
| `display-xl` (proposto, T-14) | 64px (4 rem) | 40px (2,5 rem) | 700 | 1.1 |
| `display-large` | 48px (3 rem) | 36px (2,25 rem) | 600 | 1.2 |
| `display-medium` | 40px (2,5 rem) | 28px (1,75 rem) | 600 | 1.2 |
| `display-small` | 32px (2 rem) | 24px (1,5 rem) | 600 | 1.2 |
| `title-2xl` | 32px (2 rem) | 24px (1,5 rem) | 600 | 1.2 |
| `title-lg` | 24px (1,5 rem) | 20px (1,25 rem) | 600 | 1.4 |
| `title-md` | 20px (1,25 rem) | 18px (1,125 rem) | 600 | 1.4 |
| `title-sm` | 16px (1 rem) | 16px (1 rem) | 600 | 1.4 |

### Corpo

| Token | Tamanho | Peso | Line-height | Letter-spacing |
|---|---|---|---|---|
| `body-lg` | 18px (1,125 rem) | 400 | 1.6 | 0px |
| `body-md` | 16px (1 rem) | 400 | 1.6 | 0px |

### Especiais

| Token | Tamanho | Peso | Line-height | Letter-spacing |
|---|---|---|---|---|
| `blockquote` | 18px (1,125 rem) | 500 | 1.8 | 0px |
| `code` | 16px (1 rem) | 600 | 1.4 | 0px |
| `caption` | 16px (1 rem) | 400 | 1.4 | 0px |

`code` usa Fira Code (`--tcece-font-mono`); os demais, Noto Sans. `caption` tem o mesmo tamanho do corpo e se distingue por `text/secondary` e line-height 1.4.

### Componentes não têm token próprio

Botão, label, input, helper, cabeçalho e célula de tabela usam tokens da escala (mapa de papéis, seção 4). Os antigos `button-primary`, `button-secondary`, `form-label`, `form-input`, `form-helper`, `table-header` e `table-cell` **foram removidos** (ds-v3), porque repetiam valores que a escala já tem:

| Antigo | Agora |
|---|---|
| `button-primary`, `button-secondary` | `title-sm` (16 / 600 / 1.4) |
| `form-label` | `title-sm` + `--tcece-font-accent` (Atkinson) |
| `form-input` | `body-md` (16 / 400 / 1.6) |
| `form-helper` | `caption` (16 / 400 / 1.4) |
| `table-header` | `title-sm` |
| `table-cell` | `body-md`; células numéricas com `--tcece-font-accent` |

### 3.1 Regras dos tokens `display-*` (proposta, T-14)

- **Uso:** hero e páginas institucionais, um `display-*` por página. Telas de produto continuam com `title-*`.
- **Composição do hero:** linha de apoio acima (`title-md`, por exemplo "Boas vindas ao"), nome em `display-2xl` ou `display-xl`, complemento abaixo em `body-lg`.
- **Tamanho fluido (opcional):** entre o valor mobile e o desktop com `clamp()`. Os breakpoints continuam valendo.
- **Letter-spacing 0:** o hero atual usa espaçamento largo, que conflita com a seção 5. Manter é exceção a decidir, só para `display-*`.
- **Acessibilidade:** sem altura fixa, no máximo 2 linhas por bloco, `text-wrap: balance`, funcionar em zoom de 400% sem corte nem rolagem horizontal.
- **Peso:** 700 nos dois tokens novos e 600 nos demais (a decidir).

## 4. Qual token usar (mapa de papéis)

| Elemento | Token |
|---|---|
| Título da página (ex.: "Gerenciar destinatário") | `title-lg` |
| Título de seção (ex.: "Ocorrências") | `title-md` |
| Subseção / título de tabela (ex.: "Informações internas do TCE Ceará") | `title-sm` |
| Label de campo de formulário | `title-sm` (16 / 600 / 1.4) com `--tcece-font-accent` (**Atkinson**) |
| Texto digitado no input | `body-md` (16 / 400 / 1.6) |
| Texto de ajuda (helper) | `caption` (16 / 400 / 1.4) |
| Mensagem de erro / sucesso | `caption` + ícone, cor semântica |
| Cabeçalho de coluna de tabela | `title-sm` (16 / 600 / 1.4) |
| Célula de tabela | `body-md` (16 / 400 / 1.6); célula numérica com `--tcece-font-accent` e `tabular-nums` |
| Número isolado (contador, ID, protocolo, valor de destaque) | token do papel + `--tcece-font-accent` + `tabular-nums` (classe `.tcece-num`, seção 8) |
| Botão (todas as variantes do `Button`) | `title-sm` (16 / 600); o componente está em `button-spec-tce.md` |
| "Anterior" e "Próximo" da paginação | `title-sm` (16 / 600), no `Button` `outlined`; o que diferencia as variantes é a cor, não a tipografia |
| Paginação (rótulos e números) | `body-md`; números com `--tcece-font-accent` |
| Breadcrumb | `body-md`, cor `text/secondary`; links em `tcece/link/default` |
| Texto corrido, descrições | `body-md` |
| Abas e itens de menu (ativo/inativo) | `title-sm` |
| Título de modal | `title-lg` |
| Metadado, legenda | `caption` (16 / 400 / 1.4), `text/secondary` |
| Selo, status e chip (texto) | `title-sm` (16 / 600); o componente cresce para acomodar o texto. Exceção: chip de identificação ao lado de um nome (cargo ou perfil de usuário) usa `body-md` (16 / 400) em `text/secondary`, para não competir com o nome |
| Rótulo de par rótulo–valor | `body-md` em `text/secondary` |
| Tooltip | `body-md` |
| Placeholder | `body-md` em itálico, `tcece/text/placeholder` |
| Trecho de código | `code` (16 / 600 / 1.4, Fira Code) |
| Número de destaque (indicador, KPI) | `title-2xl` (32 / 600 / 1.2; mobile 24) com `--tcece-font-accent` e `tabular-nums` (`.tcece-num`). Texto de apoio abaixo: `body-md` em `text/secondary`. Não use `title-lg`, que é do título da página |
| `display-2xl` | Proposto (T-14): hero de capa institucional (home do Conecta, páginas de entrada). Uma por página |
| `display-xl` | Proposto (T-14): hero de página inicial de módulo. Uma por página |
| `display-large` | Proposto (T-14): título de página de abertura ou de seção de destaque |
| `display-medium`, `display-small` | Proposto (T-14): destaques numéricos grandes e chamadas de painel. `display-small` repete o tamanho de `title-2xl` |
| `display-*` em telas de produto | Não use sem aprovação do design |

Ênfase dentro de texto corrido (datas, status, valor principal de card): usar peso **600** sobre `body-md`/`body-lg`.

## 5. Espaçamento de texto

Espaçamento **de layout** (gap, padding, margem) está em **`spacing-spec-tce.md`**. Esta seção é a **única definição** do espaçamento **de texto**: entrelinha, letter-spacing, word-spacing e espaço entre parágrafos. Decidido em 2026-10-28 (fecha T-2 e E-2).

| Propriedade | Valor | Observação |
|---|---|---|
| `line-height` | o do token (seção 3): 1.2 em `display-*` e `title-2xl`; 1.4 em `title-lg`, `title-md`, `title-sm`, `code` e `caption`; 1.6 em `body-*`; 1.8 em `blockquote` | Unitless. Não copie o line-height dos frames antigos do Figma (150%) |
| `letter-spacing` | `0` em todos os tokens | Os 0,08 a 0,12 em do CSS original e os 4 a 12% dos estilos antigos do Figma **não valem** mais |
| `word-spacing` | `0` | |
| Espaço entre parágrafos (texto corrido) | **24px** (`1.5rem`), via `margin-block-end`/`gap` entre parágrafos | Só texto corrido: justificativas, respostas, conteúdo de comunicações. Vale a escala de `spacing-spec-tce.md` |
| Recuo da primeira linha | não usa | |
| Largura máxima da linha | 60–80 caracteres (≈ 640–720px) | |

### O texto deve aguentar o espaçamento do usuário (WCAG 1.4.12)

Os valores padrão acima não são os mínimos da WCAG, e não precisam ser: o critério 1.4.12 exige que **nada se perca nem fique sobreposto** quando o usuário (extensão, folha de estilo própria, configuração do navegador) aplicar, ao mesmo tempo:

- line-height de pelo menos **1,5×** o tamanho da fonte;
- espaço entre parágrafos de pelo menos **2×** o tamanho da fonte;
- letter-spacing de pelo menos **0,12 em**;
- word-spacing de pelo menos **0,16 em**.

Consequências para o código e o Figma:

1. **Componente com texto usa `min-height`, nunca `height` fixa.** Botão, chip, selo, input, item de menu, aba, célula de tabela e breadcrumb crescem com o texto.
2. **Sem `overflow: hidden` em contêiner de texto** sem alternativa (truncar com reticências é permitido só em tabela, com tooltip, conforme a seção 7.1).
3. **Largura do contêiner não pode ser fixa** em texto que pode quebrar linha; use largura mínima ou máxima.
4. **Não use `px` para altura ou largura de caixa de texto**; use `rem`, `em` ou `min-height`.
5. **Teste de aceitação:** aplicar os quatro valores acima numa tela e conferir que nada é cortado, sobreposto ou escondido. Vale para cada componente novo.

## 6. Cores de texto e estados

As cores de texto, link e fundo têm spec própria: **`color-spec-tce.md`** (tokens `text/*`, `tcece/text/*`, `tcece/link/*`, `primary/*`, `background/*`, página 🎨 Cores no Figma). Esta spec usa esses nomes. Equivalência com os nomes antigos desta spec:

| Antes | Agora | Hex |
|---|---|---|
| `text-dark` | `text/primary` | #27282C |
| `text-medium` | `text/secondary` | #474C52 |
| `text-light` | `text/disabled` (só desabilitado) | #73787E |
| `primary` (links) | `tcece/link/default` | #3855A3 |
| `error` | `tcece/text/error` | #A31D24 |
| `success` | `tcece/text/success` | #206442 |
| `warning` | só como preenchimento (`warning/main`); texto sobre ele usa `tcece/text/on-warning` | #FFAE00 |

Links: `body-md` em `tcece/link/default`, sublinhados em texto corrido; hover `tcece/link/hover`; foco com o padrão de foco da spec de cor (anel amarelo com contorno preto). Placeholder: `body-md`, itálico, `tcece/text/placeholder`.

## 7. Recomendações de uso por página

Esta seção diz **como aplicar a escala em qualquer tela** dos produtos do TCE Ceará: princípios (7.1) e padrões compartilhados (7.2). A aplicação em telas de um produto específico fica no handoff dele (7.3).

### 7.1 Princípios globais

1. **Uma hierarquia por região, no máximo três níveis visíveis:** `title-lg` (página) › `title-md` (seção) › `title-sm` (subseção/grupo). Se parecer faltar um quarto nível, a estrutura da página precisa mudar, não a escala.
2. **Hierarquia se faz com tamanho e peso do token, nunca com cor ou caixa-alta isolada.** Cor secundária (`text/secondary`) é para apoio, não para criar nível.
3. **Mesmo papel, mesmo token, em todos os perfis de usuário** (equipe do TCE Ceará e jurisdicionados): o que muda é o conteúdo, não o estilo.
4. **Texto nunca abaixo de 16px**, sem exceção e em qualquer breakpoint. Abaixo de 18px, a diferença entre níveis vem de peso (400/600) e cor (`text/primary`/`text/secondary`), não de tamanho.
5. **Não reduza a fonte para caber.** Se o texto não cabe, trunque com reticências + tooltip (tabelas) ou quebre a linha (formulários, cards).
6. **Numerais:** colunas numéricas e identificadores usam `--tcece-font-accent` (Atkinson) com `font-variant-numeric: tabular-nums` (seção 2.1). Testar o suporte a `tabular-nums` na Atkinson antes de padronizar.

### 7.2 Padrões compartilhados

Os padrões que valem para todas as páginas (cabeçalho, seções, abas, tabelas, formulários, modais, feedback, status, estado vazio, texto longo) estão em **`padroes-de-interface.md`**.

### 7.3 Aplicação por produto

As recomendações por página e fluxo de cada produto ficam no documento de handoff do produto, não nesta spec.

## 8. Implementação

### CSS (custom properties)

```css
:root {
  /* Famílias */
  --tcece-font-primary: 'Noto Sans', system-ui, sans-serif;
  --tcece-font-accent: 'Atkinson Hyperlegible Next', 'Noto Sans', system-ui, sans-serif; /* só números e labels */
  --tcece-font-mono: 'Fira Code', ui-monospace, monospace;

  /* Desktop (padrão) */
  /* proposto (T-14) */
  --tcece-display-2xl-size: 5rem; --tcece-display-2xl-weight: 700; --tcece-display-2xl-lh: 1.1;
  --tcece-display-xl-size: 4rem; --tcece-display-xl-weight: 700; --tcece-display-xl-lh: 1.1;
  --tcece-display-large-size: 3rem; --tcece-display-large-weight: 600; --tcece-display-large-lh: 1.2;
  --tcece-display-medium-size: 2.5rem; --tcece-display-medium-weight: 600; --tcece-display-medium-lh: 1.2;
  --tcece-display-small-size: 2rem; --tcece-display-small-weight: 600; --tcece-display-small-lh: 1.2;
  --tcece-title-2xl-size: 2rem; --tcece-title-2xl-weight: 600; --tcece-title-2xl-lh: 1.2;
  --tcece-title-lg-size: 1.5rem; --tcece-title-lg-weight: 600; --tcece-title-lg-lh: 1.4;
  --tcece-title-md-size: 1.25rem; --tcece-title-md-weight: 600; --tcece-title-md-lh: 1.4;
  --tcece-title-sm-size: 1rem; --tcece-title-sm-weight: 600; --tcece-title-sm-lh: 1.4;
  --tcece-body-lg-size: 1.125rem; --tcece-body-lg-weight: 400; --tcece-body-lg-lh: 1.6;
  --tcece-body-md-size: 1rem; --tcece-body-md-weight: 400; --tcece-body-md-lh: 1.6;
  --tcece-blockquote-size: 1.125rem; --tcece-blockquote-weight: 500; --tcece-blockquote-lh: 1.8;
  --tcece-code-size: 1rem; --tcece-code-weight: 600; --tcece-code-lh: 1.4;
  --tcece-caption-size: 1rem; --tcece-caption-weight: 400; --tcece-caption-lh: 1.4;

  /* Espaçamento de texto (seção 5): valor único para todos os tokens */
  --tcece-text-letter-spacing: 0;
  --tcece-text-word-spacing: 0;
  --tcece-paragraph-gap: 1.5rem; /* 24px, só texto corrido */
}

@media (max-width: 767px) {
  :root {
    --tcece-display-2xl-size: 2.75rem;
    --tcece-display-xl-size: 2.5rem;
    --tcece-display-large-size: 2.25rem;
    --tcece-display-medium-size: 1.75rem;
    --tcece-display-small-size: 1.5rem;
    --tcece-title-2xl-size: 1.5rem;
    --tcece-title-lg-size: 1.25rem;
    --tcece-title-md-size: 1.125rem;
  }
}

/* Noto Sans é o padrão de tudo; Atkinson só entra pelas duas regras abaixo */
body { font-family: var(--tcece-font-primary); font-size: var(--tcece-body-md-size); letter-spacing: var(--tcece-text-letter-spacing); word-spacing: var(--tcece-text-word-spacing); }

/* Texto corrido: espaço entre parágrafos */
.tcece-prose p + p { margin-block-start: var(--tcece-paragraph-gap); }

/* O texto nunca fica abaixo de 16px: não use `font-size` menor, nem `small`, nem `font-size: smaller` */
small { font-size: 1em; }

.tcece-form-label {
  font: var(--tcece-title-sm-weight) var(--tcece-title-sm-size)/var(--tcece-title-sm-lh) var(--tcece-font-accent);
}

.tcece-num {
  font-family: var(--tcece-font-accent);
  font-variant-numeric: tabular-nums;
}
```

Uso:

```css
.tcece-page-title   { font: var(--tcece-title-lg-weight) var(--tcece-title-lg-size)/var(--tcece-title-lg-lh) var(--tcece-font-primary); }
.tcece-form-label   { font: var(--tcece-title-sm-weight) var(--tcece-title-sm-size)/var(--tcece-title-sm-lh) var(--tcece-font-accent); } /* title-sm + Atkinson */
.tcece-table-cell   { font: var(--tcece-body-md-weight) var(--tcece-body-md-size)/var(--tcece-body-md-lh) var(--tcece-font-primary); }  /* body-md */
```

**Carregamento das fontes:** Noto Sans (400, 500, 600) e Atkinson Hyperlegible Next (400, 600) com `font-display: swap`. A pilha de fallback já está nas variáveis (`system-ui, sans-serif`). Verifique o suporte a `tabular-nums` na Atkinson antes de padronizar (7.1, item 6).

### TypeScript / MUI

- `designTokens.ts` atual está **incompleto** (faltam `title-2xl`, variantes mobile e tokens `special`; ainda tem `title-xs`, `title-ss` e `body-standard`, que foram removidos) e provavelmente ainda aponta Atkinson como família principal. Regenere a partir desta spec; não edite valores à mão.
- No `createTheme`, defina `typography.fontFamily` como **Noto Sans**. Atkinson entra só na variante do label e num utilitário de número (`.tcece-num` ou `sx`). Se o tema inteiro estiver com Atkinson, é o sintoma que gerou esta revisão.
- No MUI, crie variantes customizadas no `createTheme` com os nomes dos tokens (`title-lg`, `body-md`…) em vez de reaproveitar `h1`–`h6`/`body1`.
- Para os labels (`title-sm` em Atkinson), sobrescreva `fontFamily` em `MuiInputLabel`, `MuiFormLabel` e `MuiFormControlLabel` (se o label do checkbox/radio for considerado label, ver T-13).
- Em `DataGrid`, aplique `title-sm` no `columnHeader` e `body-md` no `cell` via `sx`; nas colunas numéricas, use `cellClassName: 'tcece-num'`.

## 9. Checklist de revisão

- [ ] Nenhum `font-size`, `font-weight`, `line-height`, `letter-spacing` ou `word-spacing` literal no código novo
- [ ] Nenhum `font-family` literal: a família vem de `--tcece-font-primary` (padrão) ou `--tcece-font-accent` (só números e labels)
- [ ] `body` e o tema do MUI em **Noto Sans**; Atkinson só em labels e números
- [ ] Labels de formulário (`title-sm`) em Atkinson; helper, input e cabeçalho de tabela em Noto Sans
- [ ] Contadores, IDs, colunas numéricas e números de paginação em Atkinson com `tabular-nums`; números dentro de frase em Noto Sans
- [ ] Título da página `title-lg`, seção `title-md`, subseção `title-sm`
- [ ] **Nenhum texto abaixo de 16px** (inclui chip, selo, helper, legenda, tooltip e rodapé)
- [ ] Cabeçalho de tabela `title-sm`, células `body-md`, paginação `body-md`
- [ ] Espaçamentos de layout conforme `spacing-spec-tce.md` (seção 11 dela)
- [ ] Espaçamento de texto (seção 5): letter-spacing e word-spacing `0`, parágrafos a 24px
- [ ] Componentes com texto usam `min-height` (nunca altura fixa), sem `overflow: hidden`; nada é cortado com line-height 1,5, parágrafo 2×, letter-spacing 0,12 em e word-spacing 0,16 em (WCAG 1.4.12)
- [ ] Tokens `title-*` têm override mobile (< 768px)
- [ ] Contraste de texto: `text/primary` ou `text/secondary` sobre `background/paper` ou `background/default`
- [ ] Estados (hover, focus, disabled, erro) usando as cores da seção 6
- [ ] Apenas **um** `title-lg` por página (o título da página); demais seções em `title-md`/`title-sm`
- [ ] Contadores e números de destaque **não** usam o mesmo token do título da página (T-14)
- [ ] Links em texto corrido sublinhados; cor nunca é o único indicador (erro, sucesso, status)
- [ ] Texto longo com largura máxima de 60–80 caracteres por linha
- [ ] Nenhuma fonte fora das famílias da seção 2 (sem SF Pro, Roboto etc. vindos de templates)

## 10. Contraste das cores de texto

Os contrastes de cada token de texto, link, botão e fundo estão em `color-spec-tce.md` (seções 3 a 6), calculados sobre os valores atuais do Figma. Os valores e a tabela antiga desta seção (baseados em #212121, #1976D2 etc.) foram substituídos. Regras que continuam valendo: placeholders são texto e atingem 4,5:1 (`tcece/text/placeholder`); cor nunca é o único indicador de erro, sucesso ou status.

## 11. Pontos em aberto

Todos os pontos em aberto de tipografia estão em **`decisoes-em-aberto.md`** (T-3 a T-6, T-9 a T-14; T-1 foi decidido em 2026-10-21; T-7 e T-8 foram resolvidos em 2026-10-27 pelo piso de 16px; T-2 foi resolvido em 2026-10-28 pela seção 5). Até a decisão, vale o valor desta spec.

## 12. Mapa Figma ↔ código

| Figma | Código | Observação |
|---|---|---|
| Coleção `Typography` (67 variáveis, modo único) | Variáveis `--tcece-*` da seção 8 | Nomes no Figma: `title/lg/desktop/fontSize`, `title/lg/mobile/fontSize`, `body/md/fontSize`, `special/code/fontWeight`… Os `display` e `title` têm desktop e mobile; `body` e `special` têm valor único |
| Variável `…/lineHeight` | `--tcece-<token>-lh` | No Figma o line-height está em **px** (o estilo de texto só aceita px quando ligado a variável); a razão da spec (1.2, 1.4, 1.6, 1.8) está na descrição da variável. No código use sempre o número sem unidade |
| `special/letterSpacing` | `--tcece-text-letter-spacing` | `0` em todos os tokens (seção 5) |
| `font/primary` e `font/accent` | `--tcece-font-primary` e `--tcece-font-accent` | A Atkinson se aplica ligando a variável `font/accent` à família do texto, **mantendo** o estilo `Spec/*`. Trocar a família à mão desliga o estilo |
| Estilos `Spec/display-large`, `-medium`, `-small`, `Spec/title-2xl`, `-lg`, `-md`, `-sm`, `Spec/body-lg`, `-md`, `Spec/blockquote`, `Spec/code`, `Spec/caption` (12) | Tokens de mesmo nome da seção 3 | Os estilos usam as variáveis acima. Só existem para desktop; os estilos mobile ainda não foram criados (pendência) |
| 51 estilos antigos (`Desktop/…`, `Mobile/…`) e coleção `Tipografia Responsiva` | Não usar | Em migração: serão apagados depois de migrar as outras páginas do arquivo |
| `fontWeight/*` e `lineHeight/tight`, `normal`, `relaxed` (primitivas antigas) | Não usar | Fora da escala; revisar na limpeza do Figma |

**Mapeamento para o MUI** (`theme.typography`): A DECIDIR (T-15). Dois nomes da escala colidem com variantes reservadas do `Typography` do MUI: `caption` e o estilo do botão (`button`).

## 13. Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 4.0.1 | 2026-10-28 | Nomes dos tokens de cor atualizados conforme `color-spec-tce.md` 2.0.0 (texto) |
| 4.0.0 | 2026-10-28 | Proposta `display-2xl`/`display-xl` e seção 3.1 (a aprovar, T-14); prefixo `tcece` nas variáveis CSS e classes (`--tcece-font-primary`, `--tcece-title-lg-size`, `.tcece-num`…); cabeçalho padrão (camada, depende de, usada por); seção 12 (mapa Figma ↔ código); botão aponta para `button-spec-tce.md` |
| 3.0.0 | 2026-10-28 | Escala única: tokens `button-*`, `form-*` e `table-*` removidos; espaçamento de texto definido (seção 5, fecha T-2 e E-2). Marcada como `ds-v3` (a confirmar) |
| 2.0.0 | 2026-10-27 | Piso de 16px; tokens `title-xs`, `title-ss` e `body-standard` removidos; `caption`, `code`, `form-helper` e `button-secondary` sobem para 16px. Marcada como `ds-v2` (a confirmar) |
| 1.1.0 | 2026-10-21 | Família tipográfica decidida: Noto Sans, com Atkinson só em números e labels (fecha T-1) |
| 1.0.0 | 2026-10-07 | Revisão estrutural (`ds-v1`) |
