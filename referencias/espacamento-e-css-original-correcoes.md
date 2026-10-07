# Espaçamento: tokens do Figma × CSS original do TCE — correções para o repasse

> **Arquivo de referência**, não é spec viva: registra a análise de 2026-10-05. As decisões em aberto vivem em `../specs/decisoes-em-aberto.md` (E-1 a E-5).

Origem da análise: `index_v1.html` + pasta `css/` (variables_v1.css, typography_v1.css, components-form_v1.css, sections.css, main.css, reset.css) comparados com a spec de tipografia (`typography-spec-tce.md`) e com as variáveis criadas no arquivo ⭐ Design System TCE (página Spacing, coleção "Spacing"). Data: 2026-10-05.

## 1. O que foi aplicado no Figma (DS TCE, coleção "Spacing")

| Variável | Valor | Observação |
|---|---|---|
| `spacing/4` | 4 | rótulo → valor |
| `spacing/8` | 8 | label → campo; título → subtítulo |
| `spacing/12` | 12 | **em avaliação** (o CSS não usa) |
| `spacing/16` | 16 | entre campos; título → corpo; padding horizontal de botão e input |
| `spacing/24` | 24 | respiro em blocos e modais |
| `spacing/32` | 32 | seção → seção |
| `spacing/48` | 48 | respiro de página |
| `spacing/label-input` | → 8 | alias |
| `spacing/title-body` | → 16 | alias |
| `spacing/form-field-gap` | → 16 | alias |
| `spacing/section-section` | → 32 | alias |
| `spacing/card-padding` | → 16 | alias (ver decisão 3) |

As primitivas levam o valor no nome para **não colidir** com `--tcece-spacing-sm/md/lg/xl/2xl` do CSS, que têm outros valores (md=16, lg=18, xl=20, 2xl=24). Ainda não publicado na biblioteca.

## 2. Decisões pendentes (design)

Movidas para `../specs/decisoes-em-aberto.md` (E-1 a E-5), que é a lista única.

## 3. Correções no CSS original

- `--tcece-spacing-8xl` aponta para `--tcece-measure-11`, que não existe.
- Comentário errado em `--tcece-spacing-7xl` (diz 42px; o valor é 48px).
- `.title-desk-md` usa `--tcece-font-title-desk-lg-size` na declaração `font`, então o "md" renderiza com o tamanho do "lg".
- `p, blockquote` usa `font: var(--tcece-font-body-sm-size)`, que é um shorthand inválido: a fonte do parágrafo provavelmente não é aplicada.
- A versão antiga (`variables.css`) tem `--tcece-measure-0` = 8px; a v1 renumerou e `measure-0` virou 4px. Qualquer uso antigo mudou de valor.
- `--tcece-color-brand-secondary-01..04` declaradas duas vezes (a segunda sobrescreve a primeira); vários `var()` vazios; paleta de sistema com todos os valores iguais a `#194383`.
- `--tcece-font-family-04` está como `'Fire Code'` (o nome da fonte é Fira Code).
- Variáveis sem o prefixo (`--border-radius-sm`, `--font-weight-medium`, `--color-black-dark`) usadas em `typography_v1.css` e `components-form_v1.css`; `--border-radius-sm` e `--font-weight-medium` não são definidas em `variables_v1.css`.
- Em `components-form_v1.css`, os seletores `button.desk-lg, a.btn`, `button.desk-md, a.btn` etc. repetem `a.btn`, e a última regra vence para qualquer link com essa classe.

## 4. O que o CSS de fato usa de espaçamento

Padding de botão, input e select: 8px vertical e 16px horizontal, altura mínima 44px (NBR 17225); margem de 4px; padding do `pre` 8px; margem inferior de títulos 16px; subtítulos 16px acima e 32px abaixo; `section` com padding 32px. Os valores 80, 96 e 64px (`main`, `section`, `div`) são só layout da página de documentação. Todo o uso real cabe em 4, 8, 16 e 32.
