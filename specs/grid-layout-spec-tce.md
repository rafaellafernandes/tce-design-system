# Spec de Grid e Layout — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade para grid (colunas, margem, gutter) e para o posicionamento das regiões da página (menu lateral, área de conteúdo). Os valores vêm das coleções **Grid** e **Layout** do arquivo ⭐ Design System TCE (páginas 📏 Grid e 🧱 Layout). Itens marcados **A DECIDIR** ainda não foram aprovados pelo design: não implemente esses pontos por conta própria, pergunte.
>
> Escala de espaçamento (gap e padding de componentes) está em `spacing-spec-tce.md`. Tipografia está em `typography-spec-tce.md`. Índice geral: `design-system-index.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **1.1.0** (rascunho) |
| **Última atualização** | **2026-10-07** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **1. Átomos (tokens de grid) e 4. Templates (posição das regiões da página)** |
| **Depende de** (data da última atualização lida) | `spacing-spec-tce.md` 2.0.0 (2026-10-28, escala) |
| **Usada por** | `button-spec-tce.md` (breakpoint do mobile), `padroes-de-interface.md` (colunas de tabela) e os templates de página |
| Arquivo e Figma | `specs/grid-layout-spec-tce.md`; variáveis de grid do ⭐ Design System TCE |

Histórico na última seção. Formato do cabeçalho: `design-system-index.md`, seção 4.1.

O que é token (margem, gutter, largura do menu) é Átomo; o posicionamento do menu lateral e da área de conteúdo é Template.

## 1. Regras obrigatórias

1. **Nunca use valores soltos** de margem lateral de página, gutter ou largura de menu. Use os tokens das seções 3 e 4.
2. **Margem e gutter mudam por breakpoint.** Cada token tem um valor por breakpoint (seção 3); no código, redefina a custom property em cada media query. Não fixe um valor só.
3. **A margem de página (`grid/margin`) vale só para o container da página.** Não use 80, 112 ou 40 como padding de componente: eles estão fora da escala de espaçamento de propósito.
4. **Estrutura:** Container (margem) › Row (gap = gutter) › Column. Não ponha padding lateral na Row nem na Column.
5. **Em telas com menu lateral, o grid vale só na área de conteúdo** ao lado do menu (seção 4). O menu não faz parte do grid.
6. Se nenhum token serve, pergunte ao design. Não crie valor novo.
7. Ao terminar uma tela, rode o checklist da seção 9.

## 2. Estrutura

Container (margem lateral) › Row (gap = gutter) › Column.

```css
.container { padding-inline: var(--tcece-grid-margin); }
.row { display: grid; grid-template-columns: repeat(var(--tcece-grid-columns), 1fr); column-gap: var(--tcece-grid-gutter); }
```

Nomes decididos (G-5): `--tcece-grid-*` e `--tcece-layout-*`.

## 3. Breakpoints e tokens (coleção Grid)

| Modo Figma | Largura de referência | `grid/columns` | `grid/margin` | `grid/gutter` | Coluna (calculada)* | Grid style |
|---|---|---|---|---|---|---|
| Desktop 12 | 1440 | 12 | 80 | 32 (→ `spacing/32`) | 77,3 | Desktop/12 colunas |
| Desktop 14 | 1920 | 14 | 112 | 32 (→ `spacing/32`) | 91,4 | Desktop/14 colunas |
| iPad | 834 | 8 | 40 | 32 (→ `spacing/32`) | 66,3 | Ipad/8 colunas |
| Mobile | 390 | 6 | 24 (→ `spacing/24`) | 24 (→ `spacing/24`) | 37 | Mobile/6 colunas |

**Onde cada modo começa (decidido, G-1):** as larguras da tabela são de **referência** (tamanho do quadro no Figma). No código:

| Modo | Começa em | Chave no MUI (`theme.breakpoints.values`) |
|---|---|---|
| Mobile | 0 a 767 | `xs: 0` |
| iPad | 768 a 1199 | `md: 768` |
| Desktop 12 | 1200 a 1919 | `lg: 1200` |
| Desktop 14 | 1920 em diante | `xl: 1920` |

`sm: 600` fica definido, mas o grid não o usa. Um monitor de 1366px cai em Desktop 12. O ponto de quebra de 768 é o da tipografia e do botão (T-10).

\* (largura − 2 × margem − (colunas − 1) × gutter) ÷ colunas.

O CSS original (`grid.css`) usa container com largura máxima de 1440 e padding lateral de 24 (1,5rem). Isso diverge do Figma. **Decidido (G-2): vale o Figma, margem 80 no desktop.** Telas largas usam o Desktop 14 (margem 112).

Unidades: os valores acima estão em px (Figma). No código, converta para rem (`px ÷ 16`): margem 80 = 5 rem, 112 = 7 rem, 40 = 2,5 rem, 24 = 1,5 rem; gutter 32 = 2 rem. Tabela completa em `design-system-index.md`, seção 5.

## 4. Layout com menu lateral (coleção Layout)

Telas com menu fixo à esquerda (como nos produtos com menu fixo) usam este modelo. O menu ocupa `layout/sidebar-width` e o grid vale **só na área de conteúdo**, que tem margem própria.

| Token | Desktop 12 | Desktop 14 | iPad | Mobile | Uso |
|---|---|---|---|---|---|
| `layout/sidebar-width` | 255 | 255 | 0 | 0 | Largura do menu lateral. No iPad e no Mobile vira drawer (seção 7, G-3) |
| `layout/margin-with-sidebar` | 48 (→ `spacing/48`) | 48 | = `grid/margin` (40) | = `grid/margin` (24) | Margem lateral da área de conteúdo quando há menu |

Grid styles: "Desktop/12 colunas com menu" e "Desktop/14 colunas com menu" (offset 48, gutter 32).

| Variante | Largura | Menu | Conteúdo | Área do grid | Coluna |
|---|---|---|---|---|---|
| Desktop 12 | 1440 | 255 | 1185 | 1089 | ≈ 61,4 |
| Desktop 14 | 1920 | 255 | 1665 | 1569 | ≈ 82,4 |

Área do grid = conteúdo − 2 × 48. Coluna = (área do grid − (colunas − 1) × 32) ÷ colunas.

```css
.layout  { display: flex; }
.sidebar { width: var(--tcece-layout-sidebar-width); flex: none; }
.content { flex: 1; padding-inline: var(--tcece-layout-margin-with-sidebar); }
/* dentro de .content, o mesmo .row da seção 2 */
```

O token adotado é 48 (dentro da escala). Valores diferentes em protótipos existentes (por exemplo, 46) seriam exceção registrada (G-4 decidida: vale 48).

## 5. Componentes e templates no Figma

| Componente | Página | Função | Variantes |
|---|---|---|---|
| `Grid / Container` | 📏 Grid | Margem lateral (padding = `grid/margin`) e grid style do breakpoint | Desktop 12, Desktop 14, iPad, Mobile |
| `Grid / Row` | 📏 Grid | Linha de colunas; gap = `grid/gutter` | idem |
| `Grid / Column` | 📏 Grid | Uma coluna; o número é uma propriedade de texto | — |
| `Layout / Página sem menu` | 🧱 Layout | Template com Grid / Container | Desktop 12, Desktop 14, iPad, Mobile |
| `Layout / Página com menu` | 🧱 Layout | Template com menu (placeholder) + área de conteúdo com o grid | Desktop 12, Desktop 14 |

O Figma ainda não tem o menu real dentro do template (só um placeholder) nem as regiões de cabeçalho e barra de ações fixa.

## 6. Como o conteúdo ocupa as colunas (decidido em 2026-10-28, G-6)

Larguras com menu lateral no Desktop 12 (coluna ≈ 61,4, gutter 32): 8 colunas ≈ 715px, que bate com a largura máxima de linha da tipografia (640 a 720px).

| Conteúdo | Desktop 12 (com menu) | Desktop 14 (com menu) | iPad (8) | Mobile (6) |
|---|---|---|---|---|
| Formulário e texto longo | 8 de 12 | 6 de 14 | 8 de 8 | 6 de 6 |
| Tabela | 12 de 12 | 14 de 14 | 8 de 8 (rolagem horizontal só na tabela) | 6 de 6 (idem) |
| Cards | 4 colunas cada (3 por linha) | 7 colunas cada (2 por linha); 3 ou 4 por linha não alinham com 14 colunas | 4 colunas cada (2 por linha) | 6 (1 por linha) |
| Modal | Largura fixa, centralizada, fora do grid | idem | idem | A largura toda menos a margem |

No MUI: `<Grid container columns={{ xs: 6, md: 8, lg: 12, xl: 14 }}>` com `size={{ xs: 6, md: 8, lg: 8, xl: 6 }}` no formulário.

## 7. Responsivo

- Os breakpoints são os 4 modos da seção 3, com as larguras de início decididas (G-1): 0, 768, 1200 e 1920.
- A escala de espaçamento é a mesma em todos os breakpoints; o que muda são os tokens de Grid e de Layout.
- **Menu lateral no iPad e no Mobile (decidido, G-3): drawer** (`Drawer` temporário do MUI) aberto por um botão de menu no cabeçalho; largura `layout/sidebar-width` (255), rótulos visíveis, itens com 44/48 de altura, foco preso enquanto aberto, `Esc` fecha e devolve o foco ao botão. Detalhes de animação e gesto: G-8.

## 8. Mapa Figma ↔ código

| Figma | Código (proposta) | Observação |
|---|---|---|
| `grid/columns`, `grid/margin`, `grid/gutter` | `--tcece-grid-columns`, `--tcece-grid-margin`, `--tcece-grid-gutter` | Redefinidos por breakpoint (um modo Figma = um bloco de media query) |
| `layout/sidebar-width`, `layout/margin-with-sidebar` | `--tcece-layout-sidebar-width`, `--tcece-layout-margin-with-sidebar` | Só em telas com menu |
| `Grid / Container`, `Grid / Row`, `Grid / Column` | `.container`, `.row`, `.col` | Code Connect ainda não mapeado |
| `Layout / Página sem menu`, `Layout / Página com menu` | `.layout`, `.sidebar`, `.content` | Code Connect ainda não mapeado |

Mudança de nomes no Figma (2026-10-05): `layout/columns`, `layout/margin` e `layout/gutter` viraram `grid/columns`, `grid/margin` e `grid/gutter`; as duas variáveis do menu foram para a coleção Layout. Quem tiver usado os nomes antigos precisa atualizar.

## 9. Checklist de revisão

- [ ] Margem lateral da página vem de `grid/margin` do breakpoint, sem valor literal
- [ ] Gutter vem de `grid/gutter`, sem `gap` literal entre colunas
- [ ] Em tela com menu: largura do menu = `layout/sidebar-width`; margem do conteúdo = `layout/margin-with-sidebar`
- [ ] Número de colunas conforme o breakpoint (12, 14, 8 ou 6)
- [ ] Margens de página (80, 112, 40) não usadas como padding de componente
- [ ] Comportamento do menu abaixo do desktop não implementado sem decisão do design

## 10. Pontos em aberto

Os pontos em aberto de grid e layout estão em **`decisoes-em-aberto.md`** (G-8); G-1 a G-7 estão decididas.

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 1.1.0 | 2026-10-28 | Larguras de início dos breakpoints e chaves do MUI (G-1), margem desktop 80 (G-2), drawer no iPad e Mobile (G-3), margem com menu 48 (G-4), nomes (G-5), ocupação de colunas por conteúdo (G-6); G-7 fechada |
| 1.0.0 | 2026-10-07 | Separada da spec de espaçamento (rascunho de 2026-10-05); revisão estrutural (`ds-v1`) |
